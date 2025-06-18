# Kubernetes Deployment YAML Example & Command Guide

## ✅ Example Deployment YAML

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-deployment
  labels:
    app: my-app
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
      - name: nginx-container
        image: nginx:latest
        ports:
        - containerPort: 80
```

---

## 📌 YAML Sections Explained

| Section                  | Purpose                                      |
| ------------------------ | -------------------------------------------- |
| `apiVersion: apps/v1`    | API group/version for Deployment resource    |
| `kind: Deployment`       | Specifies this is a Deployment object        |
| `metadata`               | Metadata: name and labels for the Deployment |
| `spec`                   | Desired state of the Deployment              |
| `replicas`               | Number of Pods to run                        |
| `selector`               | How Deployment selects Pods to manage        |
| `template`               | Pod template: describes what Pods look like  |
| `spec` (inside template) | Defines containers in the Pod                |
| `containers`             | List of containers (one or more)             |
| `image`                  | Container image to run                       |
| `ports`                  | Ports exposed by the container               |

---

## ✅ Common `kubectl` Commands

| Command                                               | Description                          |
| ----------------------------------------------------- | ------------------------------------ |
| `kubectl apply -f deployment.yaml`                    | Create or update the Deployment      |
| `kubectl get deployments`                             | List all Deployments                 |
| `kubectl get pods`                                    | List all Pods created by Deployments |
| `kubectl describe deployment my-deployment`           | Detailed Deployment info             |
| `kubectl scale deployment my-deployment --replicas=5` | Scale to 5 Pods                      |
| `kubectl delete -f deployment.yaml`                   | Delete the Deployment                |
| `kubectl rollout status deployment my-deployment`     | Check rollout progress               |
| `kubectl rollout history deployment my-deployment`    | View Deployment history              |
| `kubectl rollout undo deployment my-deployment`       | Roll back to previous version        |

---

## ✅ Workflow Example

1️⃣ Write the YAML file (`deployment.yaml`)

2️⃣ Apply it:

```bash
kubectl apply -f deployment.yaml
```

3️⃣ Verify Pods:

```bash
kubectl get pods -o wide
```

4️⃣ Scale up/down:

```bash
kubectl scale deployment my-deployment --replicas=5
```

5️⃣ Update image:

* Edit `deployment.yaml`
* Run:

```bash
kubectl apply -f deployment.yaml
```

6️⃣ Roll back if needed:

```bash
kubectl rollout undo deployment my-deployment
```

7️⃣ Delete:

```bash
kubectl delete -f deployment.yaml
```

---

✅ **Tip:**

* `selector` must match `template.metadata.labels` exactly.
* Always check YAML indentations.

---

**Happy Deploying! 🚀**
