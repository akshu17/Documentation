## Kubernetes Services (ClusterIP) — Interview Questions & Answers

---

### ✅ Q1: What is a Service in Kubernetes?

A **Service** is an abstract way to expose a set of Pods as a single, stable network endpoint. It provides **load balancing** and **service discovery** inside the cluster.

---

### ✅ Q2: What is a ClusterIP Service?

A **ClusterIP** Service is the **default** Service type in Kubernetes. It assigns an internal IP address to the Service, which is accessible **only within the cluster**. It’s used for internal communication between Pods.

---

### ✅ Q3: Why use a ClusterIP instead of connecting directly to Pod IPs?

Pod IPs are ephemeral — they can change when Pods restart. The ClusterIP stays **constant**, providing a stable DNS name and virtual IP that load-balances traffic across healthy backend Pods.

---

### ✅ Q4: How does a ClusterIP Service do load balancing?

The **kube-proxy** component configures iptables (or IPVS) rules to distribute incoming connections to one of the Pods selected by the Service’s label selector. This provides basic round-robin load balancing.

---

### ✅ Q5: Can a ClusterIP be accessed from outside the cluster?

No. A ClusterIP is **internal-only** by design. To expose a Service externally, you would use **NodePort**, **LoadBalancer**, or **Ingress**.

---

### ✅ Q6: What is the default type of Service in Kubernetes?

The default Service type is **ClusterIP**.

---

### ✅ Q7: How does DNS work with ClusterIP?

Kubernetes automatically creates a DNS name for each Service. Inside the cluster, Pods can use this DNS name to reach the Service, which resolves to the Service’s ClusterIP.

Example: `my-service.my-namespace.svc.cluster.local`

---

### ✅ Q8: How do you define a ClusterIP Service in YAML?

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app: my-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
  type: ClusterIP  # Default type
```

---

### ✅ Q9: How do you check the ClusterIP assigned to a Service?

```bash
kubectl get svc
```

This shows the Service’s name, type, ClusterIP, ports, and endpoints.

---

### ✅ Q10: Can you create a Service without a ClusterIP?

Yes. By setting `spec.clusterIP: None`, you create a **headless Service**. This doesn’t get a ClusterIP and is mainly used for direct Pod discovery, e.g., for StatefulSets.

---

## ✅ Key Takeaway

**ClusterIP provides a stable, internal load-balanced IP for accessing Pods reliably inside the cluster. It’s the most common way for internal services to communicate.**
