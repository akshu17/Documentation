## 📄 Kubernetes Pod YAML Configuration Explained

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
  labels:
    app: my-app
spec:
  containers:
  - name: nginx-container
    image: nginx:latest
    ports:
    - containerPort: 80
```

---

### 🔑 Key-by-Key Explanation

| **Key**              | **Value**         | **Explanation**                                                               |
| -------------------- | ----------------- | ----------------------------------------------------------------------------- |
| `apiVersion`         | `v1`              | Defines the Kubernetes API version used for this object type (Pods use `v1`). |
| `kind`               | `Pod`             | Specifies that the object you are creating is a Pod.                          |
| `metadata`           | —                 | Provides data to identify the object, including its name and labels.          |
| ├─ `name`            | `my-pod`          | The unique name for the Pod within its namespace.                             |
| ├─ `labels`          | `app: my-app`     | Key-value pairs for organizing, selecting, and managing the Pod.              |
| `spec`               | —                 | Describes the desired state and configuration of the Pod.                     |
| ├─ `containers`      | —                 | A list of container definitions to run inside the Pod.                        |
| ├─ `- name`          | `nginx-container` | The name of the container inside the Pod.                                     |
| ├─ `image`           | `nginx:latest`    | The container image to use. Here it pulls the latest official NGINX image.    |
| ├─ `ports`           | —                 | Defines which ports the container exposes.                                    |
| ├─ `- containerPort` | `80`              | The port the container listens on (NGINX serves HTTP on port 80).             |

---

### ✅ Key Points

* `apiVersion` and `kind` tell Kubernetes **what** you want to deploy and which **API version** to use.
* `metadata` gives your Pod a **unique identity** and optional labels.
* `spec` describes **how the Pod should run**, including containers, images, and ports.
* `containers` must be a **list** (array) — so even a single container uses the `-` dash.
* `image` specifies **which container image** to run.
* `ports` tells Kubernetes which **port(s)** the container listens on inside the Pod.

---

Use this as a reference to understand and write your own Pod YAML files in Kubernetes! 🚀
