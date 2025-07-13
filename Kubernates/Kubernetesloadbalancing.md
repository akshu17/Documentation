# ⚖️ Kubernetes Load Balancing: How It Works

Kubernetes provides multiple layers of **load balancing** to efficiently distribute traffic across services and applications. Here's a breakdown of how it handles load balancing:

---

## 🔁 1. Internal Load Balancing (Service-Level)

**Service Type:** `ClusterIP` (default)

* Kubernetes uses **iptables** or **IPVS** rules to load balance traffic across the Pods in a Service.
* When a request is made to a Service IP, the kube-proxy component redirects the request to one of the available Pods.

**Round-robin** or similar algorithms are used for load distribution.

**Example:**

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  selector:
    app: my-app
  ports:
    - port: 80
      targetPort: 8080
  type: ClusterIP
```

---

## 🌐 2. External Load Balancing (Service Type: LoadBalancer)

**Service Type:** `LoadBalancer`

* Used in cloud environments (e.g., AWS, GCP, Azure).
* Automatically provisions a cloud provider’s external load balancer.
* Routes external traffic to the Kubernetes Service which then load balances to Pods.

**Example:**

```yaml
apiVersion: v1
kind: Service
metadata:
  name: external-lb-service
spec:
  type: LoadBalancer
  selector:
    app: my-app
  ports:
    - port: 80
      targetPort: 8080
```

---

## 🌍 3. Ingress-Based Load Balancing

**Component:** Ingress Controller (e.g., NGINX, Traefik, HAProxy)

* Acts as a **Layer 7 (HTTP/HTTPS)** load balancer.
* Routes traffic based on **hostnames**, **paths**, or **TLS rules**.
* Common in production setups for managing multiple routes and TLS certificates.

**Example:**

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

---

## ⚙️ 4. Pod-Level Load Balancing

**Details:**

* Kubernetes ensures that traffic is evenly distributed across Pods behind a Service.
* The kube-proxy handles traffic routing at the node level.
* Uses health checks to ensure only healthy Pods receive traffic.

---

## 📌 Summary Table

| Load Balancing Type | Description                        | Component          |
| ------------------- | ---------------------------------- | ------------------ |
| ClusterIP (default) | Internal Pod-to-Pod load balancing | kube-proxy         |
| LoadBalancer        | External traffic via cloud LB      | Cloud provider     |
| Ingress             | HTTP/HTTPS routing at layer 7      | Ingress Controller |
| Headless Service    | Direct DNS-based load balancing    | DNS + client logic |

---

## 🔍 Notes

* For custom logic or advanced routing, combine Ingress + Service + NetworkPolicy.
* DNS round-robin occurs when using **Headless Services** (`ClusterIP: None`).

Would you like to see how to implement load balancing for microservices or compare with service meshes like Istio?
