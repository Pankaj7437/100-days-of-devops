# Dockerize and Deploy Python Application – App Server 3

## 📌 Lab Overview

This repository contains the deployment steps for containerizing a Python application and deploying it on App Server 3. The application dependencies are pre-configured, and the deployment utilizes a custom Docker image to map the application's internal port to a designated host port.

---

## 🎯 Requirements

| Requirement | Configuration |
| --- | --- |
| **Server** | App Server 3 (`stapp03`) |
| **Application Directory** | `/python_app` |
| **Requirements File** | `/python_app/src/requirements.txt` |
| **Dockerfile** | `/python_app/Dockerfile` |
| **Base Image** | `python:latest` |
| **Application Script** | `server.py` |
| **Container Port** | `5001` |
| **Host Port** | `8093` |
| **Image Name** | `nautilus/python-app` |
| **Container Name** | `pythonapp_nautilus` |

---

## 🚀 Deployment Steps

### 1. Connect to App Server 3

Log in to the designated application server from your jump host.

```bash
ssh banner@stapp03
cd /python_app/

```

### 2. Create the Dockerfile

Create a `Dockerfile` inside the `/python_app` directory to package the application.

```bash
sudo nano Dockerfile

```

Add the following configuration:

```dockerfile
FROM python:latest

WORKDIR /app

COPY src/requirements.txt .

RUN pip install --no-cache-dir -r requirements.txt

COPY src/server.py .

EXPOSE 5001

CMD ["python", "server.py"]

```

*(Note: Ensure paths are typed correctly as `server.py`, and use the `EXPOSE` instruction, not `EXPORT`.)*

### 3. Build the Docker Image

Build the image using the current directory (`.`) as the build context.

```bash
docker build -t nautilus/python-app .

```

Verify the image was created successfully:

```bash
docker images

```

*Expected Output:* You should see `nautilus/python-app` with the `latest` tag.

### 4. Create and Run the Container

Run the container in detached mode (`-d`), name it appropriately, and map host port `8093` to container port `5001`.

```bash
docker container run -d --name pythonapp_nautilus -p 8093:5001 nautilus/python-app

```

Check that the container is running:

```bash
docker ps

```

### 5. Test the Application

Verify that the application is accessible on the host port.

```bash
curl http://localhost:8093/

```

*Expected Output:*
`Welcome to xFusionCorp Industries!`

---

## 📊 Deployment Architecture

```text
 App Server 3 (Host: 8093)
       │
       ▼
 ┌─────────────────────────┐
 │ pythonapp_nautilus      │
 │ Container Port: 5001    │
 │   │                     │
 │   ▼                     │
 │ server.py (Python)      │
 └─────────────────────────┘

```
