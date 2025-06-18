# 📌 Kubernetes Labels & Selectors Cheat Sheet

## ✅ What are Labels?

* Labels are key-value pairs attached to Kubernetes objects (Pods, Deployments, Services).
* Used for identifying, grouping, and selecting resources.

**Example:**

```yaml
labels:
  app: my-app
  environment: production
```

## ✅ What is a Selector?

* Selectors match labels to filter objects.
* Two types:

  * **Equality-based:** e.g., `app=my-app`
  * **Set-based:** e.g., `in`, `notin`, `exists`

---

## 🎯 Common Commands

### 1️⃣ Label a single Pod

```bash
kubectl label pod <pod-name> key=value
```

Example:

```bash
kubectl label pod my-pod environment=production
```

### 2️⃣ Label all Pods matching a selector

```bash
kubectl label pods -l app=my-app environment=production
```

### 3️⃣ Label a Deployment

```bash
kubectl label deployment my-deployment key=value
```

### 4️⃣ View labels for all Pods

```bash
kubectl get pods --show-labels
```

### 5️⃣ Describe a Pod to see full labels

```bash
kubectl describe pod <pod-name>
```

### 6️⃣ Use selector to list Pods

```bash
kubectl get pods -l environment=production
```

### 7️⃣ Use selector to delete Pods

```bash
kubectl delete pod -l environment=production
```

---

## ✅ Example Deployment with Labels & Selector

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

✅ Here:

* **Deployment label:** `app: my-app`
* **Pod template label:** `app: my-app`
* **Selector:** `matchLabels: app: my-app`

This ensures the Deployment manages Pods with that label.

---

## 🔑 Best Practices

* Always label your resources for easy management.
* Use consistent keys like `app`, `env`, `tier`.
* Use selectors for rolling updates, scaling, and clean deletes.

---

🚀 **Commands & YAML in one place — happy deploying!**
