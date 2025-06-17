## ✅ Kubernetes DaemonSet — Cheat Sheet

### 📌 **What is a DaemonSet?**

* A **DaemonSet** ensures **a copy of a specific Pod runs on every Node** in the cluster.
* When you add a new Node, the DaemonSet automatically runs the Pod on it.
* When you remove a Node, the Pod is automatically deleted.

---

### 📌 **Common Use Cases for DaemonSets**

| Use Case              | Why Use DaemonSet?                                                         |
| --------------------- | -------------------------------------------------------------------------- |
| **Log Collection**    | Deploy log collectors like Fluentd, Filebeat on every Node.                |
| **Monitoring**        | Install monitoring agents (e.g., Prometheus Node Exporter, Datadog Agent). |
| **Networking**        | Run network plugins (e.g., Calico, Flannel) on each Node.                  |
| **Storage**           | Deploy storage daemons like GlusterFS or Ceph.                             |
| **Security**          | Run security or compliance agents (e.g., Falco).                           |
| **Custom Node Tasks** | Run custom scripts or Node setup helpers on every Node.                    |

---

### 📌 **Basic DaemonSet YAML Example**

```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: fluentd
  namespace: kube-system
spec:
  selector:
    matchLabels:
      name: fluentd
  template:
    metadata:
      labels:
        name: fluentd
    spec:
      containers:
      - name: fluentd
        image: fluent/fluentd:v1.11
```

✅ **Meaning:**

* Deploy **one Fluentd Pod per Node** to collect logs.

---

### 📌 **How to Create and Verify**

**1️⃣ Save the YAML:**
`fluentd-daemonset.yaml`

**2️⃣ Apply it:**

```bash
kubectl apply -f fluentd-daemonset.yaml
```

**3️⃣ Check DaemonSets:**

```bash
kubectl get daemonsets -n kube-system
```

**4️⃣ Check Pods:**

```bash
kubectl get pods -o wide -n kube-system
```

---

### 📌 **Key Properties of DaemonSets**

* Runs **one Pod per Node** (can be limited to specific Node labels).
* Adding/removing Nodes automatically adjusts Pods.
* Ideal for **node-level operations** — unlike Deployments, which manage a set number of Pods.

---

## ✅ **Key Takeaway**

> **Use DaemonSets for log collection, monitoring, networking, security, and other tasks that must run on *every* Node.**

🚀✨
