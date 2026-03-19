# MariaDB Setup Lab – Create Database, User and Grant Permissions

## Objective

Set up a MariaDB database server on Nautilus DB Server with the following requirements:

- Install and configure MariaDB
- Create a database
- Create a user with password
- Grant full privileges to the user on the database

---

# Environment Details

| Parameter | Value |
|---|---|
| Infrastructure | Nautilus |
| Datacenter | Stratos |
| Database | MariaDB |
| Server | Nautilus DB Server |

---

# Step 1 – Connect to DB Server

```bash
ssh peter@stdb01
```

---

# Step 2 – Install MariaDB (if not installed)

```bash
sudo yum install mariadb-server -y
```

---

# Step 3 – Start and Enable MariaDB

```bash
sudo systemctl start mariadb
sudo systemctl enable mariadb
```

---

# Step 4 – Login to MariaDB

```bash
mysql -u root -p
```

(Press Enter if no password)

---

# Step 5 – Create Database

```sql
CREATE DATABASE kodekloud_db5;
```

---

# Step 6 – Create User

```sql
CREATE USER 'kodekloud_cap'@'localhost' IDENTIFIED BY 'dCV3szSGNA';
```

---

# Step 7 – Grant Privileges

```sql
GRANT ALL PRIVILEGES ON kodekloud_db5.* TO 'kodekloud_cap'@'localhost';
```

---

# Step 8 – Apply Changes

```sql
FLUSH PRIVILEGES;
```

---

# Step 9 – Verify

```sql
SHOW DATABASES;
```

---

# Commands Cheat Sheet

```bash
mysql -u root -p

CREATE DATABASE kodekloud_db5;

CREATE USER 'kodekloud_cap'@'localhost' IDENTIFIED BY 'dCV3szSGNA';

GRANT ALL PRIVILEGES ON kodekloud_db5.* TO 'kodekloud_cap'@'localhost';

FLUSH PRIVILEGES;

SHOW DATABASES;
```

---

# Common Mistakes

| Mistake | Issue |
|---|---|
| Wrong DB name | Grant fails |
| Missing `.*` | Permissions not applied properly |
| Forgetting FLUSH | Changes not reflected immediately |
| Creating extra users | Not required |

---

# Key Learning

- MariaDB database setup
- User and password creation
- Privilege management
- Difference between MySQL/MariaDB and PostgreSQL syntax

---

# Conclusion

Successfully configured MariaDB by creating database **kodekloud_db5**, user **kodekloud_cap**, and granting full privileges to the user on the database.
