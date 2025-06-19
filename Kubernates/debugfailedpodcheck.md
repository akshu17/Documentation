# Kubernetes Pod Debugging Checklist

Use this step-by-step guide to debug failing Pods in Kubernetes.

---

## ✅ 1. Check Pod status

```bash
kubectl get pods
kubectl describe pod <pod-name>
```

Look for:
- Status (`CrashLoopBackOff`, `ImagePullBackOff`, etc.)
- Events (bottom of `describe` output)
- Container states (Waiting, Running, Terminated)

---

## ✅ 2. Check logs

```bash
kubectl logs <pod-name>
kubectl logs <pod-name> -c <container-name>   # if multiple containers
kubectl logs --previous <pod-name>            # previous crashed logs
```

---

## ✅ 3. Exec into the container

```bash
kubectl exec -it <pod-name> -- /bin/sh
# or
kubectl exec -it <pod-name> -- /bin/bash
```

Check config files, test connectivity (`ping`, `curl`), etc.

---

## ✅ 4. Common issues & fixes

| Problem | What to check | Possible fix |
| --- | --- | --- |
| CrashLoopBackOff | Container keeps crashing | Fix app bug or probe config |
| ImagePullBackOff | Image pull failed | Check image name, registry credentials |
| Pending | Can't schedule | Check node resources, taints, affinity |
| Network issues | Can't reach other services | Check Service, DNS, NetworkPolicy |
| Config issues | Bad env vars, secrets | Verify ConfigMaps, Secrets |

---

## ✅ 5. Check Node status

```bash
kubectl get nodes
kubectl describe node <node-name>
```

Check node conditions: `NotReady`, `DiskPressure`, insufficient resources.

---

## ✅ 6. View Events & increase verbosity

```bash
kubectl get events --sort-by='.metadata.creationTimestamp'
kubectl get pods -v=9
```

---

## ✅ 7. Delete & recreate the Pod

```bash
kubectl delete pod <pod-name>
```

Deployment or ReplicaSet will recreate it.

---

## ✅ 8. Advanced: Ephemeral debug container

For stuck Pods (Kubernetes v1.18+):

```bash
kubectl debug -it <pod-name> --image=busybox --target=<container-name>
```

---

## 🎉 Done!

This checklist helps you troubleshoot common Pod issues step-by-step.
