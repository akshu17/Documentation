# Kubernetes Rolling Update Guide

## 📌 What is a rolling update?

A rolling update gradually replaces old Pods with new ones, ensuring zero downtime. Kubernetes does this automatically for Deployments.

---

## ✅ How to perform it

### 1️⃣ Update your Deployment YAML

Example:

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
      - name: my-app
        image: my-app:2.0  # <-- update the image tag here
```

Apply the updated YAML:

```bash
kubectl apply -f deployment.yaml
```

---

### 2️⃣ Or update directly with `kubectl set image`

```bash
kubectl set image deployment/my-app my-app=my-app:2.0
```

---

### 3️⃣ Check the rollout status

```bash
kubectl rollout status deployment/my-app
```

---

### 4️⃣ Pause or resume a rollout (optional)

Pause:

```bash
kubectl rollout pause deployment/my-app
```

Resume:

```bash
kubectl rollout resume deployment/my-app
```

---

### 5️⃣ Undo a rollout if needed

```bash
kubectl rollout undo deployment/my-app
```

---

## ⚙️ How it works

- Kubernetes creates new Pods gradually.
- Old Pods are terminated **only when new Pods are running & healthy**.
- Control rollout details with `maxSurge` and `maxUnavailable`:

```yaml
strategy:
  type: RollingUpdate
  rollingUpdate:
    maxSurge: 1
    maxUnavailable: 1
```

---

**✅ Done!** Now you know how to perform a rolling update in Kubernetes.
