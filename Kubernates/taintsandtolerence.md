# 📊 Kubernetes Affinity, Anti-affinity, NodeName, Taints & Tolerations – Interview Questions & Answers

This document covers essential Kubernetes interview questions and answers related to **Affinity**, **Anti-affinity**, **NodeName**, and **Taints & Tolerations** with command examples.

---

## 📌 1. What is Node Affinity in Kubernetes?

**Answer:**
Node Affinity is an advanced form of node selection that allows you to schedule Pods based on **rules** expressed using **label selectors**. It replaces NodeSelector with more flexible options.

Node affinity types:

* `requiredDuringSchedulingIgnoredDuringExecution`: **Mandatory** rules
* `preferredDuringSchedulingIgnoredDuringExecution`: **Soft preferences**

**Example:**

```yaml
nodeAffinity:
  requiredDuringSchedulingIgnoredDuringExecution:
    nodeSelectorTerms:
      - matchExpressions:
          - key: disktype
            operator: In
            values:
              - ssd
```

---

## 📌 2. What is Pod Affinity and Anti-Affinity?

**Answer:**

* **Pod Affinity**: Schedule Pods **near** other Pods with specific labels.
* **Pod Anti-Affinity**: Schedule Pods **away from** Pods with specific labels.

**Use cases:**

* Affinity: Microservices that benefit from proximity.
* Anti-Affinity: Distribute replicas across nodes/zones for HA.

**Example (Anti-Affinity):**

```yaml
podAntiAffinity:
  requiredDuringSchedulingIgnoredDuringExecution:
    - labelSelector:
        matchExpressions:
          - key: app
            operator: In
            values:
              - frontend
      topologyKey: "kubernetes.io/hostname"
```

---

## 📌 3. What is the difference between NodeSelector and Node Affinity?

| Feature         | NodeSelector             | Node Affinity                    |
| --------------- | ------------------------ | -------------------------------- |
| Flexibility     | Limited (key-value only) | Advanced match expressions       |
| Operators       | = only                   | In, NotIn, Exists, etc.          |
| Preferred rules | No                       | Yes (`preferredDuring...`)       |
| Recommended?    | Basic use cases          | Preferred for complex scheduling |

---

## 📌 4. What is `nodeName` and how is it used?

**Answer:**
`nodeName` directly assigns a Pod to a specific node (hardcoded placement). It bypasses scheduling decisions.

**Example:**

```yaml
spec:
  nodeName: node-1
```

**Note:** Not recommended for dynamic environments.

---

## 📌 5. What are Taints and Tolerations in Kubernetes?

**Answer:**

* **Taints**: Applied to nodes to repel Pods.
* **Tolerations**: Added to Pods to allow them to be scheduled on tainted nodes.

They work together to control where Pods **can’t** be scheduled, unless they explicitly **tolerate** the condition.

---

## 📌 6. Example: Add a taint to a node

```bash
kubectl taint nodes node1 key=value:NoSchedule
```

This prevents Pods from scheduling on `node1` unless they tolerate the taint.

---

## 📌 7. Example: Toleration in Pod YAML

```yaml
spec:
  tolerations:
    - key: "key"
      operator: "Equal"
      value: "value"
      effect: "NoSchedule"
```

This Pod can be scheduled on nodes with the matching taint.

---

## 📌 8. What are the types of taint effects?

**Answer:**

* `NoSchedule`: Pod will not be scheduled unless it tolerates the taint
* `PreferNoSchedule`: Try to avoid scheduling, but not guaranteed
* `NoExecute`: Evicts existing Pods if they don’t tolerate the taint

---

## 📌 9. Can you remove a taint from a node?

```bash
kubectl taint nodes node1 key=value:NoSchedule-
```

Adding `-` at the end removes the taint.

---

## 📌 10. When should you use Affinity or Taints?

| Use Case                  | Recommendation       |
| ------------------------- | -------------------- |
| Prefer Pod co-location    | Pod Affinity         |
| Enforce Pod separation    | Pod Anti-Affinity    |
| Limit node access by Pods | Taints & Tolerations |
| Hard bind to a node       | nodeName             |

---

## ✅ Summary

* **Affinity/Anti-Affinity**: Control **Pod-to-node** or **Pod-to-Pod** relationships
* **nodeName**: Direct hard-coded assignment
* **Taints and Tolerations**: Prevent/allow Pods on specific nodes

These features provide powerful **scheduling controls** to optimize reliability, security, and performance in Kubernetes clusters.
