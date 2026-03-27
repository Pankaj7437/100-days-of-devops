# 🔗 Git Remote Update & Push Lab (KodeKloud)

## 📌 Task Overview

* Add new remote:

  * Name: `dev_official`
  * URL: `/opt/xfusioncorp_official.git`
* Copy file `/tmp/index.html` into repo
* Commit changes on `master`
* Push to new remote

---

## 🛠️ Steps

### 🔹 Navigate to Repository

```bash
cd /usr/src/kodekloudrepos/official
```

---

### 🔹 Fix Ownership Issue

```bash
git config --global --add safe.directory /usr/src/kodekloudrepos/official
```

---

### 🔹 Add Remote

```bash
sudo git remote add dev_official /opt/xfusioncorp_official.git
```

---

### 🔹 Verify Remote

```bash
git remote -v
```

---

### 🔹 Copy File

```bash
sudo cp /tmp/index.html .
```

---

### 🔹 Add & Commit

```bash
sudo git add index.html
sudo git commit -m "Added index.html"
```

---

### 🔹 Push to New Remote

```bash
sudo git push dev_official master
```

---

## ⚠️ Common Mistakes

❌ Pushing to origin
✔ Correct:

```bash
git push dev_official master
```

---

❌ Permission denied
✔ Use:

```bash
sudo git <command>
```

---

## 📦 Final Outcome

✔ Remote `dev_official` added
✔ File committed
✔ Code pushed to new remote

---

## ✍️ Author

**Pankaj Sharma ** 🚀
DevOps Learner

---
