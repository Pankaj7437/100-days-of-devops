# Day 03 – Disable Direct SSH Root Login

## Objective
Disable direct SSH root login on all application servers to enhance security and enforce user-level access.

**Target Servers**
- stapp01 (User: tony)
- stapp02 (User: steve)
- stapp03 (User: banner)

---

## Steps Performed

### 1. Access the Jump Host
```bash
ssh thor@jump_host.stratos.xfusioncorp.com
```

---

### 2. Connect to Each Application Server

**stapp01**
```bash
ssh tony@stapp01
```

**stapp02**
```bash
ssh steve@stapp02
```

**stapp03**
```bash
ssh banner@stapp03
```

---

### 3. Modify SSH Configuration
Edit the SSH daemon configuration file on each server:

```bash
sudo vi /etc/ssh/sshd_config
```

Locate the parameter:

```
#PermitRootLogin yes
```

Update it to:

```
PermitRootLogin no
```

(If the parameter is missing, add it manually.)

---

### 4. Restart SSH Service
```bash
sudo systemctl restart sshd
```

---

### 5. Verification
From the jump host, confirm that root login is disabled:

```bash
ssh root@stapp01
ssh root@stapp02
ssh root@stapp03
```

Expected result:
```
Permission denied
```

---

## Summary
Direct SSH root login was disabled across all application servers by updating the `sshd_config` file and restarting the SSH service, ensuring compliance with security best practices.
