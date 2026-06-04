# 🚀 Copy File from Docker Host to Running Container

## 📌 Objective

A container named **ubuntu_latest** is already running on **App Server 1**.

Copy the encrypted file:

```bash
/tmp/nautilus.txt.gpg
```

from the Docker host into the container at:

```bash
/home/
```

without modifying the file.

---

# 🖥️ Server Details

| Item        | Value                    |
| ----------- | ------------------------ |
| Server      | App Server 1 (`stapp01`) |
| Container   | `ubuntu_latest`          |
| Source File | `/tmp/nautilus.txt.gpg`  |
| Destination | `/home/`                 |

---

# 🔹 Step 1: Connect to App Server 1

```bash
ssh tony@stapp01
```

---

# 🔹 Step 2: Verify Container is Running

```bash
docker ps
```

Expected output should show:

```text
ubuntu_latest
```

---

# 🔹 Step 3: Copy File into Container

```bash
docker cp /tmp/nautilus.txt.gpg ubuntu_latest:/home/
```

### Explanation

| Part                  | Purpose                                |
| --------------------- | -------------------------------------- |
| docker cp             | Copy files between host and container  |
| /tmp/nautilus.txt.gpg | Source file on host                    |
| ubuntu_latest         | Container name                         |
| /home/                | Destination directory inside container |

---

# 🔹 Step 4: Verify File Inside Container

```bash
docker exec -it ubuntu_latest ls /home/
```

Expected output:

```text
nautilus.txt.gpg
```

---

# 🔹 Alternative Verification

Check directly inside container:

```bash
docker exec -it ubuntu_latest bash
```

Then:

```bash
ls -l /home/
```

Expected:

```text
nautilus.txt.gpg
```

Exit container:

```bash
exit
```

---

# 📖 Command Explanation

### docker cp

```bash
docker cp SOURCE CONTAINER:DESTINATION
```

Used to transfer files between Docker host and container without changing file contents.

Example:

```bash
docker cp /tmp/nautilus.txt.gpg ubuntu_latest:/home/
```

Copies the encrypted file into the container's `/home` directory.

---

### docker exec

```bash
docker exec -it ubuntu_latest ls /home/
```

Runs a command inside the running container.

---

# ⚡ Commands Summary

```bash
ssh tony@stapp01

docker ps

docker cp /tmp/nautilus.txt.gpg ubuntu_latest:/home/

docker exec -it ubuntu_latest ls /home/
```

---

# ✅ Final Result

✔ Connected to App Server 1
✔ Verified container `ubuntu_latest` is running
✔ Copied `/tmp/nautilus.txt.gpg` into container
✔ File placed in `/home/` directory
✔ Verified file exists inside container
✔ File remained unchanged during transfer
✔ KodeKloud task completed successfully 🎉
