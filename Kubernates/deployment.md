## What is a Deployment in Kubernetes

### ✅ Definition

A **Deployment** is a Kubernetes resource that provides **declarative updates** for Pods and ReplicaSets. It manages the desired state for application Pods — ensuring the correct number are running and updating them safely.

### ✅ Key Features

* Rolling updates
* Rollbacks to previous versions
* Scaling (manual or auto)
* Self-healing (replaces crashed Pods)

### ✅ How it works

1. You define a Deployment YAML specifying:

   * Container image
   * Number of replicas
   * Labels and selectors
2. Kubernetes creates a ReplicaSet.
3. ReplicaSet ensures the specified number of Pods are always running.

### ✅ Example YAML

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
spec:
  replicas: 3
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      containers:
      - name: my-container
        image: nginx:latest
```

### ✅ Use Cases

* Managing stateless applications
* Performing rolling updates with zero downtime
* Reverting failed changes

**Key Takeaway:** Deployments are the standard way to run and manage stateless applications in Kubernetes.
