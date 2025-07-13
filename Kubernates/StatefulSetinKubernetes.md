# 🧱 What is a StatefulSet in Kubernetes?

A **StatefulSet** is a Kubernetes controller used to manage **stateful applications** — applications that require **persistent storage**, **stable network identities**, and **ordered deployment and scaling**.

---

## 🎯 Key Features of StatefulSet

| Feature                     | Description                                                    |
| --------------------------- | -------------------------------------------------------------- |
| 🆔 Stable Network Identity  | Each pod gets a unique, stable hostname.                       |
| 💾 Persistent Storage       | Each pod can have its own persistent volume claim.             |
| 🔢 Ordered Deployment       | Pods are created or deleted **sequentially**, not in parallel. |
| 🧼 Graceful Rolling Updates | Ensures controlled and ordered updates to pods.                |

---

## 📦 Use Cases

* Databases (PostgreSQL, MongoDB, MySQL)
* Queues (Kafka, RabbitMQ)
* Distributed filesystems (HDFS, GlusterFS)

---

## 🛠️ Example YAML

```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
  name: web
spec:
  serviceName: "nginx"
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx
        volumeMounts:
        - name: www
          mountPath: /usr/share/nginx/html
  volumeClaimTemplates:
  - metadata:
      name: www
    spec:
      accessModes: ["ReadWriteOnce"]
      resources:
        requests:
          storage: 1Gi
```

---

## 📘 Summary

Use a **StatefulSet** when your application:

* Needs stable, unique network identity
* Requires persistent storage
* Depends on ordered pod startup/shutdown

Would you like the StatefulSet commands or Helm chart deployment examples?
