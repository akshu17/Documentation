
# Kubernetes Container Types (Multi-Container Pod Patterns)

In Kubernetes, a Pod can contain more than one container. These containers share network and storage, and they enable powerful architectural patterns.

---

## ✅ Why Multi-Container Pods?
- To **separate concerns** (e.g., application + helper)
- To enhance the app functionality without modifying it
- Common design patterns: Sidecar, Ambassador, Adapter, Init

---

## 🔁 Common Pod Patterns

| Pattern    | Description                                      | Use Case                        |
|------------|--------------------------------------------------|----------------------------------|
| Sidecar    | Supports the main container                      | Log forwarder, proxy             |
| Ambassador | Connects main container to external services     | API proxy, gateway               |
| Adapter    | Transforms output formats                        | Custom metrics for Prometheus    |
| Init       | Runs initialization logic before app starts      | DB check, config setup           |

---

## 1. Sidecar Pattern

Enhances the main container (e.g., logging, monitoring, proxy).

### Example:
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: sidecar-demo
spec:
  containers:
  - name: app
    image: nginx
  - name: log-agent
    image: busybox
    command: ["sh", "-c", "tail -n+1 -f /var/log/app.log"]
    volumeMounts:
    - name: log-volume
      mountPath: /var/log
  volumes:
  - name: log-volume
    emptyDir: {}
```

---

## 2. Ambassador Pattern

Acts as a proxy between app and external service.

### Example:
```yaml
containers:
- name: app
  image: myapp
- name: proxy
  image: envoyproxy/envoy
  args: ["--config-path", "/etc/envoy/envoy.yaml"]
```

---

## 3. Adapter Pattern

Transforms the output to a different format (e.g., custom to Prometheus).

### Example:
```yaml
containers:
- name: app
  image: custom-metrics-app
- name: metrics-adapter
  image: adapter
  args: ["--input=/metrics", "--output=prometheus"]
```

---

## 4. Init Containers

Run sequentially before app containers. Useful for bootstrapping.

### Example:
```yaml
initContainers:
- name: init-db
  image: busybox
  command: ['sh', '-c', 'until nslookup mydb; do echo waiting; sleep 2; done']
```

---

## 🧠 Interview Questions

1. What are the container types in a Pod?
2. Difference between Sidecar and Adapter?
3. Can Init containers run in parallel? → No.
4. Use cases for Sidecar pattern?
5. How do containers share data in a Pod? → Volumes.

---
