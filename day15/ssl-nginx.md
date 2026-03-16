# Nginx SSL Configuration Lab – Deploy Secure Web Server on App Server 3

## Objective
The system administrators at xFusionCorp Industries need to prepare **App Server 3** for deployment of a new application.

The server must be configured with:

- **Nginx web server**
- **Self-signed SSL certificate**
- **HTTPS configuration**
- A basic **index page**

Finally, the configuration must be tested using **curl from the jump host**.

---

# Environment Details

| Parameter | Value |
|----------|------|
| Infrastructure | Nautilus |
| Data Center | Stratos |
| Target Server | App Server 3 |
| Hostname | stapp03 |
| Web Server | Nginx |
| SSL Certificate | /tmp/nautilus.crt |
| SSL Key | /tmp/nautilus.key |
| Document Root | /usr/share/nginx/html |

---

# Step 1 – Connect to App Server 3

Login from the jump host.

```bash
ssh banner@stapp03
```

---

# Step 2 – Install Nginx

Install nginx package.

```bash
sudo yum install nginx -y
```

Explanation:

| Command | Purpose |
|-------|---------|
| yum install | Install packages |
| nginx | Nginx web server |
| -y | Automatic confirmation |

---

# Step 3 – Start and Enable Nginx

Start nginx service.

```bash
sudo systemctl start nginx
```

Enable nginx at boot.

```bash
sudo systemctl enable nginx
```

Verify service status:

```bash
sudo systemctl status nginx
```

Expected:

```
Active: active (running)
```

---

# Step 4 – Move SSL Certificate and Key

Create SSL directory.

```bash
sudo mkdir -p /etc/nginx/ssl
```

Move certificate and key.

```bash
sudo mv /tmp/nautilus.crt /etc/nginx/ssl/
sudo mv /tmp/nautilus.key /etc/nginx/ssl/
```

Explanation:

| File | Purpose |
|----|--------|
| nautilus.crt | SSL certificate |
| nautilus.key | Private key |

---

# Step 5 – Configure Nginx for HTTPS

Edit nginx configuration.

```bash
sudo vi /etc/nginx/nginx.conf
```

Add or modify server block:

```
server {
    listen 443 ssl;
    server_name stapp03;

    ssl_certificate /etc/nginx/ssl/nautilus.crt;
    ssl_certificate_key /etc/nginx/ssl/nautilus.key;

    location / {
        root /usr/share/nginx/html;
        index index.html;
    }
}
```

Explanation:

| Directive | Purpose |
|----------|--------|
| listen 443 ssl | Enable HTTPS |
| ssl_certificate | SSL certificate path |
| ssl_certificate_key | SSL key path |
| root | Document root |

---

# Step 6 – Create Web Page

Create index file.

```bash
echo "Welcome!" | sudo tee /usr/share/nginx/html/index.html
```

Verify file:

```bash
cat /usr/share/nginx/html/index.html
```

Expected output:

```
Welcome!
```

---

# Step 7 – Restart Nginx

Apply configuration changes.

```bash
sudo systemctl restart nginx
```

---

# Step 8 – Test from Jump Host

Exit the server.

```bash
exit
```

Run curl test from jump host.

```bash
curl -Ik https://stapp03
```

Expected response:

```
HTTP/1.1 200 OK
server: nginx
```

`-k` flag allows connection with self-signed certificate.

---

# Commands Cheat Sheet

```bash
ssh banner@stapp03

sudo yum install nginx -y

sudo systemctl start nginx
sudo systemctl enable nginx

sudo mkdir -p /etc/nginx/ssl

sudo mv /tmp/nautilus.crt /etc/nginx/ssl/
sudo mv /tmp/nautilus.key /etc/nginx/ssl/

sudo vi /etc/nginx/nginx.conf

echo "Welcome!" | sudo tee /usr/share/nginx/html/index.html

sudo systemctl restart nginx

curl -Ik https://stapp03
```

---

# Common Mistakes

| Mistake | Problem |
|-------|--------|
| Forgetting to move SSL files | Nginx cannot start HTTPS |
| Incorrect SSL path | Configuration error |
| Not restarting nginx | Changes not applied |
| Using http instead of https | SSL test fails |
| Not using `-k` in curl | Self-signed certificate error |

---

# Key Concepts Learned

- Installing nginx on Linux
- Configuring HTTPS in nginx
- Using self-signed SSL certificates
- Managing web server configuration
- Testing HTTPS using curl

---

# Conclusion

Nginx was successfully installed and configured on **App Server 3** with a **self-signed SSL certificate**. A basic web page displaying **"Welcome!"** was created under the nginx document root, and HTTPS connectivity was verified using the curl command from the jump host.
