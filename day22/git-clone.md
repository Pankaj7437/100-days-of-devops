# 🚀 Git Repository Clone (KodeKloud Lab)

## 📌 Problem Statement
The DevOps team created a Git repository earlier, which now needs to be cloned on the **Storage Server (ststor01)** for development purposes.

---

## 🎯 Objective
- Locate the repository at `/opt/official.git`
- Clone it into `/usr/src/kodekloudrepos`
- Perform all operations using the `natasha` user
- Do not modify permissions or existing directories

---

## 🧠 Understanding the Task

- The given repository is a **bare repository**
- Bare repositories do not contain working files
- Cloning creates a working directory copy

---

## ⚙️ Steps Performed

### 🔹 Step 1: SSH into Storage Server

```bash
ssh natasha@ststor01
````

---

### 🔹 Step 2: Navigate to Target Directory

```bash
cd /usr/src/kodekloudrepos
```

---

### 🔹 Step 3: Verify Directory Contents

```bash
ls
```

👉 Ensure directory is empty before cloning

---

### 🔹 Step 4: Clone the Repository

```bash
git clone /opt/official.git
```

---

## 🧪 Output

```bash
Cloning into 'official'...
warning: You appear to have cloned an empty repository.
done.
```

---

### 🔹 Step 5: Verify Clone

```bash
ls
```

Expected output:

```bash
official
```

---

## ⚠️ Important Notes

* The repository is **empty**, so no files are visible after cloning
* No changes should be made to:

  * permissions
  * directory structure

---

## 💡 Key Concepts

| Concept         | Description                            |
| --------------- | -------------------------------------- |
| Bare Repository | Repository without working files       |
| git clone       | Creates a working copy of a repository |
| Local Clone     | Cloning from a path on the same server |

---

## 🧠 Learning Outcome

* Understood how to clone a **bare repository**
* Practiced working with **local Git paths**
* Learned to follow strict lab constraints (no modifications)

---

## 👨‍💻 Author

**Pankaj Sharma**
B.Tech CSE Student | DevOps Enthusiast

