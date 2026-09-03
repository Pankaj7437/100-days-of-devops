# Kubernetes HTTPD Deployment Lab

**Objective:** Create a Kubernetes deployment named `httpd` using the `httpd:latest` image on a pre-configured cluster.

**Environment:** The `kubectl` utility on the `jump-host` is already configured to communicate with the Kubernetes cluster.

## Solution Methods

You can complete this deployment task using either an imperative command or a declarative YAML manifest.

### Method 1: Imperative Command (Fastest)
This is the most efficient way to fulfill the lab requirements directly from the command line. Run the following command on the `jump-host`:

```bash
kubectl create deployment httpd --image=httpd:latest

```

### Method 2: Declarative YAML File

If you prefer Infrastructure as Code (IaC) principles, you can define the deployment using a manifest file. Kubernetes Deployments require the `selector` and `template` fields.

1. Create a YAML file (e.g., `httpd-deployment.yaml`):

```bash
vi httpd-deployment.yaml

```

2. Add the deployment configuration:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: httpd
spec:
  replicas: 1
  selector:
    matchLabels:
      app: httpd
  template:
    metadata:
      labels:
        app: httpd
    spec:
      containers:
      - name: httpd
        image: httpd:latest

```

3. Apply the configuration to the cluster:

```bash
kubectl apply -f httpd-deployment.yaml

```

## Verification

Ensure that your deployment was created and the pods are spinning up successfully:

```bash
# Verify the deployment exists and is ready
kubectl get deployments

# Verify the underlying pods are running
kubectl get pods

```
