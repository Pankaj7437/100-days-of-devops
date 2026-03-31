# 🚀 Git History Reset Lab (Clean README)

---

## 📌 Objective

Repository path:

```
/usr/src/kodekloudrepos/official
```

👉 Task:

* Keep only **2 commits** in history:

  * `initial commit`
  * `add data.txt file`
* Remove all extra commits
* Push updated history to remote

---

## 🖥️ Steps

### 1. SSH into server

```bash
ssh natasha@ststor01
```

---

### 2. Navigate to repository

```bash
cd /usr/src/kodekloudrepos/official
```

---

### 3. Fix permission issue (if any)

```bash
sudo git config --global --add safe.directory /usr/src/kodekloudrepos/official
```

---

### 4. Check commit history

```bash
git log --oneline
```

👉 Identify commit with message:

```
add data.txt file
```

---

### 5. Reset to that commit

```bash
sudo git reset --hard <commit-id>
```

---

### 6. Verify history

```bash
git log --oneline
```

👉 Expected:

```
add data.txt file
initial commit
```

---

### 7. Push changes (force)

```bash
sudo git push origin master --force
```

---

## 🧠 Key Concepts

* `git reset --hard` → removes commits + changes
* `--force push` → updates remote history
* Used when cleaning commit history

---

## ⚠️ Notes

* Do NOT use `git revert`
* Always use correct commit ID
* Force push is required after reset

---

## ✅ Final Result

✔ Only 2 commits remain
✔ Repository cleaned
✔ Changes pushed to remote

---

🔥 Task Completed
