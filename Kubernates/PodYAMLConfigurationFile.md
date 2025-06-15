## 📄 Kubernetes Pod YAML Configuration File Explained

### What is it?

A **Pod YAML file** is a configuration file that tells Kubernetes how to create and run a Pod. A Pod is the smallest unit in Kubernetes — it can hold one or more containers.

---

### ✅ Basic Example

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
  labels:
    app: my-app
spec:
  containers:
  - name: my-container
    image: nginx:latest
    ports:
    - containerPort: 80
```

---

### 🔍 Key Sections

| Field          | Description                                |
| -------------- | ------------------------------------------ |
| **apiVersion** | Kubernetes API version (`v1` for Pod)      |
| **kind**       | Resource type — here it’s `Pod`            |
| **metadata**   | Information about the Pod (name, labels)   |
| **spec**       | What the Pod should run                    |
| **containers** | List of containers inside the Pod          |
| **image**      | Docker image to use (e.g., `nginx:latest`) |
| **ports**      | Ports exposed by the container             |

---

### ⚙️ How to Deploy

1. Save as `my-pod.yaml`

2. Apply to cluster:

   ```bash
   kubectl apply -f my-pod.yaml
   ```

3. Check status:

   ```bash
   kubectl get pods
   ```

---

### ✨ Tips

* Pods can contain **one or more containers** that share networking and storage.
* **YAML is indentation-sensitive** — always use spaces, not tabs.
* More features can be added: environment variables, volume mounts, resource limits, etc.

---

✅ **Pods = Smallest deployable units in Kubernetes!**
