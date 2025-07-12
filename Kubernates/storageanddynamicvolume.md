# 📂 Kubernetes Storage Classes & Dynamic Persistent Volumes – Interview Questions & Answers

This document contains frequently asked interview questions and answers related to **StorageClass** and **Dynamic Volume Provisioning** in Kubernetes.

---

## 📌 1. What is a StorageClass in Kubernetes?

**Answer:**
A **StorageClass** in Kubernetes defines **how storage is dynamically provisioned**. It abstracts the details of the underlying storage provider (e.g., AWS EBS, GCP Persistent Disks, NFS) and automates volume creation using predefined parameters.

---

## 📌 2. What is Dynamic Volume Provisioning?

**Answer:**
Dynamic provisioning allows Kubernetes to automatically create a **PersistentVolume (PV)** when a **PersistentVolumeClaim (PVC)** is submitted and no existing PV matches the claim. This is done using a **StorageClass**.

---

## 📌 3. What are the key fields in a StorageClass definition?

**Answer:**

* `provisioner`: The volume plugin (e.g., `kubernetes.io/aws-ebs`)
* `parameters`: Config options for the provisioner (e.g., type, fsType)
* `reclaimPolicy`: What happens to the volume after PVC is deleted
* `volumeBindingMode`: When volume binding and dynamic provisioning should occur

---

## 📌 4. Example: StorageClass YAML for AWS

```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: standard
provisioner: kubernetes.io/aws-ebs
parameters:
  type: gp2
  fsType: ext4
reclaimPolicy: Delete
volumeBindingMode: Immediate
```

---

## 📌 5. How is a StorageClass used in a PVC?

**Answer:**
Reference the `storageClassName` in the PVC spec:

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: dynamic-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 5Gi
  storageClassName: standard
```

---

## 📌 6. What is `volumeBindingMode` in StorageClass?

**Answer:**

* `Immediate`: Volume is provisioned as soon as the PVC is created.
* `WaitForFirstConsumer`: Volume is provisioned only when a Pod using the PVC is scheduled. Useful for topology-aware provisioning.

---

## 📌 7. What is the difference between static and dynamic provisioning?

| Feature         | Static Provisioning                  | Dynamic Provisioning         |
| --------------- | ------------------------------------ | ---------------------------- |
| Volume creation | Manual (admin creates PVs)           | Automatic (via StorageClass) |
| PVC binding     | PVC binds to pre-created PV          | PVC triggers new PV creation |
| Flexibility     | Limited                              | Highly flexible              |
| Use case        | Legacy systems, fixed configurations | Modern, scalable workloads   |

---

## 📌 8. How do you list available StorageClasses?

```bash
kubectl get storageclass
```

---

## 📌 9. Can you set a default StorageClass?

**Answer:**
Yes. Add this annotation to the desired StorageClass:

```yaml
annotations:
  storageclass.kubernetes.io/is-default-class: "true"
```

---

## ✅ Summary

* StorageClass enables **dynamic provisioning** of Persistent Volumes.
* Eliminates the need for pre-provisioned storage.
* PVCs use StorageClass to request specific types of storage.
* `volumeBindingMode` helps optimize scheduling and provisioning.

StorageClasses are essential for automating scalable and efficient storage management in Kubernetes.
