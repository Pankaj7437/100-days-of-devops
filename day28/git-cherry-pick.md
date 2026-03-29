# 📘 Git Cherry-Pick Commit from Feature to Master (KodeKloud Lab)

## 🧾 Task Summary

* Repository: `/opt/demo.git`
* Clone path: `/usr/src/kodekloudrepos/demo`
* Two branches: `master` and `feature`
* Task:

  * Pick **one specific commit** from `feature`
  * Commit message: **"Update info.txt"**
  * Apply it to **master branch**
  * Push changes

---

## ⚙️ Steps Performed

### 1️⃣ Login to Storage Server

```bash
ssh natasha@ststor01
```

---

### 2️⃣ Navigate to Repository

```bash
cd /usr/src/kodekloudrepos/demo
```

---

### 3️⃣ Fix Safe Directory Issue (if needed)

```bash
git config --global --add safe.directory /usr/src/kodekloudrepos/demo
```

---

### 4️⃣ Find Required Commit

```bash
git log --oneline
```

👉 Identify commit with message:

```
Update info.txt
```

Example:

```
49d6336 Update info.txt
```

---

### 5️⃣ Switch to Master Branch

```bash
sudo git checkout master
```

---

### 6️⃣ Cherry-Pick the Commit

```bash
sudo git cherry-pick 49d6336
```

👉 (Use your actual commit ID)

---

### 7️⃣ Push Changes

```bash
sudo git push origin master
```

---

## 🚨 Common Issues

### ❌ Permission Denied (index.lock)

✔️ Solution:

```bash
sudo git cherry-pick <commit-id>
```

---

### ❌ Dubious Ownership

✔️ Solution:

```bash
git config --global --add safe.directory /usr/src/kodekloudrepos/demo
```

---

## ✅ Verification

```bash
git log --oneline
```

Expected:

* `master` branch contains commit **Update info.txt**

---

## 🎯 Result

* Specific commit moved from `feature` → `master` ✅
* No full merge performed ✅
* Changes pushed to remote ✅

---

## ⚡ Key Concept

| Command           | Purpose              |
| ----------------- | -------------------- |
| `git merge`       | Merge full branch    |
| `git cherry-pick` | Pick specific commit |

---

## 👨‍💻 Author

Pankaj Sharma
