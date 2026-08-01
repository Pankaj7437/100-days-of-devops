# Deploying an Apache (httpd) Web Server Using Docker Compose

## Objective

The objective of this lab is to deploy an **Apache (httpd)** web server inside a Docker container using **Docker Compose**. The container should be configured according to the given requirements:

- Create a Docker Compose file named **docker-compose.yml** inside **/opt/docker/**
- Use the **httpd:latest** image
- Create a container named **httpd**
- Map **host port 3002** to **container port 80**
- Mount the host directory **/opt/finance** to **/usr/local/apache2/htdocs** inside the container
- Start the container using Docker Compose

---

# Prerequisites

- Docker Engine installed
- Docker Compose installed
- SSH access to **Application Server 3**
- Existing host directory:

```
/opt/finance
```

---

# Step 1: Connect to Application Server 3

```bash
ssh banner@stapp03
```

Move to the Docker directory.

```bash
cd /opt/docker
```

---

# Step 2: Create Docker Compose File

Create the compose file.

```bash
vi docker-compose.yml
```

Paste the following configuration.

```yaml
version: "3.8"

services:
  web:
    image: httpd:latest
    container_name: httpd

    ports:
      - "3002:80"

    volumes:
      - /opt/finance:/usr/local/apache2/htdocs
```

Save and exit.

---

# Docker Compose File Explanation

## Version

```yaml
version: "3.8"
```

Defines the Docker Compose specification version.

---

## Services

```yaml
services:
```

Contains all services (containers) managed by Docker Compose.

---

## Service Name

```yaml
web:
```

Logical name of the service.

It can be any valid name because the actual container name is defined separately.

---

## Image

```yaml
image: httpd:latest
```

Uses the latest official Apache HTTP Server image from Docker Hub.

If it is not available locally, Docker automatically downloads it.

---

## Container Name

```yaml
container_name: httpd
```

Creates the container with the exact name:

```
httpd
```

instead of Docker generating a random name.

---

## Port Mapping

```yaml
ports:
  - "3002:80"
```

Maps

```
Host Port      → 3002
Container Port → 80
```

Users can access the Apache server using

```
http://<Server-IP>:3002
```

---

## Volume Mapping

```yaml
volumes:
  - /opt/finance:/usr/local/apache2/htdocs
```

Maps the host directory

```
/opt/finance
```

to Apache's default document root

```
/usr/local/apache2/htdocs
```

This allows Apache to directly serve files stored in the host directory.

---

# Step 3: Validate the Compose File (Optional)

Before deployment, verify the syntax.

```bash
docker compose config
```

If there are no errors, continue.

---

# Step 4: Deploy the Container

Start the container.

```bash
docker compose up -d
```

or

```bash
docker-compose up -d
```

The **-d** flag runs the container in detached mode.

---

# Step 5: Verify the Container

Check whether the container is running.

```bash
docker ps
```

Example Output

```
CONTAINER ID   IMAGE          STATUS
xxxxxx         httpd:latest   Up
```

---

# Step 6: Verify Port Mapping

```bash
docker port httpd
```

Expected output

```
80/tcp -> 0.0.0.0:3002
```

---

# Step 7: Verify Volume Mount

Inspect the container.

```bash
docker inspect httpd
```

Look under **Mounts**.

Expected values

```
Source:
/opt/finance

Destination:
/usr/local/apache2/htdocs
```

---

# Step 8: Test the Web Server

Open a browser or use curl.

```bash
curl http://localhost:3002
```

If the host directory contains website files, Apache will serve them.

---

# Architecture Diagram

```
                 Client Browser
                        │
                        │
           http://Server-IP:3002
                        │
                        ▼
       +--------------------------------+
       | Docker Host (Application Server)|
       |                                |
       |         Port 3002              |
       +---------------+----------------+
                       │
                       ▼
             +----------------------+
             |   Apache Container   |
             |      httpd           |
             |      Port 80         |
             |                      |
             | /usr/local/apache2   |
             |      /htdocs         |
             +----------+-----------+
                        │
                Bind Mount Volume
                        │
                        ▼
                /opt/finance (Host)
```

---

# Complete Command Summary

```bash
ssh banner@stapp03

cd /opt/docker

vi docker-compose.yml

docker compose config

docker compose up -d

docker ps

docker port httpd

docker inspect httpd

curl http://localhost:3002
```

---

# Key Concepts Learned

### Docker Compose

Docker Compose allows deploying applications using a YAML configuration file, making deployments simple, repeatable, and easy to manage.

---

### Service

A service represents a container managed by Docker Compose.

---

### Image

The image (`httpd:latest`) acts as the blueprint for creating the Apache container.

---

### Container

A running instance of the Docker image.

---

### Port Mapping

Maps traffic from the host machine to the container.

```
3002 (Host)
      │
      ▼
80 (Apache Container)
```

---

### Volume Mapping

Shares files between the host and container.

```
Host

/opt/finance

↓

Container

/usr/local/apache2/htdocs
```

This ensures website content persists even if the container is recreated.

---

### Detached Mode

```
docker compose up -d
```

Runs containers in the background.

---

### Docker Inspect

Displays detailed container configuration such as:

- Port mappings
- Mounted volumes
- Network settings
- Environment variables

---

# Real-World Use Cases

- Hosting static websites
- Deploying Apache using Infrastructure as Code
- Managing web servers with Docker Compose
- Persistent website storage using bind mounts
- Simplified application deployment in DevOps environments

---

# Learning Outcome

After completing this lab, I learned how to:

- Deploy Apache using Docker Compose
- Create and configure a `docker-compose.yml` file
- Pull and use the official `httpd` image
- Configure custom container names
- Map host ports to container ports
- Mount host directories as Docker volumes
- Validate Compose configurations
- Inspect running containers and verify deployments

---
