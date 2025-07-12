
# 🔐 Kubernetes RBAC – Interview Questions & Answers

This document covers common Kubernetes interview questions and answers on **RBAC (Role-Based Access Control)** with examples and key concepts.

---

## 📌 1. What is RBAC in Kubernetes?

**Answer:**
RBAC (Role-Based Access Control) is a method of regulating access to Kubernetes resources based on the roles assigned to users or service accounts. It allows administrators to define **who can perform what actions on which resources**.

---

## 📌 2. What are the main components of RBAC?

**Answer:**

1. **Role** – Defines a set of permissions within a **namespace**.
2. **ClusterRole** – Similar to Role but applied **cluster-wide** or across all namespaces.
3. **RoleBinding** – Grants the permissions defined in a Role to a **user/group/service account** within a **namespace**.
4. **ClusterRoleBinding** – Grants the permissions of a ClusterRole to a **user/group/service account** **cluster-wide**.

---

## 📌 3. What is the difference between Role and ClusterRole?

| Feature        | Role                        | ClusterRole                       |
|----------------|-----------------------------|------------------------------------|
| Scope          | Namespace-specific          | Cluster-wide or all namespaces     |
| Usage          | Access to namespace objects | Access to cluster-level resources  |
| Binding        | Used with RoleBinding       | Used with ClusterRoleBinding or RoleBinding |

---

## 📌 4. How does RoleBinding differ from ClusterRoleBinding?

| Feature            | RoleBinding                                  | ClusterRoleBinding                              |
|--------------------|-----------------------------------------------|--------------------------------------------------|
| Scope              | Namespace-specific binding                    | Cluster-wide binding                            |
| Binds to           | Role or ClusterRole (within namespace)        | Only ClusterRole                                 |
| Applies to         | Users, groups, or service accounts            | Users, groups, or service accounts               |

---

## 📌 5. Example: Create Role and RoleBinding

### 📝 Role YAML (namespace scoped)
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: dev
  name: pod-reader
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "watch", "list"]
```

### 🔗 RoleBinding YAML
```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: read-pods
  namespace: dev
subjects:
- kind: User
  name: dev-user
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io
```

---

## 📌 6. How do you check current RBAC rules?

**Answer:**
Use the following `kubectl` commands:
```bash
kubectl get roles --all-namespaces
kubectl get rolebindings --all-namespaces
kubectl describe rolebinding <name> -n <namespace>
kubectl auth can-i get pods --as=dev-user
```

---

## 📌 7. What is the purpose of `kubectl auth can-i`?

**Answer:**
This command checks if a user or service account has permission to perform a certain action.

**Example:**
```bash
kubectl auth can-i delete pods --as=dev-user
```

---

## 📌 8. Can you bind a ClusterRole to a specific namespace?

**Answer:**
Yes. Use a **RoleBinding** with a **ClusterRole**. This allows granting cluster-level permissions scoped to a single namespace.

---

## ✅ Summary

- RBAC allows fine-grained access control in Kubernetes.
- Use **Role/RoleBinding** for namespaced access.
- Use **ClusterRole/ClusterRoleBinding** for cluster-wide or shared access.
- Test permissions using `kubectl auth can-i`.

RBAC is essential for securing your cluster by enforcing the principle of **least privilege**.

---
