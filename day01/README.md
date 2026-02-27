# Day 01 – Linux Basics: User Management

## 🔥 What I Learned Today
- How to create a user in Linux
- How to assign a non-interactive shell
- Basic verification commands

---

## 🧑‍💻 Commands Used

### ✔ Create a user with non-interactive shell
```bash
sudo useradd -s /usr/sbin/nologin javed
```

### ✔ Verify user
```bash
getent passwd javed
```

### ✔ Set password (optional)
```bash
sudo passwd javed
```

---

## 📘 Notes
- `/usr/sbin/nologin` prevents interactive login.
- This is useful for system service accounts.
- User is created without login shell but can still own files & run services.

---

## 🏁 Summary
Today I started my **100 Days of DevOps** journey by learning user management in Linux. I created a user with a restricted shell and practiced verification commands.

---
