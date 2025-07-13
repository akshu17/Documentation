# 📈 Kubernetes Preemption & QoS – Interview Questions and Answers

This document includes frequently asked interview questions and detailed answers about **Pod Preemption** and **Quality of Service (QoS)** classes in Kubernetes.

---

## 📌 1. What is Preemption in Kubernetes?

**Answer:**
Preemption is a mechanism in Kubernetes that allows the scheduler to **evict lower-priority Pods** to make room for higher-priority Pods when cluster resources are insufficient.

---

## 📌 2. How does Preemption work?

**Answer:**
When a high-priority Pod cannot be scheduled due to lack of resources, the scheduler looks for lower-priority Pods that can be preempted (evicted). The scheduler:

1. Identifies nodes that could accommodate the new Pod if some Pods were removed.
2. Selects victims based on lowest priority.
3. Evicts victims and schedules the higher-priority Pod.

---

## 📌 3. How do you assign priority to a Pod?

**Answer:**
Define a `PriorityClass` resource and reference it in your Pod spec.

**Example:**

```yaml
apiVersion: scheduling.k8s.io/v1
kind: PriorityClass
metadata:
  name: high-priority
value: 100000
preemptionPolicy: PreemptLowerPriority
---
apiVersion: v1
kind: Pod
spec:
  priorityClassName: high-priority
  containers:
  - name: myapp
    image: nginx
```

---

## 📌 4. What are the components involved in preemption?

**Answer:**

* **PriorityClass**: Defines priority value and preemption policy.
* **Scheduler**: Makes the decision to preempt lower-priority Pods.
* **API Server**: Deletes the lower-priority Pods marked for preemption.

---

## 📌 5. What is Quality of Service (QoS) in Kubernetes?

**Answer:**
QoS in Kubernetes categorizes Pods based on their **resource requests and limits**. It helps the kubelet decide which Pods to evict under resource pressure.

---

## 📌 6. What are the QoS Classes in Kubernetes?

| QoS Class      | Description                                                         |
| -------------- | ------------------------------------------------------------------- |
| **Guaranteed** | All containers in Pod have equal memory & CPU `requests` = `limits` |
| **Burstable**  | At least one container has differing `requests` and `limits`        |
| **BestEffort** | No `requests` or `limits` are set                                   |

---

## 📌 7. How does Kubernetes evict Pods based on QoS?

**Answer:**
When a node is under resource pressure (e.g., low memory), the kubelet evicts Pods in this order:

1. BestEffort
2. Burstable
3. Guaranteed

---

## 📌 8. Can Preemption affect system stability?

**Answer:**
Yes. Frequent preemptions can lead to instability for low-priority workloads. Use carefully with proper testing.

---

## 📌 9. How do you disable preemption for a PriorityClass?

**Answer:**
Set `preemptionPolicy: Never` in the PriorityClass definition.

---

## ✅ Summary

| Feature     | Description                                            |
| ----------- | ------------------------------------------------------ |
| Preemption  | Evicts low-priority Pods for high-priority ones        |
| QoS Classes | Affects eviction during resource pressure              |
| Best for    | Managing resource fairness and workload prioritization |

Use QoS and Preemption to ensure **critical workloads** have guaranteed resources while efficiently using available capacity.
