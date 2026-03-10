# Day 09 – Troubleshooting MariaDB Service Failure

## Objective
Investigate and resolve an issue where the Nautilus application was unable to connect to the database because the **MariaDB service was down on the database server (stdb01)**.

---

## Initial Investigation

First, I logged into the database server from the jump host.

```bash
ssh peter@stdb01
```

Then I checked the MariaDB service status.

```bash
systemctl status mariadb
```

Output showed:

```
inactive (dead)
```

This confirmed that the database service was not running.

---

## Attempt to Restart Service

I attempted to restart the service:

```bash
sudo systemctl restart mariadb
```

However, the service failed with the error:

```
Job for mariadb.service failed because the control process exited with error code
```

This indicated that the issue required deeper investigation.

---

## Checking Service Logs

To diagnose the problem, I checked the detailed logs.

```bash
journalctl -xeu mariadb.service
```

The logs indicated that MariaDB could not start properly and exited with status code **1 (FAILURE)**.

---

## Checking Disk Space

Since databases may fail if the disk is full, I verified the available disk space.

```bash
df -h
```

The system had sufficient free space, so disk space was not the cause.

---

## Troubleshooting Attempts

### Attempt 1 – Reinitializing the Database

I attempted to initialize the database again.

```bash
sudo mariadb-install-db --user=mysql --datadir=/var/lib/mysql
```

Output:

```
mysql.user table already exists
Run mysql_upgrade instead
```

This indicated that the database had already been initialized.

---

### Attempt 2 – Recreating the Data Directory

I removed and recreated the MariaDB data directory.

```bash
sudo rm -rf /var/lib/mysql
sudo mkdir /var/lib/mysql
sudo chown mysql:mysql /var/lib/mysql
```

Then initialized the database again.

```bash
sudo mysql_install_db --user=mysql
```

Although initialization completed successfully, the service still failed to start.

---

## Mistakes During Troubleshooting

During troubleshooting, I made a few mistakes which helped me understand the system better.

### 1. Disabling the service accidentally

```bash
sudo systemctl disable mariadb.service
```

This disabled MariaDB from starting automatically.

### 2. Typographical errors

I mistakenly used incorrect commands:

```
systemtctl
mariad.service
```

Correct commands:

```
systemctl
mariadb.service
```

### 3. Recreating only the data directory

I recreated `/var/lib/mysql` but missed another required runtime directory.

---

## Root Cause

The actual issue was that the **MariaDB runtime directory `/run/mariadb` was missing**.

MariaDB requires this directory to create runtime files such as socket and PID files. Without it, the service fails during startup.

---

## Final Solution

Create the runtime directory:

```bash
sudo mkdir -p /run/mariadb
```

Set the correct ownership:

```bash
sudo chown mysql:mysql /run/mariadb
```

Start the MariaDB service:

```bash
sudo systemctl start mariadb
```

Enable service on boot:

```bash
sudo systemctl enable mariadb
```

---

## Verification

Check service status:

```bash
sudo systemctl status mariadb
```

Expected output:

```
active (running)
```

This confirmed that the MariaDB service was successfully restored.

---

## Commands Used

| Command | Purpose |
|------|------|
| `systemctl status mariadb` | Check MariaDB service status |
| `systemctl start mariadb` | Start MariaDB service |
| `systemctl enable mariadb` | Enable service at boot |
| `journalctl -xeu mariadb.service` | View service logs |
| `df -h` | Check disk space |
| `mkdir` | Create directory |
| `chown` | Change ownership |
| `mysql_install_db` | Initialize database |

---

## Key Learnings

- Always check service status before troubleshooting.
- Use logs (`journalctl`) to identify the root cause.
- Avoid making assumptions without verifying system state.
- Systematic troubleshooting helps resolve complex issues faster.

This task simulated a **real-world production support scenario** where proper debugging and root cause analysis were required to restore a critical database service.
