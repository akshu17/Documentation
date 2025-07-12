
# 📂 Difference Between PersistentVolume (PV) and PersistentVolumeClaim (PVC)

In Kubernetes, PersistentVolume (PV) and PersistentVolumeClaim (PVC) work together to provide durable, decoupled storage for applications. Here's how they differ:

---

## ⚖️ Comparison Table

| Feature                          | **PersistentVolume (PV)**                                                                 | **PersistentVolumeClaim (PVC)**                                                   |
|----------------------------------|-------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------|
| **What it is**                   | A piece of **storage** in the cluster, provisioned by an admin or dynamically.            | A **request** for storage made by a user or a Pod.                                 |
| **Created by**                   | Cluster administrator or dynamically via StorageClass.                                    | User, developer, or Pod specification.                                             |
| **Scope**                        | Cluster-wide resource.                                                                    | Namespaced (belongs to a specific namespace).                                      |
| **Defines**                      | The **actual storage**: size, access mode, storage type, path, etc.                       | The **requirements** for storage: size, access mode, etc.                          |
| **Purpose**                      | To provide the actual storage that can be used by Pods.                                   | To bind to a PV that meets the request criteria.                                   |
| **Binding**                      | A PV binds to a PVC if it meets the request.                                              | PVC binds to a matching PV automatically.                                          |
| **Analogy**                      | Like a **hard disk** available in a data center.                                          | Like a **ticket/request** asking for a disk with certain features.                 |

---

## 🔄 Relationship Flow

1. **Admin or Kubernetes** creates a **PV** (storage available).
2. **User** creates a **PVC** (storage needed).
3. Kubernetes automatically finds a **PV** that matches the **PVC** request.
4. The **PV and PVC are bound** together.
5. A **Pod** can now use the PVC to access the persistent storage.

---

## 📝 Quick Example

### PersistentVolume (PV):
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: my-pv
spec:
  capacity:
    storage: 5Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: /mnt/storage
```

### PersistentVolumeClaim (PVC):
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
      storage: 5Gi
```

---

## ✅ Summary

- **PV is the supply** — actual storage.
- **PVC is the demand** — the request for storage.

Together, they enable persistent, portable, and reliable data storage in Kubernetes environments.
