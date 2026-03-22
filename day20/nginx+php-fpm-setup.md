# 🚀 Configure Nginx with PHP-FPM (PHP 8.2 via Unix Socket)

## 📌 Overview
This project demonstrates how to deploy a PHP-based web application using **Nginx and PHP-FPM** with **Unix socket communication**.  
The main challenge was installing the required **PHP version (8.2)**, since default repositories provide older versions.

---

## 🏗️ Architecture
- **Web Server:** Nginx  
- **Backend:** PHP-FPM  
- **Communication:** Unix Socket (`/var/run/php-fpm/default.sock`)  
- **Port:** 8096  
- **Document Root:** `/var/www/html`  

---

## ⚠️ Problem
Default repositories do not provide PHP 8.2, causing the application to fail.

---

## ✅ Solution
Use **Remi repository** to install the correct PHP version.

---

## 🧰 Implementation Steps

### 1. Install Required Repositories
```bash
sudo yum install -y epel-release
sudo yum install -y https://rpms.remirepo.net/enterprise/remi-release-9.rpm
````

### 2. Reset PHP Module

```bash
sudo dnf module reset php -y
```

### 3. Enable PHP 8.2

```bash
sudo dnf module enable php:remi-8.2 -y
```

### 4. Install PHP and Extensions

```bash
sudo dnf install -y php php-fpm php-cli php-mysqlnd php-gd php-xml php-mbstring
```

### 5. Verify PHP Version

```bash
php -v
```

Expected output:

```
PHP 8.2.x
```

---

## ⚙️ PHP-FPM Configuration

Edit configuration file:

```bash
sudo vi /etc/php-fpm.d/www.conf
```

Update the following:

```ini
listen = /var/run/php-fpm/default.sock
listen.owner = nginx
listen.group = nginx
listen.mode = 0660

user = nginx
group = nginx
```

Create socket directory:

```bash
sudo mkdir -p /var/run/php-fpm
```

Start PHP-FPM:

```bash
sudo systemctl enable php-fpm --now
```

---

## 🌐 Nginx Configuration

Edit configuration file:

```bash
sudo vi /etc/nginx/nginx.conf
```

Add/update server block:

```nginx
server {
    listen 8096;
    server_name _;
    root /var/www/html;
    index index.php index.html;

    location / {
        try_files $uri $uri/ =404;
    }

    location ~ \.php$ {
        root /var/www/html;
        fastcgi_pass unix:/var/run/php-fpm/default.sock;
        fastcgi_index index.php;
        include fastcgi_params;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    }
}
```

---

## 🔍 Validation

Check configuration:

```bash
sudo nginx -t
```

Restart Nginx:

```bash
sudo systemctl restart nginx
```

---

## 🧪 Testing

```bash
curl http://stapp01:8096/index.php
```

---

## 🐞 Troubleshooting

### Nginx not starting

```bash
nginx -t
```

* Check syntax errors
* Ensure semicolons (`;`) are present

### PHP not working

```bash
systemctl status php-fpm
ls /var/run/php-fpm/
```

### Wrong PHP version

```bash
dnf module list php
```

---

## ⚡ Key Learnings

* Managing package versions using repositories
* Nginx and PHP-FPM integration
* Unix socket vs TCP communication
* Debugging real-world server issues

---

## 🏁 Conclusion

Successfully configured a production-style PHP stack using Nginx and PHP-FPM with proper version control and optimized communication.

---

---

## 👨‍💻 Author

**Pankaj Sharma**  
DevOps Learner 🚀

---
