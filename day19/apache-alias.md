# 🌐 DevOps Lab: Configure Apache with Alias (Multiple Sites on Port 3000)

![Linux](https://img.shields.io/badge/Platform-Linux-blue)
![Apache](https://img.shields.io/badge/WebServer-Apache-green)
![Status](https://img.shields.io/badge/Project-Completed-success)

---

## 📌 Overview

This lab demonstrates how to configure **Apache HTTP Server** to serve multiple websites using **Alias mapping** on a custom port.

Two website backups were provided on the jump host and deployed on the app server.

---

## 🎯 Objective

- Configure Apache on **App Server 3**
- Run Apache on **port 3000**
- Map URLs using Alias:
  - `/blog` → `/home/thor/blog`
  - `/cluster` → `/home/thor/cluster`
- Verify access using `curl`

---

## 🧠 Architecture

```
http://localhost:3000/blog     → /home/thor/blog
http://localhost:3000/cluster  → /home/thor/cluster
```

---

## 🛠️ Step 1: Connect to App Server

```bash
ssh banner@stapp03
```

---

## 📂 Step 2: Create Directory

```bash
sudo mkdir -p /home/thor
sudo chown banner:banner /home/thor
```

---

## 📥 Step 3: Copy Files from Jump Host

```bash
scp -r thor@jump-host:/home/thor/blog /home/thor/
scp -r thor@jump-host:/home/thor/cluster /home/thor/
```

---

## 🔍 Step 4: Verify Files

```bash
ls /home/thor
```

Expected:

```
blog  cluster
```

---

## ⚙️ Step 5: Configure Apache

```bash
sudo vi /etc/httpd/conf/httpd.conf
```

### Change Port

```
Listen 3000
```

---

### Add Alias Configuration

```
Alias /blog /home/thor/blog
Alias /cluster /home/thor/cluster

<Directory /home/thor/blog>
    Require all granted
</Directory>

<Directory /home/thor/cluster>
    Require all granted
</Directory>
```

---

## 🔄 Step 6: Restart Apache

```bash
sudo systemctl restart httpd
sudo systemctl enable httpd
```

---

## 🔍 Step 7: Verify Service

```bash
sudo systemctl status httpd
```

Expected:

```
active (running)
listening on port 3000
```

---

## 🧪 Step 8: Testing

```bash
curl http://localhost:3000/blog/
curl http://localhost:3000/cluster/
```

---

## ⚠️ Troubleshooting

| Issue | Cause | Fix |
|------|------|-----|
| Permission denied | Folder ownership issue | `chown` fix |
| 403 Forbidden | Access restriction | `Require all granted` |
| Port not working | Wrong config | Check `Listen 3000` |
| Empty output | Files missing | Verify `/home/thor` |

---

## 🔑 Key Learnings

- Apache Alias mapping
- Serving multiple apps on same server
- Port configuration in Apache
- File transfer using SCP
- Permission management in Linux

---

## 🚀 Real-World Use

- Hosting multiple apps on a single server
- Microservices frontend routing
- Reverse proxy setups

---

## 👨‍💻 Author

**Pankaj Sharma**  
DevOps Learner 🚀

---

## ⭐ Support

If you found this useful, give it a ⭐ on GitHub!
