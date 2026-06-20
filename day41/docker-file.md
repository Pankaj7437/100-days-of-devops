# 🚀 Build Custom Docker Image with Apache on Port 3002

## 📌 Objective

Create a **Dockerfile** at:

```bash
/opt/docker/Dockerfile
```

and build a custom Docker image with the following requirements:

* Base Image: `ubuntu:24.04`
* Install Apache2
* Configure Apache to listen on port **3002**
* Do not modify other Apache settings (DocumentRoot, VirtualHosts, etc.)

---

# 🖥️ Environment Details

| Component       | Value                  |
| --------------- | ---------------------- |
| Server          | App Server 3 (stapp03) |
| Dockerfile Path | /opt/docker/Dockerfile |
| Base Image      | ubuntu:24.04           |
| Web Server      | apache2                |
| Listening Port  | 3002                   |

---

# 🔹 Step 1: Connect to App Server 3

```bash
ssh banner@stapp03
```

---

# 🔹 Step 2: Create Dockerfile Directory

```bash
sudo mkdir -p /opt/docker
cd /opt/docker
```

---

# 🔹 Step 3: Create Dockerfile

```bash
sudo vi /opt/docker/Dockerfile
```

Contents:

```dockerfile
FROM ubuntu:24.04

RUN apt-get update && \
    apt-get install -y apache2

RUN sed -i 's/Listen 80/Listen 3002/' /etc/apache2/ports.conf

EXPOSE 3002

CMD ["apachectl","-D","FOREGROUND"]
```

---

# 📖 Dockerfile Explanation

### Base Image

```dockerfile
FROM ubuntu:24.04
```

Uses Ubuntu 24.04 as the parent image.

---

### Install Apache

```dockerfile
RUN apt-get update && \
    apt-get install -y apache2
```

* Updates package metadata.
* Installs Apache web server.

---

### Change Listening Port

```dockerfile
RUN sed -i 's/Listen 80/Listen 3002/' /etc/apache2/ports.conf
```

Modifies only the Apache listening port.

Before:

```apache
Listen 80
```

After:

```apache
Listen 3002
```

No other Apache configuration is changed.

---

### Expose Port

```dockerfile
EXPOSE 3002
```

Documents that the container uses port 3002.

---

### Start Apache

```dockerfile
CMD ["apachectl","-D","FOREGROUND"]
```

Starts Apache in foreground mode so the container remains running.

---

# 🔹 Step 4: Build Docker Image

```bash
cd /opt/docker

sudo docker build -t custom-apache .
```

Expected:

```text
Successfully built
Successfully tagged custom-apache:latest
```

---

# 🔹 Step 5: Verify Image

```bash
sudo docker images
```

Example:

```text
REPOSITORY      TAG       IMAGE ID
custom-apache   latest    xxxxxxxxx
```

---

# 🔍 Validation Commands

Check Dockerfile:

```bash
cat /opt/docker/Dockerfile
```

Build image:

```bash
sudo docker build -t custom-apache .
```

List images:

```bash
sudo docker images
```

---

# ⚡ Commands Used

```bash
ssh banner@stapp03

sudo mkdir -p /opt/docker
cd /opt/docker

sudo vi Dockerfile

sudo docker build -t custom-apache .

sudo docker images
```

---

# ✅ Result

Successfully created **/opt/docker/Dockerfile** using **ubuntu:24.04** as the base image, installed **apache2**, configured Apache to listen on **port 3002**, and built the Docker image successfully.
