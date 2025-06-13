## 📌 `kubectl get api-resources`

### ✅ **What it does**

The command:

```bash
kubectl get api-resources
```

lists **all resource types (API resources)** that your Kubernetes cluster knows about and can manage.

---

### 📂 **Details shown:**

| Column         | Description                                                           |
| -------------- | --------------------------------------------------------------------- |
| **NAME**       | Resource type name (e.g., `pods`, `services`, `deployments`)          |
| **SHORTNAMES** | Short alias for the resource (e.g., `po` for `pods`)                  |
| **APIGROUP**   | API group the resource belongs to (e.g., `apps`, `batch`)             |
| **NAMESPACED** | `true` if resource exists within a namespace, `false` if cluster-wide |
| **KIND**       | The formal `kind` used in YAML specs (e.g., `Pod`, `Deployment`)      |

---

### ⚡ **Example output:**

```bash
NAME               SHORTNAMES   APIGROUP   NAMESPACED   KIND
pods               po                       true         Pod
services           svc                      true         Service
deployments        deploy       apps        true         Deployment
nodes              no                       false        Node
namespaces         ns                       false        Namespace
```

---

### 🔑 **Why use it?**

✅ See **all resource types** available in your cluster
✅ Check if a resource is **namespaced or cluster-scoped**
✅ Learn the correct `kind` and `apigroup` for writing YAML
✅ Discover **shortnames** for faster `kubectl` commands

---

This helps you write valid YAML files and understand what Kubernetes can manage in your cluster!
