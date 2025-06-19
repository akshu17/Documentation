## ✅ Probes in Kubernetes

### 📌 What are Probes?

Probes are built-in health checks used by Kubernetes to monitor and manage the state of containers running inside Pods. They help Kubernetes decide whether to:

* Restart a container (if it’s unresponsive)
* Send traffic to a container (only if it’s ready)
* Confirm that an application has fully started

---

### 🔑 Types of Probes

| Type                | Purpose                                                    | What happens on failure                     |
| ------------------- | ---------------------------------------------------------- | ------------------------------------------- |
| **Liveness Probe**  | Checks if the container is alive                           | Container will be restarted                 |
| **Readiness Probe** | Checks if the container is ready to receive traffic        | Container is removed from Service endpoints |
| **Startup Probe**   | Checks if the container’s application has started properly | Container will be restarted                 |

---

### ⚙️ How Probes Work

Kubernetes supports three ways to perform a probe:

* **HTTP GET:** Makes an HTTP request to a path (e.g., `/healthz`).
* **TCP Socket:** Checks if a TCP port is open.
* **Exec Command:** Runs a shell command inside the container.

---

### 📂 Example YAML with All Probes

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: probe-demo
spec:
  containers:
  - name: my-app
    image: my-app-image
    ports:
    - containerPort: 8080
    livenessProbe:
      httpGet:
        path: /healthz
        port: 8080
      initialDelaySeconds: 5
      periodSeconds: 10
    readinessProbe:
      httpGet:
        path: /ready
        port: 8080
      initialDelaySeconds: 5
      periodSeconds: 10
    startupProbe:
      httpGet:
        path: /startup
        port: 8080
      failureThreshold: 30
      periodSeconds: 10
```

---

### ✅ Benefits of Using Probes

* **Automatic self-healing:** Kubernetes restarts unhealthy containers.
* **Smooth deployments:** Only healthy and ready Pods get traffic.
* **Stability:** Helps ensure high availability of applications.

---

### 🗂️ Common Commands

```bash
# Describe Pod and see probe status
describe pod <pod-name>

# Check YAML with probes
kubectl get pod <pod-name> -o yaml
```

---

## 📌 Summary Table

| Probe         | Checks                         | Main Use                       |
| ------------- | ------------------------------ | ------------------------------ |
| **Liveness**  | Is it running?                 | Restart deadlocked apps        |
| **Readiness** | Is it ready to serve requests? | Control traffic routing        |
| **Startup**   | Has it finished booting?       | Handle slow-start applications |

---

✅ **Tip:** Proper probes = healthier apps, fewer outages!

---
