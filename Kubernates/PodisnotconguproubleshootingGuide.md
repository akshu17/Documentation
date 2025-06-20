# Create a Markdown file for "Pod is not coming up — Troubleshooting Guide"

content = """
# 🐳 Kubernetes Troubleshooting: Pod Is Not Coming Up

## ✅ Scenario
You deploy a Pod (or Deployment) but the Pod stays stuck in:
- `Pending`
- `ContainerCreating`
- `CrashLoopBackOff`
- `Error`

Goal: Find out **why** and fix it.

---

## ✅ Step-by-Step Troubleshooting

### 1️⃣ Check Pod Status
```bash
kubectl get pods
kubectl describe pod <pod-name>
STATUS	What it means
Pending	Cannot schedule to a Node
ContainerCreating	Image/volume setup
CrashLoopBackOff	Container crashes repeatedly
Error	Container failed
2️⃣ Check Events in describe
Always show details

kubectl describe pod <pod-name>
Check the Events section:

Scheduling failures
Image pull errors
Probe failures
3️⃣ Check Node Status
Always show details

kubectl get nodes
kubectl describe node <node-name>
Check if Nodes are:

Ready
Have enough CPU / Memory
4️⃣ Check Container Logs
Always show details

kubectl logs <pod-name>
# For multiple containers:
kubectl logs <pod-name> -c <container-name>
Look for:

Application startup errors
Misconfigurations
Port conflicts
5️⃣ If Pending — Check Scheduling
Always show details

kubectl describe pod <pod-name>
Cause	Fix
Not enough resources	Scale up Nodes or adjust Pod requests.
NodeSelector / Affinity too strict	Relax rules.
Taints & Tolerations	Add proper tolerations.
6️⃣ Check Image Pull Issues
Look for ImagePullBackOff or ErrImagePull.
Causes:
Wrong image name.
Private registry → missing imagePullSecrets.
7️⃣ Check PVCs (Volumes)
If using PersistentVolumeClaims:

Always show details

kubectl get pvc
kubectl describe pvc <pvc-name>
Ensure PVC is Bound.
Unbound PVC → Pod stuck in ContainerCreating.
✅ Common Fixes

Problem	Solution
Image pull error	Fix image name, add pull secrets.
Not enough resources	Add Nodes or reduce requests.
Probe failures	Verify app health endpoints.
Unschedulable	Adjust NodeSelector / Affinity.
Volume not bound	Fix StorageClass or PVC.
📌 Key Commands

Always show details

kubectl get pods
kubectl describe pod <pod-name>
kubectl logs <pod-name>
kubectl get nodes
kubectl describe node <node-name>
kubectl get events
kubectl get pvc
kubectl describe pvc <pvc-name>
✅ Summary

Check	What to find
Pod describe	Events, scheduling, volumes
Pod logs	App errors
Node status	Schedulable & healthy
Scheduling rules	NodeSelector, Tolerations
PVCs	Bound status
✅ Good troubleshooting = check Events + Logs first!
