# 🛑 How Does Kubernetes Handle Node Failure?

Kubernetes is designed with high availability and resiliency in mind. When a node in a cluster fails or becomes unreachable, Kubernetes automatically detects the failure and initiates a series of recovery actions.

---

## 🕵️ Step-by-Step Behavior

1. **Node Heartbeat Monitoring**

   * Each node's kubelet sends periodic heartbeats to the Kubernetes control plane.
   * If the control plane doesn't receive a heartbeat within the `node-monitor-grace-period` (default: 40 seconds), the node is marked as `NotReady`.

2. **Pod Eviction**

   * After a grace period (`pod-eviction-timeout`, default: 5 minutes), the Node Controller evicts all pods from the unresponsive node.
   * These pods are rescheduled onto other available nodes by the scheduler.

3. **ReplicaSet and StatefulSet Rescheduling**

   * If the affected pods are part of a Deployment, ReplicaSet, or StatefulSet, new pods will automatically be created and scheduled on healthy nodes.

4. **Node Controller Cleanup**

   * The Node Controller manages cleanup of pods from the failed node and updates node status.

---

## 🔧 Important Configuration Parameters

| Parameter                   | Default | Description                                     |
| --------------------------- | ------- | ----------------------------------------------- |
| `node-monitor-grace-period` | 40s     | Time before a node is marked as `NotReady`      |
| `pod-eviction-timeout`      | 5m      | Time before pods are evicted from a failed node |

---

## 🧪 Useful Commands

```bash
kubectl get nodes
kubectl describe node <node-name>
kubectl get pods -o wide
```

These commands help verify node status and inspect pod distribution across nodes.

---

## ✅ Summary

* Kubernetes uses heartbeats to detect failed nodes.
* Failed nodes are marked `NotReady`.
* After a timeout, pods are evicted and rescheduled.
* High availability depends on having multiple replicas and sufficient cluster capacity.

Would you like to include a simulation scenario or troubleshooting guide?
