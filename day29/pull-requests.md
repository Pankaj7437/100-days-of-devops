# 🚀 Git Pull Request Workflow (Gitea UI Lab)

## 📌 Objective

Implement a proper Git workflow using **Pull Requests (PR)** instead of pushing directly to the `master` branch:

* Create PR from feature branch
* Assign reviewer
* Approve PR
* Merge into `master`

---

## 🖥️ Environment Details

* Git Server: Gitea
* Repo location: Storage Server
* Feature branch: `story/fox-and-grapes`
* Target branch: `master`

---

## ⚙️ Step 1: Verify Repository (Optional - CLI)

```bash
ssh natasha@ststor01
cd ~
git log
```

✔ Confirms that Max has pushed changes to a separate branch

---

## 🌐 Step 2: Access Gitea UI

* Click on **Gitea UI** (top bar in lab)
* Opens web interface

---

## 🔐 Step 3: Login as Max

* Username: `max`
* Password: `Max_pass123`

---

## 📂 Step 4: Open Repository

* Navigate to Max's repository
* Go to **Pull Requests** tab

---

## 🔀 Step 5: Create Pull Request

Click **New Pull Request**

### Fill details:

* **Source branch:** `story/fox-and-grapes`

* **Target branch:** `master`

* **Title:**

```
Added fox-and-grapes story
```

Click **Create Pull Request**

---

## 👨‍💻 Step 6: Add Reviewer

* Open the created PR
* On right panel → **Reviewers**
* Add user: `tom`

---

## 🔄 Step 7: Login as Tom

* Logout from Max
* Login with:

  * Username: `tom`
  * Password: `Tom_pass123`

---

## ✅ Step 8: Review & Approve PR

* Open the PR
* Click **Approve**

---

## 🔀 Step 9: Merge Pull Request

* After approval, click **Merge**

---

## 🧪 Verification

* Check that changes from `story/fox-and-grapes` are now in `master`
* PR should show as **Merged**

---

## 🧠 Explanation of Workflow

### 🔹 Why not push directly to master?

* Master contains **final stable code**
* Direct push can break production

---

### 🔹 Pull Request (PR)

* Used to propose changes
* Allows discussion and review before merging

---

### 🔹 Reviewer

* Ensures code quality
* Approves or requests changes

---

### 🔹 Approval Process

* Mandatory in team environments
* Prevents unreviewed code merge

---

### 🔹 Merge

* Combines feature branch into master
* Happens only after approval

---

## 🔄 Workflow Summary

```
Feature Branch → Pull Request → Review → Approval → Merge → Master
```

---

## ⚠️ Important Notes

* Use correct branch names
* Add reviewer before approval
* Login with correct user roles
* Do not merge without approval

---

## ✅ Final Outcome

* PR created successfully
* Reviewer assigned and approved
* Changes merged into `master`
* Proper DevOps workflow followed

---

🔥 Lab Completed Successfully
