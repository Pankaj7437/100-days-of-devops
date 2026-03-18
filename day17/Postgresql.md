# PostgreSQL Lab – Create User and Database with Permissions

## Objective

The Nautilus application requires a PostgreSQL database setup.  
The PostgreSQL server is already installed on the Nautilus database server.

Tasks to perform:

- Create a database user
- Create a database
- Grant full access to the user on the database

---

# Environment Details

| Parameter | Value |
|---|---|
| Infrastructure | Nautilus |
| Datacenter | Stratos |
| Database | PostgreSQL |
| Server | Nautilus DB Server |

---

# Step 1 – Connect to Database Server

```bash
ssh peter@stdb01
```

---

# Step 2 – Login to PostgreSQL

```bash
sudo -i
psql
```

---

# Step 3 – Create Database User

```sql
CREATE USER kodekloud_aim WITH PASSWORD 'GyQkFRVNr3';
```

Expected Output:

```
CREATE ROLE
```

---

# Step 4 – Create Database

```sql
CREATE DATABASE kodekloud_db6;
```

Expected Output:

```
CREATE DATABASE
```

---

# Step 5 – Grant Permissions

```sql
GRANT ALL PRIVILEGES ON DATABASE kodekloud_db6 TO kodekloud_aim;
```

Expected Output:

```
GRANT
```

---

# Step 6 – Verify Database

```sql
\l
```

---

# Important Note

- Do NOT restart PostgreSQL service (as per requirement)

---

# Commands Cheat Sheet

```bash
psql

CREATE USER kodekloud_aim WITH PASSWORD 'GyQkFRVNr3';

CREATE DATABASE kodekloud_db6;

GRANT ALL PRIVILEGES ON DATABASE kodekloud_db6 TO kodekloud_aim;

\l
```

---

# Common Mistakes

| Mistake | Issue |
|---|---|
| Using `SHOW DATABASES` | MySQL command, not PostgreSQL |
| Missing semicolon `;` | Query won't execute |
| Forgetting GRANT | User can't access DB |
| Restarting service | Lab may fail |

---

# Key Learning

- PostgreSQL user creation
- Database creation
- Permission management
- Difference between MySQL and PostgreSQL commands

---

# Conclusion

Successfully created a PostgreSQL user **kodekloud_aim**, database **kodekloud_db6**, and granted full privileges to the user without restarting the service.
