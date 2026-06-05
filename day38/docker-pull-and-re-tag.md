# 🚀 Pull and Re-tag Docker Image (KodeKloud Lab)

## 📌 Objective

On **App Server 2 (stapp02)**:

1. Pull the image:

```bash
busybox:musl
```

2. Create a new tag:

```bash
busybox:local
```

---

# 🖥️ Server Details

| Item         | Value                    |
| ------------ | ------------------------ |
| Server       | App Server 2 (`stapp02`) |
| Source Image | `busybox:musl`           |
| New Tag      | `busybox:local`          |

---

# 🔹 Step 1: Connect to App Server 2

```bash
ssh steve@stapp02
```

---

# 🔹 Step 2: Pull Image

```bash
docker pull busybox:musl
```

### Verify

```bash
docker images
```

Expected:

```text
busybox    musl
```

---

# 🔹 Step 3: Create New Tag

```bash
docker tag busybox:musl busybox:local
```

### Explanation

* Source image:

```text
busybox:musl
```

* New image tag:

```text
busybox:local
```

No new image is created; Docker simply adds another tag pointing to the same image ID.

---

# 🔹 Step 4: Verify Tag

```bash
docker images
```

Expected output:

```text
REPOSITORY   TAG
busybox      musl
busybox      local
```

Both tags should have the same IMAGE ID.

---

# 📖 Command Explanation

### Pull Image

```bash
docker pull busybox:musl
```

Downloads the BusyBox image with the `musl` tag from Docker Hub.

---

### Create Tag

```bash
docker tag busybox:musl busybox:local
```

Creates a second tag (`local`) for the same image.

---

# ⚡ Commands Summary

```bash
ssh steve@stapp02

docker pull busybox:musl

docker tag busybox:musl busybox:local

docker images
```

---

# ✅ Final Result

✔ Connected to App Server 2
✔ Pulled `busybox:musl` image
✔ Created new tag `busybox:local`
✔ Verified both tags exist
✔ KodeKloud task completed successfully 🎉
