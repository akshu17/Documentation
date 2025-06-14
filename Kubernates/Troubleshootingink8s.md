## 🛠️ Troubleshooting in Kubernetes

Troubleshooting is essential to maintain a healthy Kubernetes cluster and to resolve issues with Pods, Services, and deployments.

---

## ✅ Common Troubleshooting Areas

### 1️⃣ Check Cluster Nodes

```bash
kubectl get nodes
```

Ensure all nodes show `Ready` status.

### 2️⃣ Check Pod Status

```bash
kubectl get pods
kubectl get pods -n <namespace>
```

Check for states like `Pending`, `CrashLoopBackOff`, or `Error`.

### 3️⃣ Describe Resources

```bash
kubectl describe pod <pod-name> -n <namespace>
```

Shows detailed info: events, container status, and reasons for failures.

### 4️⃣ Check Logs

```bash
kubectl logs <pod-name> -n <namespace>
# For multi-container pods:
kubectl logs <pod-name> -c <container-name> -n <namespace>
```

### 5️⃣ Exec into a Pod

```bash
kubectl exec -it <pod-name> -- /bin/sh
```

Run commands inside the container for debugging.

### 6️⃣ Check Events

```bash
kubectl get events
```

Helpful to see scheduling failures, image pull errors, or other issues.

### 7️⃣ Validate YAML and Config

```bash
kubectl apply --dry-run=client -f <file>.yaml
```

Check manifests before applying.

### 8️⃣ Check Networking

```bash
kubectl get svc
kubectl describe svc <service-name>
```

Test connectivity:

```bash
kubectl exec -it <pod-name> -- curl <service-name>:<port>
```

---

## 🔑 Tips

* Always check Pod status and recent events.
* Verify node health and resource usage.
* Use `kubectl explain` to understand manifest fields.

  ```bash
  kubectl explain deployment.spec
  ```
* Use `kubectl api-resources` to see available resource types.

---

## ⚡ Handy Commands

| Task                     | Command                         |
| ------------------------ | ------------------------------- |
| List all resources       | `kubectl get all`               |
| List Pods with node info | `kubectl get pods -o wide`      |
| Delete a Pod             | `kubectl delete pod <pod-name>` |

---

With these checks, you can systematically debug and fix most Kubernetes issues!
