
# ✅ Kubernetes Interview Questions & Answers

---

## 🔐 Kubernetes Secrets — Q&A

### 1. ❓ What is a Secret in Kubernetes?
**Answer**: A Secret is a Kubernetes object used to store sensitive data such as passwords, tokens, and SSH keys. It keeps sensitive information separate from application code and configuration.

### 2. ❓ How are Secrets stored in Kubernetes?
**Answer**: They are stored in etcd, encoded in base64 by default (not encrypted unless encryption-at-rest is enabled).

### 3. ❓ How can a Pod access a Secret?
**Answer**:
- As environment variables
- Mounted as volumes
- Via service account tokens

### 4. ❓ What are the types of Secrets?
**Answer**:
- `Opaque` (default)
- `kubernetes.io/basic-auth`
- `kubernetes.io/dockerconfigjson`
- `kubernetes.io/service-account-token`
- `kubernetes.io/tls`

### 5. ❓ Can you decode a Secret manually?
**Answer**: Yes. Use `echo <base64_string> | base64 --decode`.

### 6. ❓ How to create a Secret from CLI?
```bash
kubectl create secret generic my-secret --from-literal=username=admin --from-literal=password=secret123
```

---

## 🧩 Kubernetes Pod Patterns — Q&A

### 1. ❓ What is a Pod in Kubernetes?
**Answer**: A Pod is the smallest deployable unit in Kubernetes that contains one or more containers sharing the same network namespace and storage.

### 2. ❓ What are the common Pod patterns?
**Answer**:
- **Single-container Pod** – simple use cases
- **Sidecar** – helper container (e.g., log processor, proxy)
- **Init container** – setup jobs (e.g., DB wait)
- **Ambassador** – network proxy pattern
- **Adapter** – translate output to compatible formats

### 3. ❓ Why use multiple containers in a single Pod?
**Answer**: When containers need to share volumes or networking (localhost communication) or work tightly together (e.g., log forwarder + app).

---

## 🏁 Init & Sidecar Containers — Q&A

### 1. ❓ What is an Init container?
**Answer**: An Init container is a special container that runs before app containers start. It completes setup tasks such as waiting for services, setting config, or database migrations.

### 2. ❓ How many Init containers can you have?
**Answer**: You can define multiple. They run sequentially in the order defined.

### 3. ❓ What happens if an Init container fails?
**Answer**: The Pod won't proceed to start the main containers until the Init container succeeds.

### 4. ❓ What is a Sidecar container?
**Answer**: A Sidecar container runs alongside the main app container and adds functionality such as:
- Logging
- Monitoring
- Config reload
- Proxying (e.g., Istio sidecar)

### 5. ❓ Key difference between Init and Sidecar?
| Feature         | Init Container              | Sidecar Container               |
|-----------------|-----------------------------|----------------------------------|
| Runs when       | Before app starts           | Alongside app                   |
| Lifecycle       | One-time                    | Runs with main app              |
| Purpose         | Setup/bootstrapping         | Support/continuous help         |
