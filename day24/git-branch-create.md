# 🌿 Git Branch Creation (KodeKloud Lab)

## 📌 Overview

In this lab, a new Git branch was created from the master branch in an existing repository without making any code changes. This helps isolate new feature development.

---

## 🧠 Problem Statement

- Repository location: `/usr/src/kodekloudrepos/official`
- Create a new branch:
```

xfusioncorp_official

````
- Base branch: `master`
- Do NOT modify any code

---

## ⚠️ Issue Faced

While accessing the repository:

```bash
fatal: detected dubious ownership in repository
````

---

## 🛠️ Solution Steps

### 1️⃣ Add Safe Directory

```bash
git config --global --add safe.directory /usr/src/kodekloudrepos/official
```

---

### 2️⃣ Navigate to Repository

```bash
cd /usr/src/kodekloudrepos/official
```

---

### 3️⃣ Switch to Master Branch

```bash
sudo git checkout master
```

---

### 4️⃣ Create New Branch

```bash
sudo git checkout -b xfusioncorp_official
```

---

### 5️⃣ Verify Branch

```bash
git branch
```

Expected output:

```
  master
  kodekloud_official
* xfusioncorp_official
```

---

## ✅ Verification

* Branch successfully created from `master`
* No changes made to code
* Working tree remains clean

---

## 🎯 Key Learnings

* Git branch creation workflow
* Handling "dubious ownership" issue
* Using safe.directory in Git
* Importance of permission management

---

## ⚠️ Common Mistakes

* Creating branch from wrong base (not master)
* Modifying files (not allowed in this task)
* Ignoring permission issues
* Not verifying branch properly

---

## 💼 Resume Point

> Created and managed Git branches in a production-like environment while resolving permission and ownership issues.

---

## 👨‍💻 Author

**Pankaj Sharma**
