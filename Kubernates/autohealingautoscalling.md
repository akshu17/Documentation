# 📈 Kubernetes Autoscaling & Autohealing Cheat Sheet

## ✅ What is Autoscaling?

**Autoscaling** automatically adjusts:
- The number of pods
- The resource limits/requests for pods
- The number of nodes in your cluster

...based on the current workload.

---

## 🔑 Types of Autoscaling

### 1️⃣ Horizontal Pod Autoscaler (HPA)

- **What it does:** Increases or decreases the number of pod replicas.
- **Based on:** CPU, memory, or custom metrics.
- **YAML Example:**

    ```yaml
    apiVersion: autoscaling/v1
    kind: HorizontalPodAutoscaler
    metadata:
      name: my-hpa
    spec:
      scaleTargetRef:
        apiVersion: apps/v1
        kind: Deployment
        name: my-deployment
      minReplicas: 2
      maxReplicas: 5
      targetCPUUtilizationPercentage: 50
    ```

- **Command Example:**

    ```bash
    kubectl autoscale deployment my-deployment --cpu-percent=50 --min=2 --max=5
    ```

---

### 2️⃣ Vertical Pod Autoscaler (VPA)

- **What it does:** Automatically adjusts the CPU and memory requests and limits for containers.
- **Typical use:** For workloads with unpredictable resource needs.
- **YAML Example:**

    ```yaml
    apiVersion: autoscaling.k8s.io/v1
    kind: VerticalPodAutoscaler
    metadata:
      name: my-vpa
    spec:
      targetRef:
        apiVersion: "apps/v1"
        kind: Deployment
        name: my-deployment
      updatePolicy:
        updateMode: "Auto"
    ```

---

### 3️⃣ Cluster Autoscaler (CA)

- **What it does:** Automatically adds or removes nodes to ensure pods can be scheduled.
- **Where:** Common in cloud-managed Kubernetes clusters like EKS, GKE, or AKS.

---

## ✅ What is Autohealing?

**Autohealing** means Kubernetes ensures your desired application state by:
- Rescheduling pods to healthy nodes if a node fails.
- Restarting unhealthy containers.
- Using probes to detect and handle container issues.

---

## 🩹 Example: Liveness Probe

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: liveness-demo
spec:
  containers:
  - name: my-app
    image: myapp:latest
    livenessProbe:
      httpGet:
        path: /healthz
        port: 8080
      initialDelaySeconds: 5
      periodSeconds: 10
