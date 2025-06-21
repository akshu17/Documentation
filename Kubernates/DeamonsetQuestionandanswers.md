## Kubernetes DaemonSet — Interview Questions & Answers

---

### ✅ Q1: What is a DaemonSet in Kubernetes?

A **DaemonSet** ensures that a copy of a specific Pod runs on all (or some) nodes in a cluster. When a new node is added, the DaemonSet automatically runs the Pod on that node.

**Common use cases:** log collection agents, monitoring agents, and node-level networking tools.

---

### ✅ Q2: How is DaemonSet different from Deployment?

| Aspect     | DaemonSet                         | Deployment                          |
| ---------- | --------------------------------- | ----------------------------------- |
| Purpose    | One Pod per node                  | Specified number of replicas        |
| Scheduling | Runs on each node automatically   | Scheduler chooses where to run Pods |
| Use Cases  | Node monitoring, logging, storage | Applications, APIs, services        |

---

### ✅ Q3: How does DaemonSet handle new nodes?

It automatically schedules the Pod on any new node that joins the cluster, ensuring coverage.

---

### ✅ Q4: Can you run a DaemonSet only on some nodes?

Yes. You can use **nodeSelector**, **node affinity**, or **taints and tolerations** to control where DaemonSet Pods run.

---

### ✅ Q5: How do you update a DaemonSet’s Pods?

DaemonSets support **rolling updates**:

* Use `updateStrategy: RollingUpdate`
* Update the Pod spec (like the container image)
* Kubernetes replaces Pods incrementally.

---

### ✅ Q6: What happens if a DaemonSet Pod is manually deleted?

The DaemonSet controller immediately recreates the Pod to maintain the desired state (one Pod per node).

---

### ✅ Q7: Can multiple DaemonSets run on the same nodes?

Yes. You can have multiple DaemonSets, each deploying different Pods to the same nodes.

---

### ✅ Q8: How do you delete a DaemonSet and its Pods?

```bash
kubectl delete daemonset <name>
```

Deleting the DaemonSet removes its Pods by default.

---

### ✅ Q9: How can you see where a DaemonSet’s Pods are running?

```bash
kubectl get pods -o wide
```

This shows each Pod’s node. Or use:

```bash
kubectl describe daemonset <name>
```

---

### ✅ Q10: Provide an example YAML for a DaemonSet

```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: my-daemonset
spec:
  selector:
    matchLabels:
      app: my-daemon
  template:
    metadata:
      labels:
        app: my-daemon
    spec:
      containers:
      - name: daemon-container
        image: busybox
        command: [ "sleep", "3600" ]
```

---

## ✅ Key Takeaway

**DaemonSet = one Pod per node, automatically maintained, great for node-level tasks.**
