
# Kubernetes Interview Questions & Answers: Init Containers & Sidecar Containers

---

## 🔹 Init Containers

### 1. What is an Init Container?

An Init Container is a special container that runs and completes before the main application containers start in a Pod.

---

### 2. What are common use cases for Init Containers?

- Wait for an external service to become available
- Run database schema migrations
- Load secrets or configuration data
- Download dependencies before the app runs

---

### 3. How do Init Containers work?

- They run sequentially before the main container starts.
- If any Init Container fails, Kubernetes retries until it succeeds.

---

### 4. Example YAML for Init Container:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: init-demo
spec:
  initContainers:
  - name: init-myservice
    image: busybox
    command: ['sh', '-c', 'echo Waiting...; sleep 10']
  containers:
  - name: main-app
    image: nginx
```

---

### 5. Can a Pod have multiple Init Containers?

Yes. They run one after the other in the order they are defined.

---

### 6. What happens if an Init Container fails?

The Pod status remains `Init:` and it retries until the Init Container succeeds or the Pod is deleted.

---

## 🔹 Sidecar Containers

### 1. What is a Sidecar Container?

A Sidecar Container is a secondary container that runs alongside the main container in the same Pod to enhance or support its functionality.

---

### 2. What are common use cases for Sidecar Containers?

- Logging and monitoring agents
- Reverse proxies or service meshes (e.g., Envoy in Istio)
- Configuration reloaders
- Security proxies

---

### 3. How do Sidecar Containers differ from Init Containers?

| Feature         | Init Container           | Sidecar Container         |
|-----------------|--------------------------|----------------------------|
| When it runs    | Before main container    | Alongside main container  |
| Lifecycle       | Ends before app starts   | Runs as long as Pod runs  |
| Use case        | Setup/init tasks         | Support functionality     |

---

### 4. Can you scale a Sidecar independently?

No. All containers in a Pod scale together.

---

### 5. Example YAML for Sidecar:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: sidecar-demo
spec:
  containers:
  - name: app-container
    image: my-app
  - name: log-agent
    image: fluentd
    volumeMounts:
    - name: shared-logs
      mountPath: /logs
  volumes:
  - name: shared-logs
    emptyDir: {}
```

---

### 6. Can a Pod have both Init and Sidecar containers?

Yes. Init Containers run first and exit, then the Sidecar and main containers run concurrently.

---

## ✅ Key Takeaways

- Init Containers are used for setup before the app runs.
- Sidecar Containers provide continuous support during runtime.
- Both improve modularity and maintainability of Kubernetes apps.
