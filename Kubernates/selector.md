## ✅ Kubernetes Selectors — Cheat Sheet

### 📌 **What is a Selector?**

* A **Selector** is a filter in Kubernetes.
* It selects a group of resources (Pods, etc.) **based on labels**.
* Used by Services, ReplicaSets, Deployments, etc.

---

### 📌 **Types of Selectors**

### 1️⃣ **Equality-based Selectors**

* Match resources with a **specific label key=value**.

```yaml
selector:
  matchLabels:
    app: nginx
    environment: production
```

✅ **Meaning:** Select resources where `app=nginx` AND `environment=production`.

### 2️⃣ **Set-based Selectors**

* Match resources where label keys’ values **are in or not in a list**.

```yaml
selector:
  matchExpressions:
    - key: environment
      operator: In
      values:
        - dev
        - staging
    - key: tier
      operator: NotIn
      values:
        - frontend
```

✅ **Meaning:** Select where `environment` is `dev` or `staging` AND `tier` is NOT `frontend`.

---

### 📌 **Where Selectors Are Used**

| Resource       | How it uses a Selector                    |
| -------------- | ----------------------------------------- |
| **Service**    | Selects Pods to forward traffic to        |
| **ReplicaSet** | Selects Pods to manage their count        |
| **Deployment** | Uses ReplicaSet’s selector to manage Pods |
| **kubectl**    | Filter resources on the CLI               |

---

### 📌 **Example: Selector in a Service**

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app: myapp
  ports:
    - port: 80
      targetPort: 8080
```

✅ **Meaning:** Route traffic to Pods with `app=myapp`.

---

### 📌 **Example: Selector in a ReplicaSet**

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: my-replicaset
spec:
  replicas: 3
  selector:
    matchLabels:
      app: myapp
  template:
    metadata:
      labels:
        app: myapp
    spec:
      containers:
        - name: myapp
          image: myapp:1.0
```

✅ **Meaning:** Ensure 3 Pods exist with `app=myapp`.

---

### 📌 **Selector in kubectl**

```bash
# List Pods with label app=myapp
kubectl get pods --selector app=myapp

# Shorthand
kubectl get pods -l app=myapp
```

✅ **Tip:** Works with any resource (Pods, Services, Deployments).

---

## ✅ **Key Takeaway**

> **Selectors group and filter resources using labels. They are fundamental for how Kubernetes connects, scales, and manages your apps!** 🚀✨
