## What is Ingress in Kubernetes

### ✅ Definition

An **Ingress** is a Kubernetes resource that manages **external HTTP and HTTPS access** to Services inside the cluster. It acts as a smart entry point with routing rules.

### ✅ How it works

* Ingress defines rules for routing requests (e.g., based on hostname or URL path).
* Needs an **Ingress Controller** (like NGINX, Traefik) to work.

### ✅ Why use Ingress?

* Consolidates external access in one place.
* Supports SSL termination.
* Provides path-based and host-based routing.

### ✅ Example YAML

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

### ✅ Key Points

* Ingress needs an Ingress Controller running in the cluster.
* It does not expose TCP/UDP traffic — only HTTP/HTTPS.

**Use Ingress for smart, flexible, secure web traffic management!**
