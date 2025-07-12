# 🔍 Kubernetes Probes (Startup, Liveness, Readiness) – Interview Questions & Answers

This document provides commonly asked Kubernetes interview questions and detailed answers related to Probes: Startup, Liveness, and Readiness.

---

## 📌 1. What are probes in Kubernetes?

**Answer:**
Probes are diagnostic tools used by the Kubernetes kubelet to check the status of containers running in a Pod. Kubernetes uses three types of probes:

* **Liveness Probe:** Checks if the container is still running.
* **Readiness Probe:** Checks if the container is ready to accept traffic.
* **Startup Probe:** Checks if the container has started successfully.

---

## 📌 2. Why are probes important in Kubernetes?

**Answer:**
Probes help Kubernetes manage the lifecycle and health of containers. They ensure high availability and reliability by:

* Restarting containers that fail liveness checks
* Only routing traffic to ready containers
* Giving time to containers that require longer startup periods

---

## 📌 3. What is a Liveness Probe?

**Answer:**
Liveness probes determine whether a container is alive. If the liveness probe fails, Kubernetes will restart the container.

**Example:**

```yaml
livenessProbe:
  httpGet:
    path: /healthz
    port: 8080
  initialDelaySeconds: 3
  periodSeconds: 5
```

---

## 📌 4. What is a Readiness Probe?

**Answer:**
Readiness probes determine whether a container is ready to accept requests. If it fails, the container is removed from the Service endpoint list.

**Example:**

```yaml
readinessProbe:
  httpGet:
    path: /ready
    port: 8080
  initialDelaySeconds: 5
  periodSeconds: 5
```

---

## 📌 5. What is a Startup Probe?

**Answer:**
Startup probes are used for slow-starting applications. They delay liveness and readiness checks until the startup probe succeeds.

**Example:**

```yaml
startupProbe:
  httpGet:
    path: /startup
    port: 8080
  failureThreshold: 30
  periodSeconds: 10
```

---

## 📌 6. What types of handlers are available for probes?

**Answer:**
Kubernetes supports the following probe handlers:

* `httpGet`: Performs HTTP GET requests.
* `exec`: Runs a command inside the container.
* `tcpSocket`: Opens a TCP connection to the specified port.

---

## 📌 7. How do you configure a probe in a Pod spec?

**Answer:**
You configure probes in the container spec section:

```yaml
containers:
- name: my-app
  image: my-app-image
  livenessProbe:
    httpGet:
      path: /healthz
      port: 8080
    initialDelaySeconds: 3
    periodSeconds: 5
```

---

## 📌 8. Can you use multiple probes in a single container?

**Answer:**
Yes, a container can have all three probes (startup, readiness, liveness) configured together. This is a common practice to manage container lifecycle precisely.

---

## 📌 9. What happens if a readiness probe fails?

**Answer:**
If a readiness probe fails, the container remains running but is **removed from the Service endpoints**, meaning it stops receiving traffic until it becomes ready again.

---

## 📌 10. When should you use a startup probe?

**Answer:**
Use a startup probe for applications that take a long time to initialize. It prevents Kubernetes from prematurely killing the container due to failed liveness or readiness checks.

---

## ✅ Summary

| Probe Type | Purpose                      | Action on Failure            |
| ---------- | ---------------------------- | ---------------------------- |
| Liveness   | Checks if container is alive | Restarts the container       |
| Readiness  | Checks if container is ready | Removes from service routing |
| Startup    | Checks if app has started    | Blocks other probes          |

Probes help Kubernetes monitor and maintain application health and improve availability by detecting and handling unhealthy containers automatically.
