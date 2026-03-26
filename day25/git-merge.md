# 🚀 Git Branch, Commit, Merge & Push Lab (KodeKloud)

## 📌 Task Overview

The DevOps team is working on a project repository located at:

```
/usr/src/kodekloudrepos/games
```

### Requirements:

1. Create a new branch `datacenter` from `master`
2. Copy `/tmp/index.html` into the repo
3. Add and commit the file in the new branch
4. Merge the branch back into `master`
5. Push both branches to origin

---

## 🛠️ Step-by-Step Solution

### 🔹 Step 1: Navigate to Repository

```bash
cd /usr/src/kodekloudrepos/games
```

---

### 🔹 Step 2: Fix Permission Issue (Important)

```bash
git config --global --add safe.directory /usr/src/kodekloudrepos/games
```

---

### 🔹 Step 3: Switch to Master Branch

```bash
sudo git checkout master
```

---

### 🔹 Step 4: Create New Branch

```bash
sudo git checkout -b datacenter
```

---

### 🔹 Step 5: Copy File into Repo

```bash
sudo cp /tmp/index.html .
```

---

### 🔹 Step 6: Add and Commit Changes

```bash
sudo git add index.html
sudo git commit -m "Added index.html in datacenter branch"
```

---

### 🔹 Step 7: Switch Back to Master

```bash
sudo git checkout master
```

---

### 🔹 Step 8: Merge Branch into Master

```bash
sudo git merge datacenter
```

---

### 🔹 Step 9: Push Changes to Remote

```bash
sudo git push origin master
sudo git push origin datacenter
```

---

## ✅ Verification

```bash
git branch
git log --oneline
```

---

## ⚠️ Common Errors & Fixes

### ❌ Permission Denied (index.lock)

✔ Solution:

```bash
sudo git <command>
```

---

### ❌ Dubious Ownership Error

✔ Solution:

```bash
git config --global --add safe.directory /usr/src/kodekloudrepos/games
```

---

### ❌ Changes Not Reflected in Lab

✔ Reason:
👉 Push step missed

✔ Fix:

```bash
git push origin <branch>
```

---

## 🧠 Key Concepts

* **Branching** → Isolate new changes
* **Commit** → Save snapshot
* **Merge** → Combine branches
* **Push** → Upload to remote (MOST IMPORTANT)

---

## 📦 Final Outcome

✔ New branch `datacenter` created
✔ File added and committed
✔ Changes merged into `master`
✔ Both branches pushed successfully

---

## ✍️ Author

**Pankaj Sharma (Commander)** 🚀
B.Tech CSE | DevOps Learner

---
