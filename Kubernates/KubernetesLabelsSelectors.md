# 📌 Kubernetes Labels & Selectors Cheat Sheet

## ✅ What are Labels?

* Key-value pairs attached to objects (Pods, Nodes, Deployments, etc.)
* Used for identification, organization, and selection.

**Example:**

```yaml
metadata:
  labels:
    app: my-app
    tier: frontend
```

---

## ✅ What are Selectors?

* Expressions that filter objects by matching labels.
* Used by `kubectl` and controllers (like Deployments, Services).

**Example:**

```yaml
selector:
  matchLabels:
    app: my-app
```

---

## ✅ Common Commands

### 1️⃣ Add Label

```bash
kubectl label pod my-pod environment=production
```

### 2️⃣ View Labels

```bash
kubectl get pods --show-labels
```

### 3️⃣ Get by Label (Selector)

```bash
kubectl get pods -l app=my-app
kubectl get pods -l app=my-app,tier=frontend
```

### 4️⃣ Remove Label

```bash
kubectl label pod my-pod environment-
```

### 5️⃣ Label a Node

```bash
kubectl label node my-node disktype=ssd
```

### 6️⃣ Use Selector in Scheduling

```yaml
spec:
  nodeSelector:
    disktype: ssd
```

---

## ✅ Example Deployment YAML with Labels & Selector

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
      - name: nginx
        image: nginx
```

**Key Points:**

* `metadata.labels`: Label the Deployment object itself.
* `spec.selector.matchLabels`: Deployment selects Pods with matching labels.
* `template.metadata.labels`: Pods created by Deployment will have this label.

---

## ✅ Tips

* Use `kubectl get ... -o wide` to see Nodes and Labels.
* Use labels for organizing environments: `env=dev`, `env=prod`.
* Services use selectors to target Pods dynamically.

---

## 🏷️ Must-Know Flags

| Command              | Description           |
| -------------------- | --------------------- |
| `-l` or `--selector` | Filter by label(s)    |
| `--show-labels`      | Show labels in output |

---

✅ **Labels + Selectors = Powerful resource grouping and management!** 🚀
