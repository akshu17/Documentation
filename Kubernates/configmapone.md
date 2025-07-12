
# ✅ Kubernetes ConfigMap — Interview Questions, Answers, and Use Cases

---

## 📘 What is a ConfigMap in Kubernetes?

A ConfigMap is a Kubernetes object that allows you to decouple configuration artifacts from container images. It stores configuration data in key-value pairs and can be consumed by Pods as environment variables, command-line arguments, or configuration files.

---

## 🎯 Why Use ConfigMap?

- To avoid hardcoding config values in Docker images.
- To enable dynamic updates of configuration without rebuilding images.
- To maintain different configs for different environments (dev, staging, prod).

---

## 🛠️ Different Ways to Create a ConfigMap

### 1. From literal values

```bash
kubectl create configmap my-config --from-literal=env=dev
```

### 2. From a file

```bash
kubectl create configmap my-config --from-file=config.txt
```

### 3. From a directory

```bash
kubectl create configmap my-config --from-file=./config-dir/
```

### 4. From a manifest YAML file

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-config
data:
  app.properties: |
    ENV=production
    LOG_LEVEL=info
```

---

## 🚀 Using ConfigMap in a Pod

### 1. As environment variables

```yaml
envFrom:
  - configMapRef:
      name: my-config
```

### 2. As individual environment variables

```yaml
env:
  - name: ENV
    valueFrom:
      configMapKeyRef:
        name: my-config
        key: ENV
```

### 3. Mounted as a volume

```yaml
volumes:
  - name: config-volume
    configMap:
      name: my-config
containers:
  - name: app
    volumeMounts:
      - name: config-volume
        mountPath: /etc/config
```

---

## 🔐 ConfigMap vs Secret

| Feature       | ConfigMap            | Secret                    |
|---------------|----------------------|----------------------------|
| Use Case      | General config        | Sensitive data (passwords) |
| Storage       | Plaintext (etcd)     | Base64-encoded (etcd)      |
| Access        | Env / Volume         | Env / Volume               |
| Security      | Not encrypted        | More secure                |

---

## 🧠 Behavior and Limits

- Size limit: Less than 1 MB
- Pod restart required if used as env var
- Mounted ConfigMaps update dynamically

---

## 🧾 What Happens If ConfigMap is Deleted?

- If used as env var: Pod continues with existing values.
- If mounted: May cause broken mount or empty file.

---

## 📚 Commands

```bash
kubectl create configmap my-config --from-literal=key1=value1
kubectl create configmap my-config --from-file=app.properties
kubectl get configmap my-config -o yaml
kubectl edit configmap my-config
kubectl delete configmap my-config
```

---

## 💼 Real-world Use Cases

- Injecting configuration into containers
- Switching environments (dev, staging, prod)
- Dynamically changing logging or feature toggles

