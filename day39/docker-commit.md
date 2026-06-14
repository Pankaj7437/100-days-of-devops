# 🚀 Create Docker Image from Running Container

## 📌 Objective

Create a new Docker image named **games:devops** from the running container **ubuntu_latest** on **Application Server 1 (stapp01)**.

---

# 🖥️ Environment Details

| Component          | Value                          |
| ------------------ | ------------------------------ |
| Server             | Application Server 1 (stapp01) |
| Existing Container | ubuntu_latest                  |
| New Image          | games:devops                   |

---

# 🔹 Step 1: Connect to Application Server 1

```bash
ssh tony@stapp01
```

---

# 🔹 Step 2: Verify the Running Container

List currently running containers:

```bash
docker ps
```

Expected output should show:

```text
ubuntu_latest
```

This confirms the source container exists and is running.

---

# 🔹 Step 3: Create a New Image from the Container

Create the image:

```bash
docker commit ubuntu_latest games:devops
```

### Explanation

* `docker commit` creates a new Docker image from an existing container.
* `ubuntu_latest` is the source container.
* `games:devops` is the name and tag of the new image.

Docker captures the current state of the container filesystem and saves it as a reusable image.

---

# 🔹 Step 4: Verify Image Creation

Check available images:

```bash
docker images
```

Expected output:

```text
REPOSITORY   TAG
games        devops
```

This confirms that the image was successfully created.

---

# 📖 Command Explanation

### docker commit

Syntax:

```bash
docker commit <container_name> <image_name>:<tag>
```

Example:

```bash
docker commit ubuntu_latest games:devops
```

Result:

```text
games:devops
```

A new image is created from the current state of the container.

---

# 🔍 Verification Commands

```bash
docker ps
docker images
```

Verify:

* Container `ubuntu_latest` exists and is running.
* Image `games:devops` exists in the local image repository.

---

# ⚡ Commands Used

```bash
ssh tony@stapp01

docker ps

docker commit ubuntu_latest games:devops

docker images
```

---

# ✅ Result

Successfully created a Docker image **games:devops** from the running container **ubuntu_latest** on **Application Server 1**, and verified its presence using `docker images`.
