## 📄 Kubernetes YAML Pod Configuration Guide

### ✅ What is a Pod YAML Configuration File?

A **YAML configuration file** in Kubernetes describes the desired **state** of a resource — here, a **Pod**. It tells the Kubernetes API how to create and run the Pod, including its containers, volumes, network settings, and labels.

A Pod YAML file must follow a clear structure with key-value pairs.

---

### 📂 Basic Structure of a Pod YAML

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
  namespace: default  # Optional: defaults to 'default' if omitted
  labels:
    app: my-app
spec:
  containers:
  - name: my-container
    image: nginx:latest
    ports:
    - containerPort: 80
```

**Explanation:**

| Field        | Meaning                                                                |
| ------------ | ---------------------------------------------------------------------- |
| `apiVersion` | API version to use (`v1` for core resources like Pods)                 |
| `kind`       | Type of object (`Pod` here)                                            |
| `metadata`   | Data that helps uniquely identify the object (name, namespace, labels) |
| `spec`       | The specification for the Pod: containers, volumes, etc.               |

---

### ⚙️ Important Sections

* **metadata:**

  * `name`: Unique name for the Pod within the namespace.
  * `namespace`: Optional; defaults to `default`.
  * `labels`: Key-value pairs to tag and select Pods.

* **spec:**

  * `containers`: List of one or more containers the Pod should run.
  * Each container defines:

    * `name`: Container’s name
    * `image`: Docker image to run
    * `ports`: Ports exposed by the container

---

### 🔑 Important Notes

✅ YAML is **space-sensitive** — always use **spaces** (never tabs) for indentation.

✅ Indentation shows hierarchy — child fields are indented under parent fields.

✅ You can add more fields to `spec`:

* `volumes` for persistent storage
* `env` for environment variables
* `resources` for resource limits and requests

✅ You can use `kubectl apply -f <file>.yaml` to create/update the Pod from YAML.

✅ Always check YAML syntax with `kubectl apply --dry-run=client -f <file>.yaml`

---

### 🗂️ Example: More Detailed Pod YAML

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: busybox-pod
  labels:
    purpose: demo
spec:
  containers:
  - name: busybox
    image: busybox
    command: ['sh', '-c', 'echo Hello, Kubernetes! && sleep 3600']
```

---

### 📌 Key Commands

| Command                           | Description                        |
| --------------------------------- | ---------------------------------- |
| `kubectl apply -f pod.yaml`       | Create/Update the Pod from YAML    |
| `kubectl get pods`                | List Pods in the current namespace |
| `kubectl describe pod <pod-name>` | Detailed Pod info                  |
| `kubectl delete -f pod.yaml`      | Delete Pod defined in YAML         |

---

## ✅ Summary

Kubernetes YAML files are **declarative blueprints** for your cluster resources.
A clear, properly indented Pod YAML helps you consistently deploy applications.

✨ **Always keep YAML organized, validated, and versioned in your source control!**
