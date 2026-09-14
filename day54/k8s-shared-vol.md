# Nautilus DevOps: Kubernetes Multi-Container Shared Volume

## Problem Statement
The Nautilus DevOps team is developing a deployment template for applications that run across multiple containers within a single pod. These containers require a shared temporary storage space to exchange and persist transient data during their lifecycle.

## Objective
Deploy a multi-container pod (`volume-share-devops`) utilizing an `emptyDir` volume to share data between two `fedora:latest` containers mounted at different paths. 

## Lab Specifications
*   **Pod Name:** `volume-share-devops`
*   **Volume:** `volume-share` (Type: `emptyDir`)
*   **Container 1:** 
    *   **Name:** `volume-container-devops-1`
    *   **Image:** `fedora:latest`
    *   **Mount Path:** `/tmp/ecommerce`
*   **Container 2:** 
    *   **Name:** `volume-container-devops-2`
    *   **Image:** `fedora:latest`
    *   **Mount Path:** `/tmp/games`

---

## Deployment Guide

### 1. Create the Pod Configuration
Create a manifest file named `volume-pod.yaml` on the `jump-host` terminal to define the pod, containers, and volume mounts:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: volume-share-devops
spec:
  volumes:
  - name: volume-share
    emptyDir: {}
  containers:
  - name: volume-container-devops-1
    image: fedora:latest
    command: ["sleep", "3600"]
    volumeMounts:
    - name: volume-share
      mountPath: /tmp/ecommerce
  - name: volume-container-devops-2
    image: fedora:latest
    command: ["sleep", "3600"]
    volumeMounts:
    - name: volume-share
      mountPath: /tmp/games

```

### 2. Deploy the Pod

Apply the manifest to the Kubernetes cluster:

```bash
kubectl apply -f volume-pod.yaml

```

Wait for the pod to reach the `Running` state with both containers ready (`2/2`):

```bash
kubectl get pod volume-share-devops

```

### 3. Generate Test Data in Container 1

Execute a command in `volume-container-devops-1` to create a text file within its designated mount path (`/tmp/ecommerce`):

```bash
kubectl exec volume-share-devops -c volume-container-devops-1 -- sh -c "echo 'Welcome to xFusionCorp Industries' > /tmp/ecommerce/ecommerce.txt"

```

### 4. Verify Shared Volume in Container 2

Read the file from `volume-container-devops-2` using its respective mount path (`/tmp/games`) to confirm the `emptyDir` volume successfully bridged the two containers:

```bash
kubectl exec volume-share-devops -c volume-container-devops-2 -- cat /tmp/games/ecommerce.txt

```

**Expected Output:**

```
Welcome to xFusionCorp Industries

```
