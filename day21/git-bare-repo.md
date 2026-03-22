# 🚀 Create a Bare Git Repository on Storage Server

## 📌 Overview
This task involves setting up a bare Git repository on a storage server for centralized version control. A bare repository is used as a remote repository for collaboration and does not contain a working directory.

## 🏗️ Objective
- Install Git on the storage server
- Create a bare repository at `/opt/official.git`

## 🧰 Implementation

### Step 1: Connect to Storage Server
```bash
ssh natasha@ststor01
````

### Step 2: Install Git

```bash
sudo yum install -y git
```

### Step 3: Create Bare Repository

```bash
sudo mkdir -p /opt/official.git
cd /opt/official.git
sudo git init --bare
```

## 🔍 Verification

```bash
ls -la /opt/official.git
```

Expected structure includes:

* HEAD
* config
* objects/
* refs/

## ⚠️ Important Notes

* Use `--bare` flag (mandatory)
* Path must be exactly `/opt/official.git`
* Do not create a normal repository

## ⚡ Key Concept

A bare repository:

* Has no working directory
* Acts as a central remote repository
* Stores only Git history

## 🏁 Conclusion

Successfully configured a central Git repository on the storage server for team collaboration.

## 👨‍💻 Author
Pankaj Sharma  
B.Tech CSE | DevOps
