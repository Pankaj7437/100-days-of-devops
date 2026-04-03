# 🚀 Git Push Issue + Fix Typo (KodeKloud Lab)

---

## 📌 Objective

👉 Server: **ststor01 (storage server)**
👉 User: `max`
👉 Repo: `/home/max/story-blog`

### Tasks:

1. Fix typo in file → `lion-and-mouse.txt`
2. Push changes to remote repository
3. Ensure all 4 story titles exist in `story-index.txt`

---

## 🧠 Problem Understanding

* Repo already has changes → **ahead by 1 commit**
* Push is failing (common lab issue)
* There is a typo:

  ```
  ❌ Moose → ✅ Mouse
  ```

---

## 🖥️ Step-by-Step Solution

---

### 🔹 1. SSH into server

```bash
ssh max@ststor01
```

Password:

```
Max_pass123
```

---

### 🔹 2. Go to repository

```bash
cd /home/max/story-blog
```

---

### 🔹 3. Verify files

```bash
ls
```

Expected:

```
fox-and-grapes.txt
frogs-and-ox.txt
lion-and-mouse.txt
story-index.txt
```

---

### 🔹 4. Fix Typo

Open file:

```bash
vi lion-and-mouse.txt
```

👉 Find:

```
Moose
```

👉 Replace with:

```
Mouse
```

Save:

```
:wq
```

---

### 🔹 5. Verify story-index.txt

```bash
cat story-index.txt
```

👉 Must contain all 4 titles:

* Fox and Grapes
* Frogs and Ox
* Lion and Mouse
* (Any 4th story)

👉 If missing → edit:

```bash
vi story-index.txt
```

---

### 🔹 6. Add changes

```bash
git add .
```

---

### 🔹 7. Commit

```bash
git commit -m "fix typo in lion and mouse story"
```

---

### 🔹 8. Push changes

```bash
git push origin master
```

---

## ⚠️ If Push Fails (Important)

👉 If you get error like:

```
permission denied / rejected
```

Run:

```bash
git pull --rebase origin master
git push origin master
```

---

## 🧠 Why this happens?

| Issue         | Reason         |
| ------------- | -------------- |
| Push rejected | Remote updated |
| Fix           | Pull + rebase  |
| Result        | Clean history  |

---

## ✅ Final Verification

```bash
git status
```

✔ Should show:

```
nothing to commit, working tree clean
```

```bash
git log --oneline
```

✔ Latest commit should include your fix

---

## ⚡ Quick Commands

```bash
cd /home/max/story-blog
vi lion-and-mouse.txt
git add .
git commit -m "fix typo"
git push origin master
```

---

## 🎯 Final Result

✔ Typo fixed (Moose → Mouse)
✔ All stories present
✔ Changes committed
✔ Successfully pushed to remote

---

🔥 Task Completed Successfully
