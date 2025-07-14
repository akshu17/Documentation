# 🔐 How to Secure Kubernetes Secrets

Kubernetes Secrets are used to store sensitive information such as passwords, OAuth tokens, and SSH keys. To ensure these secrets are well-protected, several best practices and mechanisms should be followed.

---

## 🧱 1. Use Secrets Instead of ConfigMaps

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: mysecret
  namespace: default
stringData:
  username: admin
  password: secret123
```

**Why?** Secrets are base64-encoded and treated as sensitive data by Kubernetes.

---

## 🔐 2. Enable Encryption at Rest

Enable secrets encryption in the kube-apiserver config using a `EncryptionConfiguration`:

```yaml
apiVersion: apiserver.config.k8s.io/v1
kind: EncryptionConfiguration
resources:
  - resources:
      - secrets
    providers:
      - aescbc:
          keys:
            - name: key1
              secret: <base64-encoded-key>
      - identity: {}
```

Update the API server with:

```
--encryption-provider-config=/path/to/encryption-config.yaml
```

---

## 🛡️ 3. Restrict Access with RBAC

```yaml
kind: Role
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  namespace: default
  name: secret-reader
rules:
- apiGroups: [""]
  resources: ["secrets"]
  verbs: ["get", "list"]
```

Then bind it:

```yaml
kind: RoleBinding
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: read-secrets
  namespace: default
subjects:
- kind: User
  name: alice
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: secret-reader
  apiGroup: rbac.authorization.k8s.io
```

---

## 🕵️‍♂️ 4. Avoid Mounting Secrets as Environment Variables

Prefer mounting secrets as files:

```yaml
volumeMounts:
  - name: secret-volume
    mountPath: "/etc/secret-volume"
volumes:
  - name: secret-volume
    secret:
      secretName: mysecret
```

**Why?** Environment variables are harder to revoke and can be exposed in logs.

---

## 🔍 5. Audit Access to Secrets

Enable auditing in your cluster to track secret access.

```yaml
--audit-log-path=/var/log/k8s/audit.log
--audit-policy-file=/etc/kubernetes/audit-policy.yaml
```

---

## 🔐 6. Use External Secret Management Tools

Consider integrating:

* HashiCorp Vault
* AWS Secrets Manager
* Azure Key Vault
* Google Secret Manager

These offer:

* Advanced access controls
* Auto-rotation
* Audit trails

---

## ✅ Summary

| Practice                     | Purpose                          |
| ---------------------------- | -------------------------------- |
| Use Kubernetes Secrets       | Store sensitive data             |
| Encrypt secrets at rest      | Prevent raw etcd access leakage  |
| Use RBAC                     | Limit secret access              |
| Mount secrets as files       | Improve runtime security         |
| Audit secret access          | Track who accessed what and when |
| Use external secret managers | Centralized, secure management   |

Would you like examples using HashiCorp Vault with Kubernetes?
