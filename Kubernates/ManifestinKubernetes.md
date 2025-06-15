## 📜 What is a Manifest in Kubernetes?

In Kubernetes, a **manifest** is a **YAML (or JSON)** configuration file that defines the **desired state** of a Kubernetes resource. You describe what you want, and Kubernetes makes it happen.

---

### ✏️ Key Parts of a Manifest

| Field        | What it does                                      |
| ------------ | ------------------------------------------------- |
| `apiVersion` | Which version of the K8s API to use               |
| `kind`       | Type of resource (Pod, Deployment, Service, etc.) |
| `metadata`   | Name, labels, namespace, and annotations          |
| `spec`       | Detailed desired configuration                    |

---

### 📄 Example Manifest (Pod)

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
  labels:
    app: my-app
spec:
  containers:
  - name: nginx-container
    image: nginx:latest
    ports:
    - containerPort: 80
```

✅ **Explanation:**

* Creates a **Pod** named `my-pod`
* Runs an **nginx** container
* Exposes port **80** inside the container

---

### ⚡ How to Apply a Manifest

Use `kubectl apply` to create or update resources:

```bash
kubectl apply -f pod.yaml
```

---

### 📌 Benefits of Manifests

* **Declarative:** Describe the desired state, Kubernetes handles the rest.
* **Reusable:** Store in version control, share with teams.
* **Idempotent:** Running the same file multiple times won’t break things — Kubernetes ensures the actual state matches the desired state.

---

**In summary:** A manifest is your blueprint for Kubernetes resources!
