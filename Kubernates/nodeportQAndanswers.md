## Kubernetes NodePort Service — Interview Questions & Answers

---

### ✅ Q1: What is a NodePort Service in Kubernetes?

A **NodePort Service** exposes a Kubernetes Service on a static port on each Node’s IP address. It allows external clients to send traffic to `<NodeIP>:<NodePort>`.

---

### ✅ Q2: How does NodePort work internally?

When you create a NodePort Service:

* Kubernetes allocates a port (from the range 30000–32767) on every node.
* The **kube-proxy** sets up routing rules so that requests to that port are forwarded to the corresponding ClusterIP Service.
* The ClusterIP Service then load-balances requests to backend Pods.

---

### ✅ Q3: What is the default port range for NodePort?

By default, NodePorts use ports in the range **30000–32767**.

You can configure this range in the `kube-apiserver` with the `--service-node-port-range` flag.

---

### ✅ Q4: When should you use NodePort?

NodePort is ideal for:

* Simple testing and development.
* Exposing services without needing a cloud LoadBalancer.
* Bare-metal or on-premises clusters.

---

### ✅ Q5: What are the drawbacks of NodePort?

* Less flexible for production because it requires manual port management.
* No smart routing — just forwards traffic.
* You need to know node IPs to access the Service externally.

---

### ✅ Q6: Can you use a custom port for NodePort?

Yes. You can manually specify a NodePort in the YAML. If you don’t, Kubernetes assigns one automatically within the allowed range.

Example:

```yaml
ports:
  - port: 80
    targetPort: 8080
    nodePort: 30080
```

---

### ✅ Q7: How do you create a NodePort Service in YAML?

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-nodeport-service
spec:
  type: NodePort
  selector:
    app: my-app
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
      nodePort: 30080
```

---

### ✅ Q8: How do you access a NodePort Service?

From outside the cluster, use:

```
http://<NodeIP>:<NodePort>
```

---

### ✅ Q9: What happens if you delete a NodePort Service?

When you delete the Service, the reserved port on the nodes is released.

---

### ✅ Q10: How is NodePort related to LoadBalancer?

A LoadBalancer Service is built on top of NodePort + ClusterIP:

* It automatically provisions a cloud load balancer.
* The load balancer forwards traffic to the NodePort, which then forwards to the ClusterIP and Pods.

So, NodePort is an intermediate step under the hood.

---

## ✅ Key Takeaway

**NodePort makes a Service reachable externally by reserving a port on every Node. It’s simple but not always ideal for production.**
