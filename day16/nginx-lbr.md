# Nginx Load Balancer Configuration on LBR Server

## Objective
Traffic on the website managed by the Nautilus production support team is increasing, causing performance degradation.  
To improve availability and distribute traffic efficiently, the team decided to configure **Nginx as a load balancer** on the **LBR server (stlb01)** in the Stratos Datacenter.

The load balancer will distribute incoming traffic across all application servers.

---

# Infrastructure Overview

| Component | Host |
|---|---|
| Load Balancer | stlb01 |
| Application Server 1 | stapp01 |
| Application Server 2 | stapp02 |
| Application Server 3 | stapp03 |
| Backend Service | Apache (httpd) |
| Apache Port | 8084 |

Architecture:

```
Client Request
      │
      ▼
   stlb01
   (Nginx)
      │
 ┌────┴────┐
 │         │
 ▼         ▼
stapp01   stapp02   stapp03
 Apache    Apache    Apache
 Port 8084 Port 8084 Port 8084
```

---

# Step 1: Connect to LBR Server

```bash
ssh loki@stlb01
```

---

# Step 2: Install Nginx

Install nginx if it is not already installed.

```bash
sudo yum install nginx -y
```

Start and enable nginx.

```bash
sudo systemctl start nginx
sudo systemctl enable nginx
```

---

# Step 3: Identify Backend Servers

Check the IP addresses of application servers from the jump host.

```bash
getent hosts stapp01 stapp02 stapp03
```

Example output:

```
10.244.195.31 stapp01
10.244.48.1   stapp02
10.244.195.41 stapp03
```

Apache service on these servers is already running on **port 8084**.

---

# Step 4: Configure Nginx Load Balancer

Edit the main nginx configuration file.

```bash
sudo vi /etc/nginx/nginx.conf
```

Inside the **http block**, add the following configuration.

```
upstream backend_servers {
    server 10.244.195.31:8084;
    server 10.244.48.1:8084;
    server 10.244.195.41:8084;
}

server {
    listen 80;
    listen [::]:80;

    server_name _;

    location / {
        proxy_pass http://backend_servers;
    }
}
```

Explanation:

| Directive | Purpose |
|---|---|
| upstream | Defines backend application servers |
| server | Backend servers with Apache service |
| listen 80 | Accept HTTP traffic |
| proxy_pass | Forward requests to backend servers |

---

# Step 5: Test Configuration

Validate nginx configuration.

```bash
sudo nginx -t
```

Expected output:

```
syntax is ok
test is successful
```

---

# Step 6: Restart Nginx

Apply configuration changes.

```bash
sudo systemctl restart nginx
```

Check service status.

```bash
sudo systemctl status nginx
```

---

# Step 7: Verify Apache on App Servers

Ensure Apache service is running on all application servers.

Example:

```bash
ssh tony@stapp01
sudo systemctl status httpd
```

Apache should be listening on port **8084**.

---

# Step 8: Test Load Balancer

From the jump host, test the load balancer.

```bash
curl http://stlb01:80
```

Expected output:

```
Welcome to xFusionCorp Industries!
```

---

# Commands Cheat Sheet

```bash
ssh loki@stlb01

sudo yum install nginx -y

sudo vi /etc/nginx/nginx.conf

sudo nginx -t

sudo systemctl restart nginx

curl http://stlb01:80
```

---

# Key Concepts Learned

- Nginx load balancing
- Reverse proxy configuration
- High availability architecture
- Traffic distribution across backend servers
- Service verification and testing

---

# Conclusion

Nginx was successfully configured as a **load balancer on the LBR server (stlb01)**. Incoming traffic is now distributed across all application servers running Apache on port **8084**, improving performance and scalability of the application.
