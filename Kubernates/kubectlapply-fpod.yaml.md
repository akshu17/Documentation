# 📄 `kubectl apply -f pod.yaml` Cheat Sheet

## ✅ What does it do?

* `kubectl apply -f pod.yaml` tells Kubernetes to **create or update** the resource(s) defined in the `pod.yaml` file.
* It makes sure the cluster's state matches the **desired state** described in the YAML.

---

## 📌 Command breakdown

| Part          | Meaning                                 |
| ------------- | --------------------------------------- |
| `kubectl`     | Kubernetes command-line tool            |
| `apply`       | Create or update resource declaratively |
| `-f pod.yaml` | Use configuration from this file        |

---

## ⚙️ How it works

| Scenario                    | Result                                   |
| --------------------------- | ---------------------------------------- |
| Resource **does not exist** | It will be **created**                   |
| Resource **exists**         | It will be **updated** to match the YAML |

This makes it **safe** and **idempotent**.

---

## 📦 Example `pod.yaml`

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: my-pod
spec:
  containers:
  - name: nginx-container
    image: nginx:latest
    ports:
    - containerPort: 80
```

### ✅ What this does

Creates a Pod named `my-pod` running an `nginx` container.

---

## 🗂️ Related Commands

| Command                      | Description                             |
| ---------------------------- | --------------------------------------- |
| `kubectl create -f pod.yaml` | **Create** resource; error if it exists |
| `kubectl apply -f pod.yaml`  | **Create or update** resource           |
| `kubectl delete -f pod.yaml` | **Delete** resource defined in file     |

---

## 🗝️ Best Practice

* Use `apply` for **declarative resource management**.
* Track YAML files in version control (Git) to manage changes.

---

## ✅ Example Usage

```bash
kubectl apply -f pod.yaml   # create or update a Pod
kubectl get pods            # verify it's running
kubectl delete -f pod.yaml  # delete the Pod
```

---

## 🚀 Tip

Always check your YAML for correct:

* Indentation
* Naming rules (lowercase, dashes instead of underscores)
* Correct API version and kind

---

**Happy K8s practicing! 🚀**
