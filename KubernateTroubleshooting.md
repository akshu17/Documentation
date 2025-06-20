
# 🛠️ Kubernetes Troubleshooting Cheat Sheet

## ✅ 1️⃣ Pods & Containers

**Common Issues:**
- `CrashLoopBackOff` — container keeps crashing
- `ImagePullBackOff` — can’t pull image
- `OOMKilled` — out of memory

**Commands:**
```bash
kubectl get pods
kubectl describe pod <pod-name>
kubectl logs <pod-name> [-c <container-name>]
kubectl logs --previous <pod-name>
```

**What to check:**
- Image name & pull secrets
- Environment variables
- Resources (CPU/Memory)

---

## ✅ 2️⃣ Deployments & Rollouts

```bash
kubectl rollout status deployment <deployment-name>
kubectl describe deployment <deployment-name>
kubectl rollout undo deployment <deployment-name>
```

---

## ✅ 3️⃣ Nodes & Cluster

```bash
kubectl get nodes
kubectl describe node <node-name>
```

Check:
- Ready status
- DiskPressure, MemoryPressure
- Node conditions

---

## ✅ 4️⃣ Networking & Services

```bash
kubectl get svc
kubectl describe svc <service-name>
kubectl get pods -o wide
kubectl exec -it <pod> -- /bin/sh
```

Check:
- Service type & endpoints
- Network Policies blocking traffic

---

## ✅ 5️⃣ Persistent Storage

```bash
kubectl get pv
kubectl get pvc
kubectl describe pvc <pvc-name>
```

Check:
- PVC bound status
- PV availability
- StorageClass

---

## ✅ 6️⃣ Permissions (RBAC)

```bash
kubectl auth can-i <verb> <resource> --as <user>
kubectl describe rolebinding <rolebinding>
```

Check:
- Roles, RoleBindings
- ServiceAccount permissions

---

## ✅ General Troubleshooting Commands

```bash
kubectl get pods -A
kubectl describe pod <pod>
kubectl logs <pod>
kubectl get events --sort-by=.metadata.creationTimestamp
```

---

## 🚀 Summary

| Issue | Command |
| ----- | ------- |
| Pod crashing | `logs`, `describe pod` |
| Rollout stuck | `rollout status`, `undo` |
| Node problem | `describe node` |
| Service not reachable | `describe svc`, exec + curl |
| Volume stuck | `get pvc`, `describe pvc` |
| Permission denied | `auth can-i` |

✅ **Tip:** Use `kubectl describe` for Events — very helpful!

