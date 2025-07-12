
# Kubernetes Interview Questions and Answers: PersistentVolume (PV) & PersistentVolumeClaim (PVC)

This document provides common interview questions and detailed answers about PersistentVolume (PV) and PersistentVolumeClaim (PVC) in Kubernetes, including examples and command-line usage.

---

## 📌 1. What is a PersistentVolume (PV) in Kubernetes?

**Answer:**
A PersistentVolume (PV) is a piece of storage in the cluster that has been provisioned by an administrator or dynamically provisioned using Storage Classes. It is a resource in the cluster just like a node is a cluster resource.

**Key Points:**
- Decouples storage from pod lifecycle
- Managed by the cluster
- Defined using `apiVersion: v1`, `kind: PersistentVolume`

**Example PV YAML:**
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: my-pv
spec:
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: /mnt/data
```

---

## 📌 2. What is a PersistentVolumeClaim (PVC)?

**Answer:**
A PersistentVolumeClaim (PVC) is a request for storage by a user. It is similar to a pod requesting specific compute resources.

**Key Points:**
- Requests specific size and access mode
- Binds to an available PV
- Defined using `apiVersion: v1`, `kind: PersistentVolumeClaim`

**Example PVC YAML:**
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: my-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
```

---

## 📌 3. How are PV and PVC bound together?

**Answer:**
Kubernetes matches a PVC to a suitable PV based on size and access mode. Once matched, they bind together and are used by a Pod.

---

## 📌 4. What are the Access Modes available for PV/PVC?

**Answer:**
- `ReadWriteOnce` (RWO): Mounted as read-write by a single node.
- `ReadOnlyMany` (ROX): Mounted read-only by many nodes.
- `ReadWriteMany` (RWX): Mounted as read-write by many nodes.

---

## 📌 5. How does dynamic provisioning work in Kubernetes?

**Answer:**
If no existing PV matches the PVC, Kubernetes can dynamically provision a new volume using a StorageClass.

**Example StorageClass:**
```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: standard
provisioner: kubernetes.io/aws-ebs
parameters:
  type: gp2
```

PVC with StorageClass:
```yaml
spec:
  storageClassName: standard
```

---

## 📌 6. How do you use a PVC in a Pod?

**Example Pod YAML:**
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pod-using-pvc
spec:
  containers:
  - name: app
    image: nginx
    volumeMounts:
    - mountPath: "/usr/share/nginx/html"
      name: my-storage
  volumes:
  - name: my-storage
    persistentVolumeClaim:
      claimName: my-pvc
```

---

## 📌 7. How do you create and manage PVs and PVCs using `kubectl`?

**Commands:**
```bash
# Create resources
kubectl apply -f pv.yaml
kubectl apply -f pvc.yaml

# Check status
kubectl get pv
kubectl get pvc

# Describe for detailed info
kubectl describe pv my-pv
kubectl describe pvc my-pvc
```

---

## 📌 8. What happens when a PVC is deleted?

**Answer:**
If the PVC is deleted, the volume becomes "Released" but the data still exists. Final cleanup depends on the **reclaim policy** of the PV (e.g., Retain, Recycle, Delete).

---

## 📌 9. What are Reclaim Policies in PV?

**Answer:**
- `Retain`: Keeps the data and requires manual cleanup.
- `Recycle`: Basic scrub (deprecated).
- `Delete`: Deletes the associated storage resource automatically.

---

## ✅ Tips for Interviews

- Be clear about the difference between PV and PVC.
- Understand binding and access modes.
- Know how dynamic provisioning works.
- Be familiar with StorageClasses and reclaim policies.
