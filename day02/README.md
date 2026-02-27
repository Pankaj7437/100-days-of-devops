# Day 02 – Temporary User Creation with Expiry Date

## 🔥 What I Learned Today
- How to create a temporary user in Linux
- How to set an account expiry date
- How to verify expiry settings

---

## 🧑‍💻 Commands Used

### ✔ Create a user with an expiry date
```bash
sudo useradd -e 2024-03-10 tempuser
```
`-e` → expiry date in YYYY-MM-DD format.

### ✔ Set expiry using chage (alternative)
```bash
sudo chage -E 2024-03-10 tempuser
```

### ✔ Verify expiry date
```bash
sudo chage -l tempuser
```

---

## 📘 Notes
- After the expiry date, the user **cannot log in**.
- The account is not deleted; it is just disabled.
- Useful for interns, temporary service accounts, KodeKloud lab tasks.

---

## 🏁 Summary
Today I learned how to create temporary users with an expiry date and how to manage their validity using the `useradd` and `chage` commands.
