# 🚀 Git Rebase Lab (Feature → Master without Merge Commit)

---

## 📌 Objective

Repository:

```bash
/usr/src/kodekloudrepos/games
```

👉 Task:

* Rebase **feature** branch onto **master**
* Do NOT create a merge commit
* Preserve feature changes
* Push updated history

---

## 🧠 Concept First (IMPORTANT)

👉 **Why rebase?**

| Merge                        | Rebase            |
| ---------------------------- | ----------------- |
| Creates extra merge commit ❌ | Clean history ✅   |
| Non-linear history ❌         | Linear history ✅  |
| Easy but messy               | Clean but careful |

👉 Here requirement = **NO merge commit → use REBASE**

---

## 🖥️ Steps

---

### 🔹 1. SSH into server

```bash
ssh natasha@ststor01
```

---

### 🔹 2. Go to repo

```bash
cd /usr/src/kodekloudrepos/games
```

---

### 🔹 3. Fix permission issue (IMPORTANT)

```bash
sudo git config --global --add safe.directory /usr/src/kodekloudrepos/games
```

---

### 🔹 4. Verify branches

```bash
git branch
```

👉 Output:

```
* feature
  master
```

---

### 🔹 5. Rebase feature onto master

```bash
sudo git rebase master
```

---

## 🧠 What happens here?

👉 Internally:

1. Git takes feature commits
2. Moves them on top of master
3. Creates clean linear history

---

### 🔹 6. Verify history

```bash
git log --oneline
```

👉 You should see:

```
initial commit
(master commits)
feature commits (on top)
```

---

### 🔹 7. Push changes

```bash
sudo git push origin feature --force
```

---

## ⚠️ Important Notes

* Use **--force** because history changed (rebase rewrites commits)
* Do NOT use normal push → it will fail
* Safe in this lab because controlled environment

---

## 🧠 Rebase vs Merge Visualization

### ❌ Merge:

```
A---B---C (master)
     \ 
      D---E (feature)
          \
           M (merge commit)
```

### ✅ Rebase:

```
A---B---C---D'---E' (feature)
```

---

## ✅ Final Result

✔ Feature branch rebased on master
✔ No merge commit created
✔ Clean linear history
✔ Changes pushed successfully

---

## ⚡ Quick Commands

```bash
cd /usr/src/kodekloudrepos/games
sudo git config --global --add safe.directory /usr/src/kodekloudrepos/games
git branch
sudo git rebase master
sudo git push origin feature --force
```

---

🔥 Task Completed Successfully
