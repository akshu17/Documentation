## Kubernetes Services — NodePort, LoadBalancer, Headless — and Stateful vs Stateless Apps — Interview Q\&A

---

### ✅ NodePort Service — Q\&A

**Q1: What is a NodePort Service?**
A NodePort exposes a Service on a static port on each Node’s IP. It allows external clients to access the cluster using `<NodeIP>:<NodePort>`.

**Q2: How does NodePort work?**
Kubernetes opens a specific port on all nodes and forwards traffic to the backend Pods via a ClusterIP.

**Q3: When should you use NodePort?**
When you want basic external access without using a cloud LoadBalancer — for dev/test clusters or self-managed clusters.

**Q4: Example YAML:**

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-nodeport
spec:
  selector:
    app: my-app
  type: NodePort
  ports:
    - port: 80
      targetPort: 8080
      nodePort: 30036
```

---

### ✅ LoadBalancer Service — Q\&A

**Q1: What is a LoadBalancer Service?**
A LoadBalancer Service provisions an external cloud load balancer (like AWS ELB, GCP LB) and routes external traffic to backend Pods.

**Q2: How is it different from NodePort?**

* NodePort exposes ports on each node — you access using Node IPs.
* LoadBalancer provisions a single external IP/DNS — simpler for clients.

**Q3: Use case?**
When you want production-grade external access, with automatic traffic distribution across nodes.

**Q4: Example YAML:**

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-loadbalancer
spec:
  selector:
    app: my-app
  type: LoadBalancer
  ports:
    - port: 80
      targetPort: 8080
```

---

### ✅ Headless Service — Q\&A

**Q1: What is a Headless Service?**
A Service without a ClusterIP (`spec.clusterIP: None`). It doesn’t do load balancing — instead, it lets clients discover Pod IPs directly.

**Q2: Why use Headless Services?**
Useful for StatefulSets, databases, or apps needing direct Pod-to-Pod communication.

**Q3: How does DNS work with Headless Services?**
DNS queries return **all Pod IPs**, not a single ClusterIP. Clients can pick Pods themselves.

**Q4: Example YAML:**

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-headless
spec:
  clusterIP: None
  selector:
    app: my-app
  ports:
    - port: 80
```

---

### ✅ Stateful vs Stateless Applications — Q\&A

**Q1: What is a Stateless application?**
A stateless app does not store any client session or data on the server side. Requests are independent.

**Examples:** web frontends, REST APIs, static websites.

**Q2: What is a Stateful application?**
A stateful app keeps track of previous interactions or stores data persistently.

**Examples:** databases (MySQL, MongoDB), distributed caches, message queues.

**Q3: How does Kubernetes treat Stateless vs Stateful apps?**

* Stateless: Run as Deployments — Pods can be replaced freely.
* Stateful: Use StatefulSets — provide stable network IDs, persistent volumes, and ordered deployment.

**Q4: Why is this distinction important?**
It affects how Pods are scaled, upgraded, and recovered. Stateless apps can easily scale out. Stateful apps need careful handling to keep data integrity.

---

## ✅ Key Takeaway

| **Service Type** | **Purpose**                                 |
| ---------------- | ------------------------------------------- |
| ClusterIP        | Internal-only, default                      |
| NodePort         | External access via node IP and static port |
| LoadBalancer     | External access via a cloud load balancer   |
| Headless         | No load balancing, direct Pod discovery     |

| **App Type** | **Examples**               |
| ------------ | -------------------------- |
| Stateless    | Frontends, APIs            |
| Stateful     | Databases, storage systems |
