
# 📌 Kubernetes NodePort Service — Detailed Guide with Example

## ✅ What is NodePort?

- **NodePort** is a Kubernetes Service type that exposes your Pods to **external traffic**.
- It opens a port on **every Node’s IP** so that you can access the Service from outside the cluster.

---

## ⚙️ How it works

- Kubernetes picks a port in the range `30000–32767` by default.
- It opens that port on **all Nodes**.
- Any request to `<NodeIP>:<NodePort>` is routed to the Service, which forwards it to healthy Pods.

---

## 📂 Example YAML

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-nodeport-service
spec:
  type: NodePort
  selector:
    app: my-web
  ports:
    - port: 80          # Cluster-internal Service port
      targetPort: 8080  # Container port
      nodePort: 30080   # Exposed port on each Node IP
```

- **selector**: Finds Pods with label `app=my-web`
- **port**: Internal port used by other cluster resources
- **targetPort**: Actual container port (`8080`)
- **nodePort**: External port on Nodes (`30080`)

---

## ✅ How to create a NodePort Service

**1️⃣ Create Deployment**

```bash
kubectl create deployment my-web --image=nginx --port=8080
```

**2️⃣ Expose it with NodePort**

```bash
kubectl expose deployment my-web --type=NodePort --port=80 --target-port=8080
```

**3️⃣ Check the Service**

```bash
kubectl get svc my-web
```

Example output:

```
NAME     TYPE       CLUSTER-IP     EXTERNAL-IP   PORT(S)        AGE
my-web   NodePort   10.96.132.45   <none>        80:30567/TCP   1m
```

Here:
- `ClusterIP`: for internal routing
- `NodePort`: 30567 (picked automatically)

**4️⃣ Access your app**

Open:
```
http://<NodeIP>:30567
```

---

## ⚡ Traffic flow

```
Client → NodeIP:NodePort → kube-proxy → ClusterIP:port → Pod:targetPort
```

---

## 🔑 Port range

- By default: `30000–32767`
- Can be customized with `--service-node-port-range` in `kube-apiserver`.

---

## ✅ When to use NodePort

| Use case | Details |
| -------- | ------- |
| ✅ Quick test | Easily expose for dev/testing |
| ✅ Small cluster | No LoadBalancer needed |
| ✅ With Ingress | Common pattern: LB/Ingress → NodePort |
| ❌ Standalone prod | Not robust enough for heavy production by itself |

---

## 🗂️ NodePort vs ClusterIP

| | ClusterIP | NodePort |
|---|---|---|
| Internal | ✅ | ✅ |
| External | ❌ | ✅ |
| Port exposed | No | Yes |
| Load balancing | Yes | Yes |

---

## ✅ Good to know

- NodePort works with **Ingress Controllers** and **external Load Balancers**.
- For production, use NodePort behind a LoadBalancer or Ingress for better security and high availability.
- Traffic hits every Node — so all Nodes must be reachable.

---

## ✅ Key takeaway

**NodePort = simplest way to expose your Pods externally by opening a port on every Node’s IP.**

Use with Ingress or LoadBalancer for more robust setups!

---

🚀 Happy Kubernetes-ing!
