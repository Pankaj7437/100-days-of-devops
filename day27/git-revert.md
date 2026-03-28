# 📘 Git Revert Latest Commit (KodeKloud Lab)

## 🧾 Task Summary

* Revert latest commit (**HEAD**) to previous commit
* Use commit message: **revert beta**
* Maintain commit history (no reset)
* Push changes to remote repository

---

## ⚙️ Steps Performed

### 1️⃣ Login to Storage Server

```bash
ssh natasha@ststor01
```

---

### 2️⃣ Navigate to Repository

```bash
cd /usr/src/kodekloudrepos/beta
```

---

### 3️⃣ Fix Safe Directory Issue (if occurs)

```bash
git config --global --add safe.directory /usr/src/kodekloudrepos/beta
```

---

### 4️⃣ Check Commit History (optional)

```bash
git log --oneline
```

---

### 5️⃣ Revert Latest Commit

```bash
sudo git revert HEAD
```

👉 When editor opens, update message:

```
revert beta
```

👉 Save and exit:

```
:wq
```

---

### 6️⃣ Push Changes to Remote

```bash
sudo git push origin master
```

---

## 🚨 Common Issues

### ❌ Permission Denied (`index.lock`)

✔️ Solution:

```bash
sudo git revert HEAD
```

---

### ❌ Dubious Ownership Error

✔️ Solution:

```bash
git config --global --add safe.directory /usr/src/kodekloudrepos/beta
```

---

## ✅ Verification

```bash
git log --oneline
```

Expected:

* New commit with message **revert beta**
* Previous commit still present

---

## 🎯 Result

* Latest commit reverted safely ✅
* History preserved ✅
* Changes pushed to remote ✅

---

## ⚡ Key Concept

| Command      | Behavior             |
| ------------ | -------------------- |
| `git reset`  | Deletes history ❌    |
| `git revert` | Creates new commit ✅ |

---

## 👨‍💻 Author

Pankaj Sharma
