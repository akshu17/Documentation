# 🔐 How Does Kubernetes RBAC Work?

**Role-Based Access Control (RBAC)** in Kubernetes is a method of regulating access to resources within a cluster based on the roles of individual users or service accounts.

---

## 📘 Key Concepts

### 1. **Role**

* Defines a set of permissions (verbs) for resources within a **namespace**.

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: default
  name: pod-reader
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "watch", "list"]
```

### 2. **ClusterRole**

* Similar to Role, but applies cluster-wide or to non-namespaced resources.

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: node-reader
rules:
- apiGroups: [""]
  resources: ["nodes"]
  verbs: ["get", "watch", "list"]
```

### 3. **RoleBinding**

* Grants a Role’s permissions to a user/service account **within a namespace**.

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: read-pods
  namespace: default
subjects:
- kind: User
  name: jane
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io
```

### 4. **ClusterRoleBinding**

* Grants a ClusterRole’s permissions across the entire cluster.

```yaml
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: read-nodes-global
subjects:
- kind: User
  name: jane
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: ClusterRole
  name: node-reader
  apiGroup: rbac.authorization.k8s.io
```

---

## 🔄 Workflow Summary

1. Define roles (`Role` or `ClusterRole`).
2. Bind them to users/groups/service accounts using bindings.
3. Kubernetes API server checks access on every request.

---

## ✅ Best Practices

* Use **least privilege** principle.
* Prefer **Roles** over **ClusterRoles** when working in namespaces.
* Use **service accounts** for application-to-Kubernetes access.

Would you like a command-line walkthrough or a hands-on RBAC example setup?
