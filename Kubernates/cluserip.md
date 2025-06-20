
# 📌 Kubernetes ClusterIP Service — Detailed Guide with Example

## ✅ What is ClusterIP?

- **ClusterIP** is the default Kubernetes Service type.
- It creates a **virtual IP** accessible **only within the cluster**.
- Used for **internal communication** between Pods.

---

## ⚙️ How it works

- Kubernetes assigns a stable internal IP.
- Creates a DNS name.
- Uses `kube-proxy` to route to matching Pods.
- Load balances requests.

---

## 📂 Example YAML

```yaml
apiVersion: v1
kind: Service
metadata:
  name: backend-service
spec:
  type: ClusterIP
  selector:
    app: backend
  ports:
  - port: 80
    targetPort: 8080
```

- **selector**: finds Pods with `app=backend`.
- **port**: internal Service port (`80`).
- **targetPort**: container port (`8080`).

---

## ✅ How to use

1️⃣ Create Deployment:

```bash
kubectl create deployment backend --image=nginx --port=8080
```

2️⃣ Create ClusterIP Service:

```bash
kubectl expose deployment backend --port=80 --target-port=8080
```

3️⃣ Verify:

```bash
kubectl get svc backend
```

4️⃣ Test from another Pod:

```bash
kubectl run test-pod --rm -it --image=busybox -- /bin/sh
# Inside pod:
wget -qO- http://backend:80
```

---

## 🎯 When to use ClusterIP

| Use case | Example |
| -------- | ------- |
| Internal microservices | frontend → backend |
| Database connection | app → database |
| Not for public | No direct external access |

---

## 🗂️ ClusterIP vs Others

| Service | Scope | Use for |
| ------- | ----- | ------- |
| ClusterIP | Internal only | Pod-to-Pod |
| NodePort | External (Node IP:Port) | Dev/test |
| LoadBalancer | Cloud LB | Production public access |

---

## 🔑 Good to know

- You can set a custom IP: `spec.clusterIP: 10.96.0.10`
- For direct Pod IPs: use **headless** Service: `clusterIP: None`
- DNS: `service-name.namespace.svc.cluster.local`

---

## ✅ Key takeaway

**ClusterIP = stable internal gateway for a set of Pods**.

Best for **secure, internal-only service discovery and load balancing**.

---

🚀 Happy Clustering!
