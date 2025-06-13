## 📌 What is `kubectl`?

`kubectl` is the **command-line tool** for interacting with a **Kubernetes cluster**.

Think of `kubectl` as the **remote control** for Kubernetes — it lets you **create**, **view**, **update**, and **delete** resources like Pods, Deployments, Services, Namespaces, and more.

---

## 🎯 What does `kubectl` do?

✅ **Main tasks:**

* **Deploy applications** (e.g., create Pods, Deployments)
* **Inspect cluster resources** (e.g., check running Pods)
* **Manage configuration** (e.g., scale, update, or roll back applications)
* **Debug issues** (e.g., check logs, describe resources)

---

## ⚡ Common `kubectl` commands

| Task                     | Command                        | Example                                 |
| ------------------------ | ------------------------------ | --------------------------------------- |
| View cluster nodes       | `kubectl get nodes`            | Lists all worker and master nodes       |
| View pods                | `kubectl get pods`             | Lists all Pods in the default namespace |
| View pods in a namespace | `kubectl get pods -n dev`      |                                         |
| Apply a config file      | `kubectl apply -f my-app.yaml` | Creates or updates resources from YAML  |
| Get resource details     | `kubectl describe pod mypod`   | Shows detailed info about `mypod`       |
| View logs                | `kubectl logs mypod`           | Shows logs for `mypod`                  |

---

## 🗂️ Example

```bash
# Create a Deployment
kubectl apply -f deployment.yaml

# Check its status
kubectl get deployment

# Scale it to 3 replicas
kubectl scale deployment my-deployment --replicas=3
```

---

## ✅ Summary

**`kubectl`** is an essential tool for:

* **Managing** Kubernetes clusters
* **Controlling** workloads
* **Troubleshooting** resources

Without `kubectl`, you’d have to interact with the cluster’s API manually — so it’s the most practical way to work with Kubernetes.
