# Kubernetes Deployment YAML Manifest Cheat Sheet

## ✅ What is a Deployment?

A Deployment is a higher-level Kubernetes object that manages ReplicaSets and Pods. It ensures that a specified number of Pods are always running and up-to-date.

---

## 📄 Example Deployment YAML

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

## 🗂️ Explanation of Fields

| Field                           | Description                                                |
| ------------------------------- | ---------------------------------------------------------- |
| `apiVersion`                    | The API version to use (`apps/v1` for Deployment)          |
| `kind`                          | Resource type: `Deployment`                                |
| `metadata`                      | Name and labels for the Deployment                         |
| `spec.replicas`                 | Number of Pods to run                                      |
| `spec.selector`                 | Label selector to identify Pods managed by this Deployment |
| `spec.template`                 | Pod template: defines the labels and containers            |
| `spec.template.spec.containers` | List of containers, their images, and exposed ports        |

---

## ✅ How to Create and Apply

**1️⃣ Save the YAML:**
Create a file named `deployment.yaml` and paste the above YAML.

**2️⃣ Apply the Deployment:**

```bash
kubectl apply -f deployment.yaml
```

**3️⃣ Check status:**

```bash
kubectl get deployments
kubectl get pods
kubectl describe deployment my-deployment
```

---

## 🔄 Rolling Update

Kubernetes automatically does a rolling update if you change the Deployment (e.g., a new image version). It replaces old Pods with new ones gradually.

**Update the image:**

```bash
kubectl set image deployment/my-deployment nginx-container=nginx:1.21
```

**Check rollout status:**

```bash
kubectl rollout status deployment/my-deployment
```

**Roll back if needed:**

```bash
kubectl rollout undo deployment/my-deployment
```

---

## 📌 Tips

✅ Make sure `selector.matchLabels` matches `template.metadata.labels` exactly.
✅ Use `replicas: 2` or more for high availability.
✅ Use versioned container images (`nginx:1.21` instead of `latest`) for predictable deployments.

---

## 📚 Common Commands

| Command                                        | Purpose               |
| ---------------------------------------------- | --------------------- |
| `kubectl get deployments`                      | List deployments      |
| `kubectl get pods`                             | List Pods             |
| `kubectl describe deployment <name>`           | Show detailed info    |
| `kubectl delete deployment <name>`             | Delete the Deployment |
| `kubectl scale deployment <name> --replicas=5` | Scale up/down         |
| `kubectl rollout status deployment <name>`     | Check rollout         |
| `kubectl rollout undo deployment <name>`       | Roll back update      |

---

✅ **You now have a complete Deployment cheat sheet!**
