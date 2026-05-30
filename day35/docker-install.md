# 🚀 Docker CE & Docker Compose Installation on App Server 1

## 📌 Objective

Install and configure Docker on **App Server 1**:

* Install `docker-ce`
* Install Docker Compose
* Start Docker service
* Enable Docker service at boot

---

# 🖥️ Server Details

| Item   | Value                    |
| ------ | ------------------------ |
| Server | App Server 1 (`stapp01`) |
| OS     | CentOS Stream 9 / EL9    |
| User   | tony                     |

---

# ⚠️ Initial Issue

When attempting installation:

```bash
sudo yum install docker-ce docker-compose
```

Error received:

```text
No match for argument: docker-ce
No match for argument: docker-compose
Unable to find a match
```

### Reason

The Docker CE repository was not configured on the server, so the package manager could not locate Docker packages.

---

# 🔧 Solution

## Step 1: Install DNF Plugin

Required to add external repositories.

```bash
sudo dnf install -y dnf-plugins-core
```

---

## Step 2: Add Docker Repository

```bash
sudo dnf config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
```

### Purpose

Adds Docker's official package repository to the system.

---

## Step 3: Refresh Repository Metadata

```bash
sudo dnf makecache
```

### Purpose

Downloads latest package information from configured repositories.

---

## Step 4: Install Docker CE

```bash
sudo dnf install -y docker-ce
```

### Purpose

Installs Docker Engine Community Edition.

---

## Step 5: Install Docker Compose Plugin

```bash
sudo dnf install -y docker-compose-plugin
```

### Purpose

Installs Docker Compose v2 plugin.

---

# ▶️ Start Docker Service

## Step 6: Start Docker

```bash
sudo systemctl start docker
```

### Purpose

Starts Docker daemon (`dockerd`) immediately.

---

## Step 7: Enable Docker at Boot

```bash
sudo systemctl enable docker
```

### Purpose

Ensures Docker starts automatically after server reboot.

---

# 🔍 Verification

## Check Docker Version

```bash
docker --version
```

Example:

```text
Docker version 28.x.x
```

---

## Check Docker Compose Version

```bash
docker compose version
```

Example:

```text
Docker Compose version v2.x.x
```

---

## Verify Docker Service

```bash
systemctl status docker
```

Expected:

```text
Active: active (running)
```

---

Or:

```bash
systemctl is-active docker
```

Expected:

```text
active
```

---

# 📖 Command Explanation

### Install Docker CE

```bash
sudo dnf install -y docker-ce
```

Installs Docker Engine used for creating and managing containers.

---

### Install Docker Compose Plugin

```bash
sudo dnf install -y docker-compose-plugin
```

Provides Compose functionality for managing multi-container applications.

---

### Start Docker Service

```bash
sudo systemctl start docker
```

Starts Docker daemon.

---

### Enable Docker Service

```bash
sudo systemctl enable docker
```

Configures Docker to start automatically on system boot.

---

# ⚡ Complete Command Summary

```bash
sudo dnf install -y dnf-plugins-core

sudo dnf config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

sudo dnf makecache

sudo dnf install -y docker-ce docker-compose-plugin

sudo systemctl start docker

sudo systemctl enable docker

docker --version

docker compose version

systemctl status docker
```

---

# ✅ Final Result

✔ Docker CE installed successfully
✔ Docker Compose plugin installed successfully
✔ Docker service started
✔ Docker service enabled at boot
✔ Docker verified and operational on App Server 1
✔ KodeKloud task completed successfully 🎉
