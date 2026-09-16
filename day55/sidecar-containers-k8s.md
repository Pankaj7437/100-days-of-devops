# Nautilus DevOps: Kubernetes Native Sidecar Log Aggregation

## Problem Statement
The Nautilus DevOps team requires access to the last 24 hours of web server access and error logs to trace issues and bugs. However, these logs are not critical enough to warrant a persistent volume, and the primary Nginx container should remain focused solely on serving web pages. To adhere to the separation of concerns principle, a sidecar pattern must be implemented to ship the logs to an aggregation service without modifying the web server container.

## Objective
Deploy a multi-container pod (`webserver`) that utilizes an `emptyDir` shared volume to stream Nginx logs via a secondary sidecar container. The sidecar must be deployed using the modern Kubernetes Native Sidecar feature to satisfy both the pod lifecycle and automated grading requirements.

## Lab Specifications
*   **Pod Name:** `webserver`
*   **Shared Volume:** `shared-logs` (Type: `emptyDir`)
*   **Primary Container:** 
    *   **Name:** `nginx-container`
    *   **Image:** `nginx:latest`
    *   **Mount Path:** `/var/log/nginx`
*   **Sidecar (Init) Container:** 
    *   **Name:** `sidecar-container`
    *   **Image:** `ubuntu:latest`
    *   **Lifecycle Policy:** `restartPolicy: Always` (Native Sidecar)
    *   **Command:** `["sh", "-c", "while true; do cat /var/log/nginx/access.log /var/log/nginx/error.log; sleep 30; done"]`
    *   **Mount Path:** `/var/log/nginx`

---

## Deployment Guide

### 1. Create the Pod Configuration
On the `jump-host` terminal, create a manifest file named `webserver.yaml`. By defining the sidecar under `initContainers` and adding `restartPolicy: Always`, Kubernetes treats it as a background service that runs alongside the main container.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: webserver
spec:
  volumes:
  - name: shared-logs
    emptyDir: {}
  containers:
  - name: nginx-container
    image: nginx:latest
    volumeMounts:
    - name: shared-logs
      mountPath: /var/log/nginx
  initContainers:
  - name: sidecar-container
    image: ubuntu:latest
    restartPolicy: Always
    command: ["sh", "-c", "while true; do cat /var/log/nginx/access.log /var/log/nginx/error.log; sleep 30; done"]
    volumeMounts:
    - name: shared-logs
      mountPath: /var/log/nginx

```

### 2. Deploy the Pod

Apply the configuration to the Kubernetes cluster:

```bash
kubectl apply -f webserver.yaml

```

Check the status to ensure both containers start successfully and the pod reaches the `Running` state:

```bash
kubectl get pods webserver

```

### 3. Verify the Log Streaming

Manually generate an access log entry by sending a background request to the Nginx container:

```bash
kubectl exec webserver -c nginx-container -- curl -s http://localhost > /dev/null

```

Check the output of the sidecar container to confirm it is successfully reading the logs from the shared volume:

```bash
kubectl logs webserver -c sidecar-container

```

---

## Troubleshooting & Solutions

### Issue 1: Automated Grader Reports `'sidecar-container' doesn't exist`

* **Symptom:** The pod deploys successfully and reaches a `Running` state, but the lab platform marks the task as failed, stating the container or the `ubuntu:latest` image is missing.
* **Cause:** The automated grader script is hardcoded to look for `sidecar-container` strictly inside the `initContainers` array. If you deployed it as a standard sidecar under the `containers` array (the traditional K8s method), the grader cannot find it.
* **Solution:** Move the `sidecar-container` definition into the `initContainers` block in your YAML file.

### Issue 2: Pod is Stuck in `Init:0/1` Status

* **Symptom:** After moving the sidecar to `initContainers`, the pod never reaches the `Running` state. The Nginx container never starts.
* **Cause:** Standard init containers must run to completion (exit code 0) before Kubernetes will start the main containers. Because the sidecar runs an infinite `while true` loop, it never exits, trapping the pod in an endless initialization phase.
* **Solution:** Add `restartPolicy: Always` to the `sidecar-container` definition. This leverages the **Kubernetes Native Sidecar** feature (introduced in K8s v1.28). It instructs the cluster to start the init container, leave it running in the background, and immediately proceed to boot the main `nginx-container`.
