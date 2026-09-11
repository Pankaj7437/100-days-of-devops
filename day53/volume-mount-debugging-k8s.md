# Nautilus DevOps: Kubernetes Nginx & PHP-FPM Troubleshooting

## Problem Statement
The Nginx and PHP-FPM setup on the Kubernetes cluster halted its functionality. The `nginx-phpfpm` pod and `nginx-config` ConfigMap were active, but the website was inaccessible. The root cause was identified as a volume mount mismatch: the Nginx configuration defined the document root as `/var/www/html`, but the `nginx-container` incorrectly mounted the shared volume to `/usr/share/nginx/html`.

## Objective
Identify the volume mount discrepancy, correct the pod configuration, recreate the pod, and deploy the `index.php` application file into the proper document root to restore website functionality.

## Lab Specifications
*   **Pod Name:** `nginx-phpfpm`
*   **Containers:** `php-fpm-container`, `nginx-container`
*   **ConfigMap:** `nginx-config`
*   **Correct Document Root:** `/var/www/html`
*   **Application File:** `/home/thor/index.php`

---

## Resolution Guide

### 1. Extract the Pod Configuration
Export the current configuration of the misconfigured pod into a YAML file for editing:
```bash
kubectl get pod nginx-phpfpm -o yaml > nginx-phpfpm.yaml

```

### 2. Correct the Volume Mount Path

Update the volume mount path for the `nginx-container` so it matches the PHP-FPM container and the Nginx configuration file. Replace `/usr/share/nginx/html` with `/var/www/html`:

```bash
sed -i 's#/usr/share/nginx/html#/var/www/html#g' nginx-phpfpm.yaml

```

### 3. Recreate the Pod

Apply the corrected YAML file. The `--force` flag cleanly deletes the broken pod and immediately recreates it with the fixed volume mount:

```bash
kubectl replace --force -f nginx-phpfpm.yaml

```

Wait for the pod to reach a ready state:

```bash
kubectl get pods

```

*(Wait until the `READY` column displays `2/2`)*

### 4. Deploy the Application File

Copy the `index.php` file from the jump-host directly into the newly corrected document root inside the Nginx container:

```bash
kubectl cp /home/thor/index.php nginx-phpfpm:/var/www/html/index.php -c nginx-container

```

### 5. Verification

Verify that the file was copied successfully and is present in the shared volume:

```bash
kubectl exec nginx-phpfpm -c nginx-container -- ls -l /var/www/html/index.php

```

Click the **Website** button on the top bar of the lab environment to confirm the Nginx server is correctly processing and serving the PHP file.

```

```
