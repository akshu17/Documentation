## 📌 Kubernetes (K8s) Commands — Explained

Kubernetes uses the `kubectl` command-line tool to interact with your cluster. Below are **essential commands**, their purposes, and examples.

---

### ✅ **Basic Commands**

| Command                | What It Does                                  | Example                                |
| ---------------------- | --------------------------------------------- | -------------------------------------- |
| `kubectl version`      | Shows client & server version info            | `kubectl version --short`              |
| `kubectl cluster-info` | Displays cluster master & services info       | `kubectl cluster-info`                 |
| `kubectl get`          | Lists resources (pods, nodes, services, etc.) | `kubectl get pods`                     |
| `kubectl describe`     | Shows detailed info of a resource             | `kubectl describe pod my-pod`          |
| `kubectl create`       | Creates a resource from a YAML                | `kubectl create -f pod.yaml`           |
| `kubectl apply`        | Applies a YAML (create/update resource)       | `kubectl apply -f pod.yaml`            |
| `kubectl delete`       | Deletes a resource                            | `kubectl delete pod my-pod`            |
| `kubectl logs`         | Shows logs of a container                     | `kubectl logs my-pod`                  |
| `kubectl exec`         | Runs a command in a container                 | `kubectl exec -it my-pod -- /bin/bash` |

---

### ⚙️ **Namespace Related**

| Command                           | Purpose                   | Example                   |
| --------------------------------- | ------------------------- | ------------------------- |
| `kubectl get ns`                  | Lists all namespaces      | `kubectl get ns`          |
| `kubectl get pods -n <namespace>` | Lists pods in a namespace | `kubectl get pods -n dev` |
| `kubectl create ns <namespace>`   | Creates a namespace       | `kubectl create ns test`  |

---

### 📌 **Resource Info & Debug**

| Command                     | Purpose                            | Example                     |
| --------------------------- | ---------------------------------- | --------------------------- |
| `kubectl get api-resources` | Lists all supported resource types | `kubectl get api-resources` |
| `kubectl get events`        | Lists cluster events               | `kubectl get events`        |
| `kubectl top pod`           | Shows CPU/memory usage of pods     | `kubectl top pod`           |
| `kubectl top node`          | Shows resource usage of nodes      | `kubectl top node`          |

---

### 📦 **Scaling and Updating**

| Command                  | Purpose                                    | Example                                        |
| ------------------------ | ------------------------------------------ | ---------------------------------------------- |
| `kubectl scale`          | Scales up/down replicas                    | `kubectl scale deployment my-app --replicas=5` |
| `kubectl rollout status` | Checks rollout status of a deployment      | `kubectl rollout status deployment my-app`     |
| `kubectl rollout undo`   | Rollbacks a deployment to previous version | `kubectl rollout undo deployment my-app`       |

---

## ✅ **Handy Tips**

* Use `-n <namespace>` to run commands in a specific namespace.
* Use `--help` for help on any command:
  Example: `kubectl get --help`
* Use `kubectl explain <resource>` to get API reference:
  Example: `kubectl explain pod`

---

## 📂 **Example Workflow**

1️⃣ Create a resource:

```bash
kubectl apply -f deployment.yaml
```

2️⃣ Check status:

```bash
kubectl get deployments
kubectl get pods
```

3️⃣ Debug if needed:

```bash
kubectl describe pod <pod-name>
kubectl logs <pod-name>
```

4️⃣ Scale it:

```bash
kubectl scale deployment my-app --replicas=3
```

5️⃣ Delete when done:

```bash
kubectl delete -f deployment.yaml
```

---

## 📌 Summary

**`kubectl`** is the main tool to control your cluster: create, inspect, scale, debug, and delete resources easily.
