## 📂 Kubernetes Namespaces

### What is a Namespace?

A **namespace** in Kubernetes is a **logical partition** (virtual cluster) inside a **physical Kubernetes cluster**.
Namespaces help **organize and isolate** Kubernetes resources like Pods, Services, and Deployments.

---

### 🎯 Why use Namespaces?

✅ **Purpose:**

* Group resources by **team**, **project**, or **environment** (`dev`, `test`, `prod`).
* Apply **different permissions** for different teams.
* Limit **resource usage** (CPU, memory) per namespace.
* Avoid **name conflicts** — the same resource name can exist in different namespaces.

---

### 🏷️ Built-in Namespaces

| Namespace         | Purpose                                                  |
| ----------------- | -------------------------------------------------------- |
| `default`         | For user resources when no namespace is specified.       |
| `kube-system`     | For Kubernetes system resources (e.g., DNS, networking). |
| `kube-public`     | Publicly readable resources. Rarely used.                |
| `kube-node-lease` | Manages node heartbeats efficiently.                     |

---

### 🧩 Example YAML

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-app
  namespace: dev   # Pod is created in the 'dev' namespace
```

---

### ⚡ Useful Commands

| Task                            | Command                                      |
| ------------------------------- | -------------------------------------------- |
| List all namespaces             | `kubectl get namespaces` or `kubectl get ns` |
| List all pods in a namespace    | `kubectl get pods -n <namespace>`            |
| List all pods in all namespaces | `kubectl get pods --all-namespaces`          |
| Create a namespace              | `kubectl create namespace <name>`            |

---

### ✅ Summary

**Namespaces** help you **organize**, **secure**, and **manage** multiple groups of Kubernetes resources within a single cluster.
