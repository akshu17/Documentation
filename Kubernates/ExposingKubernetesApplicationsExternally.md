# 🌐 Exposing Kubernetes Applications Externally

Kubernetes provides several methods to expose applications running inside the cluster to the outside world. Below are the most common techniques:

---

## 1️⃣ NodePort

* Exposes a service on a static port on each node.
* Access using: `http://<NodeIP>:<NodePort>`

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-nodeport-service
spec:
  type: NodePort
  selector:
    app: myapp
  ports:
  - protocol: TCP
    port: 80
    targetPort: 8080
    nodePort: 30036
```

🔸 **Use case:** Quick testing or limited access setups.

---

## 2️⃣ LoadBalancer (for cloud providers)

* Creates an external load balancer with a public IP (supported by cloud providers).
* Access using: Public IP assigned by the cloud provider.

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-loadbalancer-service
spec:
  type: LoadBalancer
  selector:
    app: myapp
  ports:
  - protocol: TCP
    port: 80
    targetPort: 8080
```

🔸 **Use case:** Production-grade services in cloud environments.

---

## 3️⃣ Ingress (Advanced HTTP/S Routing)

* Uses Ingress resources to manage external access to the services in a cluster.
* Requires an Ingress Controller (like NGINX, Traefik).

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: my-ingress
spec:
  rules:
  - host: myapp.example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: my-service
            port:
              number: 80
```

🔸 **Use case:** Complex routing, TLS termination, path or host-based routing.

---

## ✅ Summary Table

| Method       | Best For                         | Notes                                 |
| ------------ | -------------------------------- | ------------------------------------- |
| NodePort     | Dev/Test environments            | Not ideal for production use          |
| LoadBalancer | Cloud-native production services | Automatically gets external IP        |
| Ingress      | Advanced HTTP/S routing          | Supports TLS, host/path-based routing |

---

Would you like sample YAML files or instructions on setting up an NGINX Ingress controller?
