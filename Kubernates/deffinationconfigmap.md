## Kubernetes — ConfigMap & Secrets

### 🔹 ConfigMap

A **ConfigMap** in Kubernetes is an API object used to store non-sensitive configuration data in key-value pairs. It decouples environment-specific configurations from your container images, making your applications more portable and manageable.

#### ✅ Where is ConfigMap Used?

* Inject environment variables into containers
* Mount configuration files into Pods
* Pass command-line arguments or application settings
* Provide configuration for multiple containers in a Pod

#### 📄 Example: ConfigMap YAML

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  DB_HOST: "mysql"
  DB_PORT: "3306"
  FEATURE_X_ENABLED: "true"
```

#### 🚀 How to Use in a Pod

✅ As environment variables:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
spec:
  containers:
  - name: myapp-container
    image: myapp:1.0
    envFrom:
    - configMapRef:
        name: app-config
```

✅ As mounted files:

```yaml
volumes:
- name: config-volume
  configMap:
    name: app-config

volumeMounts:
- mountPath: /etc/appconfig
  name: config-volume
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
