# 🔐 How to Secure a Kubernetes Cluster

Securing a Kubernetes cluster involves multiple layers, including network, authentication, authorization, and runtime security. Below are best practices and tools for hardening a Kubernetes environment.

---

## 🧱 1. Authentication & Authorization

### ✅ Use RBAC

* Implement **Role-Based Access Control** (RBAC) for least-privilege access.
* Audit and rotate permissions regularly.

### ✅ Enable and Manage API Authentication

* Use certificates, tokens, or OIDC for secure authentication.
* Disable anonymous access to the Kubernetes API server.

---

## 🌐 2. Network Security

### ✅ Use Network Policies

* Restrict traffic between pods using **NetworkPolicies**.

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: deny-all
spec:
  podSelector: {}
  policyTypes:
  - Ingress
  - Egress
```

### ✅ Secure ETCD

* Encrypt etcd at rest.
* Use TLS for communication.
* Restrict access to etcd only to API server.

---

## 🔒 3. Secrets Management

### ✅ Use Kubernetes Secrets (encrypted at rest)

```bash
kubectl create secret generic my-secret --from-literal=password=pa$$w0rd
```

* Enable encryption at rest.
* Use external secret management tools like **HashiCorp Vault**, **Sealed Secrets**, or **External Secrets Operator**.

---

## 🧪 4. Runtime Security

### ✅ Enable Pod Security Standards

* Use **PodSecurity** admission or OPA/Gatekeeper for enforcing policies.

### ✅ Run Containers as Non-Root

```yaml
securityContext:
  runAsUser: 1000
  runAsNonRoot: true
```

### ✅ Use Read-Only Root Filesystem

```yaml
securityContext:
  readOnlyRootFilesystem: true
```

---

## 📦 5. Image and Supply Chain Security

### ✅ Scan Images

* Use tools like **Trivy**, **Grype**, or **Clair** to scan container images.

### ✅ Use Signed and Trusted Images

* Implement **image provenance** (e.g., Sigstore, Cosign).

---

## 📋 6. Audit and Monitoring

### ✅ Enable Audit Logs

* Configure audit policies on the API server.

### ✅ Monitor Cluster Activity

* Use Prometheus, Grafana, and tools like **Falco**, **Kube-bench**, or **Kube-hunter**.

---

## ✅ Summary Checklist

| Area               | Key Practices                                     |
| ------------------ | ------------------------------------------------- |
| Authentication     | RBAC, Certs, OIDC                                 |
| Network            | Network Policies, Secure etcd                     |
| Secrets            | Encrypt at rest, external managers                |
| Runtime            | Non-root users, read-only FS, PodSecurityPolicies |
| Images             | Scan, sign, and validate                          |
| Audit & Monitoring | Logs, alerts, behavioral monitoring               |

Would you like a customizable security audit checklist or YAML templates?
