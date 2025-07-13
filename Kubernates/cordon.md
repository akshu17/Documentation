# 📌 Kubernetes - Cordon, Drain, Multi-Master Cluster: Interview Q\&A

This document covers commonly asked Kubernetes interview questions on **cordon**, **drain**, and **multi-master cluster setup** with command usage.

---

## 📌 1. What does `kubectl cordon` do?

**Answer:**
`kubectl cordon` marks a node as **unschedulable**, preventing new Pods from being scheduled on it. Existing Pods are not affected.

**Command:**

```bash
kubectl cordon <node-name>
```

---

## 📌 2. What is the purpose of `kubectl drain`?

**Answer:**
`kubectl drain` safely evicts all Pods from a node and prepares it for maintenance. It marks the node as unschedulable and deletes Pods (respecting PodDisruptionBudgets).

**Command:**

```bash
kubectl drain <node-name> --ignore-daemonsets --delete-emptydir-data
```

* `--ignore-daemonsets`: Skips DaemonSet-managed Pods
* `--delete-emptydir-data`: Deletes emptyDir volumes (loss of data)

---

## 📌 3. What is the difference between `cordon` and `drain`?

| Feature               | Cordon                    | Drain                    |
| --------------------- | ------------------------- | ------------------------ |
| Schedules new Pods    | No                        | No                       |
| Deletes existing Pods | No                        | Yes (evicts them safely) |
| Common use case       | Quick block of scheduling | Node maintenance/upgrade |

---

## 📌 4. How do you make a node schedulable again?

**Answer:**
Use the `kubectl uncordon` command:

```bash
kubectl uncordon <node-name>
```

---

## 📌 5. What is a multi-master cluster in Kubernetes?

**Answer:**
A **multi-master cluster** consists of more than one master/control plane node to ensure high availability and fault tolerance of the control plane.

---

## 📌 6. Why do we need multiple master nodes?

**Answer:**

* Redundancy: Prevent single point of failure
* Scalability: Handle more API requests
* High availability: Components like etcd, scheduler, controller-manager are replicated

---

## 📌 7. What components are replicated in a multi-master setup?

**Answer:**

* `kube-apiserver` (usually behind a load balancer)
* `controller-manager`
* `scheduler`
* `etcd` (in clustered mode, e.g., 3 or 5 nodes)

---

## 📌 8. How do nodes communicate with multiple masters?

**Answer:**
Worker nodes and kubectl clients typically access the control plane through a **load balancer** that distributes traffic to healthy API servers.

---

## 📌 9. How do you handle etcd in a multi-master cluster?

**Answer:**
Run etcd in a **clustered mode** (odd number like 3, 5) with each master node hosting an etcd member. This ensures data consistency and leader election for high availability.

---

## 📌 10. Can you upgrade one master node at a time in multi-master setup?

**Answer:**
Yes, you can upgrade one master node at a time without downtime, as long as other masters remain functional. This allows for zero-downtime control plane upgrades.

---

## ✅ Summary

| Command            | Purpose                           |
| ------------------ | --------------------------------- |
| `kubectl cordon`   | Marks a node unschedulable        |
| `kubectl drain`    | Evicts Pods for safe node removal |
| `kubectl uncordon` | Makes a node schedulable again    |

* **Multi-master clusters** provide **high availability** and eliminate control plane SPOFs.
* `cordon` and `drain` are essential for safe node maintenance without impacting workloads.
