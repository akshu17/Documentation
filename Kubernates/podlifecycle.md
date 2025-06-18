# 📌 Kubernetes Pod Lifecycle Cheat Sheet

## 🔑 Pod Phases

| Phase         | Description                                                                    |
| ------------- | ------------------------------------------------------------------------------ |
| **Pending**   | Pod accepted but not yet running (e.g., waiting for scheduling or image pull). |
| **Running**   | Pod scheduled, containers created, at least one container running.             |
| **Succeeded** | All containers terminated successfully (exit code 0) and will not restart.     |
| **Failed**    | All containers terminated, at least one failed (non-zero exit code).           |
| **Unknown**   | Kubernetes cannot determine Pod state (e.g., Node unreachable).                |

---

## 🚦 Pod Lifecycle Steps

1️⃣ **Pending**

* Pod defined and accepted by API server.
* Scheduler assigns it to a Node.
* Images are being pulled.

2️⃣ **Running**

* Containers start on assigned Node.
* Readiness probes check if containers are ready.
* Liveness probes check if containers stay healthy.

3️⃣ **Succeeded**

* All containers complete successfully.
* Common for Jobs or batch processing.

4️⃣ **Failed**

* Containers complete but with errors.
* Pod won't restart if policy is `Never` or `OnFailure` conditions met.

5️⃣ **Unknown**

* Kubernetes can't reach Node or get state.

---

## ⚙️ Pod Restart Policies

```yaml
restartPolicy: Always     # Default for Deployments
restartPolicy: OnFailure  # Retry on non-zero exit codes (e.g., Jobs)
restartPolicy: Never      # Run once, never restart
```

---

## 📊 Useful Commands

| Command                      | Description                                       |
| ---------------------------- | ------------------------------------------------- |
| `kubectl get pods`           | List Pods and their phases.                       |
| `kubectl describe pod <pod>` | See detailed info and Events for troubleshooting. |
| `kubectl logs <pod>`         | Get container logs.                               |
| `kubectl delete pod <pod>`   | Delete Pod and force termination.                 |

---

## ✅ Example YAML

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: hello-pod
spec:
  containers:
  - name: hello
    image: busybox
    command: ["echo", "Hello, Kubernetes!"]
  restartPolicy: Never
```

* Creates a Pod that echoes a message.
* Will go: **Pending → Running → Succeeded**.

---

## 📌 Key Tips

* Use `kubectl describe pod` to debug Events.
* Probes control auto-restarts and health checks.
* Pods are ephemeral; prefer Deployments or ReplicaSets for self-healing workloads.
