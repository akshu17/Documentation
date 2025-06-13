## 📂 Kubernetes Namespaces

### 🔑 What is a Namespace?

A **namespace** is a virtual cluster inside a Kubernetes cluster, used to organize and isolate resources.

---

### 📌 Types of Default Namespaces with Examples

| Namespace         | Purpose                                                                  | Example                                                                                           |
| ----------------- | ------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------- |
| `default`         | Where your objects go if you don’t specify a namespace.                  | If you run `kubectl run nginx --image=nginx`, the pod will be created in the `default` namespace. |
| `kube-system`     | Contains system-managed pods like DNS, network plugins, and controllers. | `kube-dns` runs here to resolve service names.                                                    |
| `kube-public`     | Readable by all users; mostly for public info.                           | Cluster info config may be here, accessible without auth.                                         |
| `kube-node-lease` | Stores node heartbeat leases for quicker node status updates.            | Each node has a `Lease` object to track heartbeat in this namespace.                              |

---

### ✅ Summary

Namespaces group resources logically and help manage cluster organization and security.

---

### ⚡ Commands

`kubectl get namespaces` — List all namespaces

`kubectl get pods -n kube-system` — See system pods

`kubectl create ns dev` — Create a custom namespace `dev`

---
