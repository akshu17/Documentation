# 📈 Setting Up Autoscaling in Kubernetes (HPA)

Kubernetes autoscaling allows you to automatically adjust the number of pods in a deployment, replica set, or stateful set based on resource utilization.

---

## ⚙️ What Is Horizontal Pod Autoscaler (HPA)?

HPA automatically scales the number of pods based on CPU utilization or other select metrics (like memory, custom metrics).

---

## 🔧 Step-by-Step Setup

### 1. ✅ Ensure Metrics Server Is Installed

HPA relies on the **metrics server** to fetch resource utilization metrics.

```bash
kubectl get deployment metrics-server -n kube-system
```

If it’s not installed, you can install it using:

```bash
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
```

---

### 2. 📦 Create a Deployment

Here’s a sample deployment with CPU requests:

```yaml
env:
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-app
spec:
  replicas: 2
  selector:
    matchLabels:
      app: web
  template:
    metadata:
      labels:
        app: web
    spec:
      containers:
      - name: web
        image: nginx
        resources:
          requests:
            cpu: "100m"
          limits:
            cpu: "200m"
```

---

### 3. ⚙️ Apply HPA

Create an autoscaler for the deployment:

```bash
kubectl autoscale deployment web-app --cpu-percent=50 --min=2 --max=10
```

---

### 4. 🔍 View the HPA

```bash
kubectl get hpa
```

You’ll see the target and current CPU usage, as well as current replica count.

---

## 🧪 Testing Autoscaling

To simulate CPU load:

```bash
kubectl run -i --tty load-generator --image=busybox /bin/sh
# Inside the container:
while true; do wget -q -O- http://<pod-ip>; done
```

You should see the number of replicas increase if usage exceeds threshold.

---

## 🔐 Additional Notes

* You can also scale on **memory** or **custom metrics**.
* HPA only works when resource requests are set on containers.
* Vertical Pod Autoscaler (VPA) and Cluster Autoscaler are also available for more control.

---

## ✅ Summary Table

| Step                   | Command/Action                     |
| ---------------------- | ---------------------------------- |
| Install Metrics Server | `kubectl apply -f <metrics-yaml>`  |
| Create Deployment      | Define `resources` in YAML         |
| Apply HPA              | `kubectl autoscale deployment ...` |
| Monitor HPA            | `kubectl get hpa`                  |
| Simulate Load          | Use BusyBox or stress tools        |

Would you like to see a YAML-based HPA manifest instead of using `kubectl autoscale`?
