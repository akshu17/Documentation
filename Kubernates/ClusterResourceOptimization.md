# 🚀 Optimizing a Kubernetes Cluster Low on Resources

When your Kubernetes cluster is running low on CPU, memory, or disk, it's important to take proactive steps to free up and better manage resources. Here's how you can optimize it:

---

## 🔍 1. Identify Resource Bottlenecks

### Check node usage:

```bash
kubectl top nodes
```

### Check pod usage:

```bash
kubectl top pods --all-namespaces
```

---

## 📦 2. Right-Size Workloads

### Review resource requests and limits:

```yaml
resources:
  requests:
    memory: "256Mi"
    cpu: "250m"
  limits:
    memory: "512Mi"
    cpu: "500m"
```

* Reduce overprovisioning.
* Avoid running without limits.

---

## 🧹 3. Clean Up Unused Resources

* Delete unused pods, deployments, services:

```bash
kubectl get all --all-namespaces
kubectl delete pod <pod-name> --namespace=<ns>
```

* Remove completed or failed jobs.
* Scale down idle workloads.

---

## 🎯 4. Use Autoscaling

### Horizontal Pod Autoscaler (HPA):

```bash
kubectl autoscale deployment myapp --cpu-percent=50 --min=1 --max=5
```

* Automatically scales pods based on CPU usage.

### Cluster Autoscaler (cloud-based clusters):

* Automatically adds/removes nodes as needed.
* Works with managed Kubernetes (EKS, GKE, AKS).

---

## 🗃️ 5. Optimize Storage Usage

* Clean up unused PVCs and volumes.
* Remove orphaned PVs:

```bash
kubectl get pvc --all-namespaces
```

---

## 🔧 6. Use Efficient Container Images

* Use lightweight base images (e.g., `alpine`).
* Remove unnecessary dependencies from images.

---

## 🧠 7. Monitor and Alert

* Set up monitoring with **Prometheus + Grafana**.
* Use **Kube-state-metrics**, **metrics-server**, and alerting rules.

---

## ✅ Summary

| Action                 | Benefit                              |
| ---------------------- | ------------------------------------ |
| Right-size workloads   | Avoids over-allocation               |
| Use autoscaling        | Dynamically adjusts resource use     |
| Clean unused resources | Frees up CPU, memory, and storage    |
| Monitor and alert      | Proactive response to resource usage |

Would you like YAML templates or CLI automation scripts for optimization?
