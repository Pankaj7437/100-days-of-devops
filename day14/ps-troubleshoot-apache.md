# Apache Service Troubleshooting – Fix Apache Service on App Servers

## Objective
The monitoring system in the Nautilus infrastructure reported that the **Apache service was unavailable on one of the application servers** in the Stratos Data Center.

The task was to:

- Identify the faulty application server
- Fix the issue preventing Apache from running
- Ensure Apache is running on **port 3000**
- Ensure Apache service is **running on all application servers**
- Similar to task 12
---

# Environment Details

| Parameter | Value |
|----------|------|
| Infrastructure | Nautilus |
| Data Center | Stratos DC |
| Service | Apache (httpd) |
| Required Port | 3000 |
| Application Servers | stapp01, stapp02, stapp03 |

---

# Step 1 – Connect to App Server 1

```bash
ssh tony@stapp01
```

Check Apache service status:

```bash
sudo systemctl status httpd
```

Output showed:

```
Active: failed
Address already in use
```

### Problem Identified

Apache failed to start because **port 3000 was already in use**.

---

# Step 2 – Identify Process Using Port 3000

Check which process is occupying the port.

```bash
sudo ss -tulpn | grep 3000
```

Output:

```
tcp LISTEN 127.0.0.1:3000 users:(("sendmail",pid=20694))
```

### Root Cause

The **sendmail service** was already using **port 3000**, preventing Apache from binding to the port.

---

# Step 3 – Stop the Conflicting Process

Terminate the process using port 3000.

```bash
sudo kill -9 20694
```

Verify that port 3000 is now free:

```bash
sudo ss -tulpn | grep 3000
```

No output confirms the port is free.

---

# Step 4 – Start Apache Service

Start Apache again.

```bash
sudo systemctl start httpd
```

Enable Apache to start automatically on boot.

```bash
sudo systemctl enable httpd
```

---

# Step 5 – Verify Apache Service

Check service status.

```bash
sudo systemctl status httpd
```

Expected output:

```
Active: active (running)
Server configured, listening on: port 3000
```

---

# Step 6 – Verify Other Application Servers

Repeat verification on other servers.

### App Server 2

```bash
ssh steve@stapp02
sudo systemctl status httpd
```

Apache service confirmed **running on port 3000**.

---

### App Server 3

```bash
ssh banner@stapp03
sudo systemctl status httpd
```

Apache service confirmed **running on port 3000**.

---

# Commands Cheat Sheet

```bash
ssh tony@stapp01

sudo systemctl status httpd

sudo ss -tulpn | grep 3000

sudo kill -9 <PID>

sudo systemctl start httpd
sudo systemctl enable httpd

sudo systemctl status httpd
```

---

# Common Mistakes

| Mistake | Problem |
|-------|--------|
| Restarting Apache repeatedly | Does not fix port conflict |
| Not checking port usage | Root cause remains hidden |
| Forgetting to free port | Apache cannot bind to port |
| Fixing only one server | Task requires verification on all app servers |

---

# Key Concepts Learned

- Apache service troubleshooting
- Port conflict diagnosis
- Using `ss` command to check open ports
- Killing conflicting processes
- Managing services using `systemctl`

---

# Conclusion

The Apache service failure was caused by a **port conflict on port 3000**, where the **sendmail process was already listening on the port**. After terminating the conflicting process, Apache was successfully started and enabled. Verification confirmed that Apache is running properly on **all application servers in the Stratos data center**.
