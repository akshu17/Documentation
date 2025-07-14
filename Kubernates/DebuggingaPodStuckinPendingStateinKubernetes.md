# 🛠️ Debugging a Pod Stuck in Pending State in Kubernetes

When a pod is stuck in the `Pending` state, it usually means that Kubernetes can't schedule it on any node due to resource constraints or configuration issues.

---

## 🔍 Step-by-Step Debugging

### 1. ✅ Check Pod Status

```bash
kubectl get pods
```

### 2. 📖 Describe the Pod for Detailed Info

```bash
kubectl describe pod <pod-name>
```

Look for:

* **Events section**
* **Scheduler messages**

Common issues:

* No nodes match affinity/anti-affinity rules
* Insufficient CPU/Memory
* Taints on nodes without matching tolerations
* VolumeBinding issues

---

### 3. 📦 Check Node Resource Availability

```bash
kubectl describe nodes
```

OR

```bash
kubectl get nodes -o json | jq '.items[] | {name: .metadata.name, allocatable: .status.allocatable}'
```

Check if:

* Nodes have enough CPU/memory
* Disk pressure or memory pressure is reported

---

### 4. 🧭 Check for Node Selectors or Affinities

```bash
kubectl get pod <pod-name> -o json | jq '.spec.nodeSelector'
```

Also look at:

```bash
kubectl describe pod <pod-name>
```

---

### 5. 🧱 Check Persistent Volume Claims

If your pod uses volumes:

```bash
kubectl get pvc
```

Check PVC status. If in `Pending`, the volume may not be available or misconfigured.

---

### 6. ⛔ Check Taints on Nodes

```bash
kubectl describe node <node-name>
```

Look for:

* `Taints:` field
* Ensure pod has matching tolerations

---

## 📘 Summary

A `Pending` pod usually means Kubernetes can’t find a suitable node. This could be due to:

* Resource shortages
* Affinity/anti-affinity rules
* Taints and tolerations
* PVC unavailability

Would you like a YAML example that causes a pending state for learning purposes?
