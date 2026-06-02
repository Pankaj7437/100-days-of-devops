# 🚀 Deploy Nginx Alpine Container on App Server 1

## 📌 Objective

Deploy an Nginx container on **Application Server 1 (stapp01)** with the following requirements:

* Use image: `nginx:alpine`
* Container name: `nginx_1`
* Container must remain in **running** state

---

# 🖥️ Server Details

| Item           | Value                            |
| -------------- | -------------------------------- |
| Server         | Application Server 1 (`stapp01`) |
| User           | tony                             |
| Container Name | nginx_1                          |
| Image          | nginx:alpine                     |

---

# 🔹 Step 1: Connect to Application Server 1

```bash
ssh tony@stapp01
```

Enter the password when prompted.

---

# 🔹 Step 2: Pull Nginx Alpine Image

```bash
docker pull nginx:alpine
```

### Explanation

* `docker pull` downloads an image from Docker Hub.
* `nginx` is the web server image.
* `alpine` is a lightweight Linux-based version of Nginx.

Verify image:

```bash
docker images
```

Expected output:

```text
nginx    alpine
```

---

# 🔹 Step 3: Create and Start Container

```bash
docker run -d --name nginx_1 nginx:alpine
```

### Command Breakdown

| Option           | Description                                  |
| ---------------- | -------------------------------------------- |
| `docker run`     | Creates a new container                      |
| `-d`             | Runs container in background (detached mode) |
| `--name nginx_1` | Assigns container name                       |
| `nginx:alpine`   | Image used for container                     |

---

# 🔹 Step 4: Verify Container Status

```bash
docker ps
```

Expected output:

```text
CONTAINER ID   IMAGE          STATUS
xxxxxxx        nginx:alpine   Up
```

Container name should appear as:

```text
nginx_1
```

---

# 🔹 Optional Verification

Check container state:

```bash
docker inspect -f '{{.State.Running}}' nginx_1
```

Expected:

```text
true
```

---

# 📖 Concepts Used

### Docker Image

A template used to create containers.

Example:

```text
nginx:alpine
```

---

### Docker Container

A running instance of an image.

Example:

```text
nginx_1
```

---

### Detached Mode

```bash
-d
```

Runs the container in the background without occupying the terminal.

---

# ⚡ Commands Summary

```bash
ssh tony@stapp01

docker pull nginx:alpine

docker run -d --name nginx_1 nginx:alpine

docker ps
```

---

# ✅ Final Result

✔ Connected to Application Server 1
✔ Downloaded `nginx:alpine` image
✔ Created container `nginx_1`
✔ Container running successfully in detached mode
✔ Verified container status using `docker ps`
✔ KodeKloud task completed successfully 🎉
