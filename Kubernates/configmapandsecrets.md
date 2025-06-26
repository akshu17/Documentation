## Kubernetes — ConfigMap & Secrets

### 🔹 ConfigMap

A **ConfigMap** is used to store non-sensitive configuration data as key-value pairs.

#### ✅ Use Cases:

* Application configs (e.g., log levels, environment flags)
* File-based configurations (.env files, property files)
* Environment variables for containers

#### 📄 Example: ConfigMap YAML

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-config
data:
  APP_MODE: "production"
  LOG_LEVEL: "debug"
```

#### 🔧 Using ConfigMap in Pod

✅ As environment variables:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: configmap-demo
spec:
  containers:
  - name: app
    image: nginx
    envFrom:
    - configMapRef:
        name: my-config
```

✅ As mounted files:

```yaml
    volumeMounts:
    - name: config-volume
      mountPath: /etc/config
  volumes:
  - name: config-volume
    configMap:
      name: my-config
```

---

### 🔹 Secret

A **Secret** is used to store sensitive information like passwords, tokens, or keys.

#### ✅ Use Cases:

* Database credentials
* TLS certificates
* API keys and tokens

#### 📄 Example: Secret YAML

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: my-secret
  type: Opaque
  data:
    username: YWRtaW4=         # 'admin' in base64
    password: MWYyZDFlMmU2N2Rm # '1f2d1e2e67df' in base64
```

#### 🔧 Creating Secret with kubectl

```bash
kubectl create secret generic my-secret \
  --from-literal=username=admin \
  --from-literal=password=1f2d1e2e67df
```

#### 🔧 Using Secret in Pod

✅ As environment variables:

```yaml
    env:
    - name: USERNAME
      valueFrom:
        secretKeyRef:
          name: my-secret
          key: username
```

✅ As mounted files:

```yaml
  volumes:
  - name: secret-volume
    secret:
      secretName: my-secret
```

---

### 🔍 ConfigMap vs Secret Comparison

| Feature       | ConfigMap           | Secret                  |
| ------------- | ------------------- | ----------------------- |
| Data type     | Plain text          | Base64-encoded          |
| Use for       | Config settings     | Sensitive info          |
| Storage       | etcd (plain)        | etcd (base64)           |
| Access method | Env var / Volume    | Env var / Volume        |
| CLI Tool      | `kubectl create cm` | `kubectl create secret` |
