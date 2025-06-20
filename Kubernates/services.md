
# 📌 Kubernetes Services — Detailed Explanation with Examples

## What is a Service?

A **Service** in Kubernetes is an abstraction that defines:
- A stable way to access a set of Pods
- Automatic load balancing
- A stable IP and DNS name, even though Pods are dynamic.

---

## How it works

- Selects Pods using labels.
- Gets a stable ClusterIP.
- `kube-proxy` routes requests to healthy Pods.

---

## Types of Services

| Type | Purpose | Exposed To |
|------|---------|-------------|
| **ClusterIP** | Internal only | Inside the cluster |
| **NodePort** | Open Node IP:Port | External |
| **LoadBalancer** | Cloud LB | External |
| **ExternalName** | Alias to external DNS | External |

---

## Key Fields

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-service
spec:
  type: ClusterIP  # or NodePort, LoadBalancer, ExternalName
  selector:
    app: my-app
  ports:
  - port: 80         # Service port inside cluster
    targetPort: 8080 # Container port
    nodePort: 30080  # Only for NodePort
```

---

## Example: ClusterIP

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-clusterip-service
spec:
  type: ClusterIP
  selector:
    app: backend
  ports:
  - port: 80
    targetPort: 8080
```

- Internal only.
- Other Pods reach it at `http://my-clusterip-service:80`.

---

## Example: NodePort

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-nodeport-service
spec:
  type: NodePort
  selector:
    app: backend
  ports:
  - port: 80
    targetPort: 8080
    nodePort: 30080
```

- Accessible externally at `http://<NodeIP>:30080`.

---

## Example: LoadBalancer

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-loadbalancer-service
spec:
  type: LoadBalancer
  selector:
    app: backend
  ports:
  - port: 80
    targetPort: 8080
```

- Provisions a cloud Load Balancer (GCP, AWS, Azure).

---

## Example: ExternalName

```yaml
apiVersion: v1
kind: Service
metadata:
  name: my-external-service
spec:
  type: ExternalName
  externalName: api.example.com
```

- Maps DNS name: `my-external-service` → `api.example.com`

---

## How traffic flows

**Example for NodePort:**

```
Client → NodeIP:nodePort → kube-proxy → ClusterIP:port → Pod:targetPort
```

---

## Commands

```bash
# Create ClusterIP
kubectl expose deployment my-app --port=80 --target-port=8080

# Create NodePort
kubectl expose deployment my-app --type=NodePort --port=80 --target-port=8080

# Check Services
kubectl get svc
```

---

## Summary

| Goal | Service Type |
|------|-----------------|
| Internal only | ClusterIP |
| Expose with Node IP | NodePort |
| Use cloud LB | LoadBalancer |
| Alias to external DNS | ExternalName |

---

## Good to know

- Services provide stable DNS & IP.
- Load balance across Pods.
- kube-proxy handles routing.
- Combine with NetworkPolicies for security.

---

✅ **Kubernetes Services are the backbone of stable networking!**
