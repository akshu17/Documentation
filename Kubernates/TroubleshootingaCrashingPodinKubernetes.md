# 🛠️ Troubleshooting a Crashing Pod in Kubernetes

When a Pod in Kubernetes keeps crashing, systematic debugging is required to find and resolve the issue.

---

## 🔍 Step-by-Step Troubleshooting Guide

### 1. 📋 Get Pod Status

```bash
kubectl get pods
kubectl describe pod <pod-name>
```

**Look for:**

* Events at the bottom (image pull errors, OOM kills, etc.)
* Exit codes (e.g., `Exit Code 1`, `CrashLoopBackOff`)

---

### 2. 📄 View Logs

```bash
kubectl logs <pod-name>
```

If the container restarts frequently:

```bash
kubectl logs <pod-name> --previous
```

**Look for:**

* Errors in application startup
* Stack traces
* Configuration issues

---

### 3. 🧪 Check Readiness/Liveness Probes

```bash
kubectl describe pod <pod-name>
```

**Check for:**

* Probe failures
* Timeout or incorrect paths in readiness/liveness configuration

---

### 4. 🧠 Investigate Resource Limits

```bash
kubectl describe pod <pod-name>
```

**Look for:**

* `OOMKilled` or high memory/CPU usage
* Verify if limits are too restrictive

---

### 5. 🔁 CrashLoopBackOff Analysis

**Common causes:**

* Application failing to start
* Misconfigured env vars
* Missing config/secret
* Failing init containers

**Use:**

```bash
kubectl get events --sort-by=.metadata.creationTimestamp
```

To get time-ordered events

---

### 6. 📦 Check Image & Pull Errors

```bash
kubectl describe pod <pod-name>
```

**Look for:**

* `ImagePullBackOff`
* Incorrect image name/tag
* Missing imagePullSecrets

---

### 7. 🔒 Validate ConfigMaps and Secrets

```bash
kubectl get configmap
kubectl get secret
```

**Ensure:**

* Config values are valid
* Secrets are base64 encoded correctly

---

### 8. 🧩 Check Init Containers

```bash
kubectl get pod <pod-name> -o jsonpath='{.status.initContainerStatuses[*].state}'
```

**Ensure:**

* Init containers complete successfully
* No permission or dependency failures

---

### 9. 🧼 Use Ephemeral Debug Container (if supported)

```bash
kubectl debug -it <pod-name> --image=busybox
```

**Useful for:** Inspecting Pod’s filesystem, mounted volumes, network issues

---

## ✅ Prevention Tips

* Add proper readiness/liveness probes
* Set resource limits appropriately
* Use `restartPolicy: Never` in dev to catch issues early
* Validate config before applying

---

Would you like a YAML checklist template for Pod debugging or a script that automates parts of this workflow?
