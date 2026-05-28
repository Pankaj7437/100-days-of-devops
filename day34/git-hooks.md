# 🚀 Git Hook + Merge + Auto Release Tag (KodeKloud Lab)

---

# 📌 Objective

Repository:

```bash
/opt/official.git
```

Cloned Repository:

```bash
/usr/src/kodekloudrepos/official
```

### Tasks:

* Merge `feature` branch into `master`
* Create a `post-update` hook
* Automatically create release tag:

```bash
release-YYYY-MM-DD
```

* Test the hook
* Push all changes

---

# 🧠 Concepts Used

| Concept          | Explanation                    |
| ---------------- | ------------------------------ |
| Git Branch       | Separate development workflow  |
| Merge            | Combine branch changes         |
| Git Hook         | Script triggered automatically |
| post-update Hook | Runs after repository updates  |
| Git Tag          | Named snapshot/version         |

---

# 🖥️ Step-by-Step Commands

---

# 🔹 1. SSH into storage server

```bash
ssh natasha@ststor01
```

---

# 🔹 2. Move to repository directory

```bash
cd /usr/src/kodekloudrepos
```

---

# 🔹 3. Open repository

```bash
cd official
```

---

# 🔹 4. Check files

```bash
ls
```

Expected:

```bash
feature.txt
info.txt
```

---

# 🔹 5. Fix safe directory issue (if shown)

```bash
git config --global --add safe.directory /usr/src/kodekloudrepos/official
```

---

# 🌿 Merge Branches

---

# 🔹 6. Check branches

```bash
git branch
```

Expected:

```bash
feature
master
```

---

# 🔹 7. Switch to master branch

```bash
git checkout master
```

---

# 🔹 8. Merge feature branch

```bash
git merge feature
```

---

# 🧠 Merge Explanation

| Command             | Purpose                   |
| ------------------- | ------------------------- |
| git checkout master | Switch to master branch   |
| git merge feature   | Merge feature into master |

---

# 🔥 Create post-update Hook

---

# 🔹 9. Go to hooks directory

```bash
cd .git/hooks
```

---

# 🔹 10. Create hook file

```bash
vi post-update
```

---

# 🔹 11. Add below script

```bash
#!/bin/bash

DATE=$(date +%F)
TAG="release-$DATE"

git tag $TAG
```

---

# 🧠 Script Explanation

---

## 🔹 Shebang

```bash
#!/bin/bash
```

Executes script using Bash shell.

---

## 🔹 Get Current Date

```bash
DATE=$(date +%F)
```

### Example:

```bash
2026-04-04
```

`%F` means:

```bash
YYYY-MM-DD
```

---

## 🔹 Create Tag Variable

```bash
TAG="release-$DATE"
```

Example:

```bash
release-2026-04-04
```

---

## 🔹 Create Git Tag

```bash
git tag $TAG
```

Creates release tag automatically.

---

# 🔹 12. Make hook executable

```bash
chmod +x post-update
```

Without executable permission hook will not run.

---

# 🧪 Test Hook

---

# 🔹 13. Run hook manually

```bash
./post-update
```

---

# 🔹 14. Verify tag

```bash
git tag
```

Expected:

```bash
release-2026-04-04
```

---

# 🚀 Push Changes

---

# 🔹 15. Push master branch

```bash
git push origin master
```

---

# 🔹 16. Push tags

```bash
git push origin --tags
```

---

# 🔍 Verification

---

## 🔹 Check git history

```bash
git log --oneline
```

---

## 🔹 Check release tags

```bash
git tag
```

---

# ⚠️ Important Notes

| Important Point             | Reason                        |
| --------------------------- | ----------------------------- |
| Hook must be executable     | Otherwise it won’t run        |
| Push tags separately        | Tags don’t push automatically |
| Correct tag format required | Lab validation depends on it  |

---

# 📌 Hook Workflow

```text
Merge/Push
    ↓
post-update hook executes
    ↓
Current date fetched
    ↓
Release tag created
    ↓
Tag stored in repository
```

---

# ⚡ Quick Commands

```bash
ssh natasha@ststor01

cd /usr/src/kodekloudrepos/official

git config --global --add safe.directory /usr/src/kodekloudrepos/official

git checkout master

git merge feature

cd .git/hooks

vi post-update

chmod +x post-update

./post-update

git push origin master

git push origin --tags
```

---

# ✅ Final Result

✔ Feature branch merged into master
✔ post-update hook created
✔ Automatic release tag generated
✔ Correct tag naming format
✔ All changes pushed successfully

🔥 Task Completed Successfully
