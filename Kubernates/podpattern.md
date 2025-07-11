
# Kubernetes Interview Questions & Answers: Pod Patterns

---

## 🔹 1. What are Pod Patterns in Kubernetes?

Pod patterns refer to common design patterns and best practices for managing Pods in Kubernetes, especially for specific scenarios like co-located containers, one-off tasks, or sidecar deployments.

---

## 🔹 2. What is the Sidecar Pattern?

### ➤ Definition:
A sidecar is a helper container that runs alongside the main container in a Pod. It shares the same network namespace and volume, enabling tight integration.

### ➤ Use Cases:
- Logging agent (e.g., Fluentd)
- Proxy (e.g., Envoy)
- Configuration reloader

---

## 🔹 3. What is the Ambassador Pattern?

### ➤ Definition:
An ambassador container is used to proxy network traffic to external services from the main application container.

### ➤ Use Cases:
- Communicating with external databases
- Adding TLS offloading

---

## 🔹 4. What is the Adapter Pattern?

### ➤ Definition:
An adapter container translates output from an application into a format consumable by another system (e.g., metrics formatting).

### ➤ Use Cases:
- Exporting custom metrics to Prometheus
- Logging data transformations

---

## 🔹 5. What is Init Container Pattern?

### ➤ Definition:
Init containers are specialized containers that run before the main application containers start. They are used for setup tasks.

### ➤ Use Cases:
- Waiting for external services
- Populating configuration files
- Running database migrations

---

## 🔹 6. Can multiple containers run inside one Pod?

Yes. Containers in a Pod share the same network and volume, and are used together for close cooperation, as seen in sidecar, ambassador, or adapter patterns.

---

## 🔹 7. What’s the difference between Sidecar and Init containers?

| Feature        | Sidecar Container     | Init Container       |
|----------------|-----------------------|-----------------------|
| When it runs   | Alongside main app    | Before app starts     |
| Duration       | Runs with the Pod     | Exits after setup     |
| Use case       | Monitoring, proxy     | Setup, waiting, config|

---

## 🔹 8. Why use multi-container Pods?

Multi-container Pods are useful when containers must:
- Share files or state (via volume)
- Share a network (localhost communication)
- Work tightly coupled as a unit

---

## 🔹 9. Can we scale Pods with sidecar individually?

No. All containers in a Pod scale together. You can’t independently scale containers in a Pod.

---

## 🔹 10. Real World Examples:

| Pattern    | Example                           |
|------------|-----------------------------------|
| Sidecar    | Envoy proxy in Istio mesh         |
| Ambassador | Proxy for legacy database         |
| Adapter    | Prometheus metrics sidecar        |
| Init       | Helm chart init scripts           |

---
