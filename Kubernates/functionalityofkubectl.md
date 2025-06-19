## 📌 What is `kubectl`?

* `kubectl` is the command-line tool used to interact with a Kubernetes cluster.
* It communicates with the Kubernetes API Server to manage and control cluster resources.

---

## ⚙️ Core functionalities of `kubectl`

| Functionality            | What it does                                            | Example                                               |
| ------------------------ | ------------------------------------------------------- | ----------------------------------------------------- |
| **Create**               | Create resources like Pods, Deployments, Services, etc. | `kubectl apply -f pod.yaml`                           |
| **Get / View**           | Retrieve information about resources                    | `kubectl get pods`                                    |
| **Describe**             | Show detailed information about a resource              | `kubectl describe pod my-pod`                         |
| **Update / Edit**        | Update resources manually or via YAML                   | `kubectl edit deployment my-deployment`               |
| **Delete**               | Remove resources from the cluster                       | `kubectl delete pod my-pod`                           |
| **Scale**                | Change the number of pod replicas in a Deployment       | `kubectl scale deployment my-deployment --replicas=5` |
| **Rollout**              | Manage rolling updates and rollbacks                    | `kubectl rollout status deployment/my-deployment`     |
| **Logs**                 | View logs from containers                               | `kubectl logs my-pod`                                 |
| **Exec**                 | Execute a command inside a container                    | `kubectl exec -it my-pod -- /bin/bash`                |
| **Port-forward**         | Forward local port to a pod port                        | `kubectl port-forward pod/my-pod 8080:80`             |
| **Namespace operations** | Work within a specific namespace                        | `kubectl get pods -n kube-system`                     |

---

## 🔑 How `kubectl` works

1. **Run a command:** Example: `kubectl get pods`
2. **Talks to API Server:** Uses `kubeconfig` to authenticate.
3. **Performs action:** API server executes the request.
4. **Returns output:** Results are displayed in your terminal.

---

## ✅ Why `kubectl` is important

* It's the primary tool for interacting with Kubernetes clusters.
* Helps with automation and scripting.
* Supports debugging and troubleshooting.
* Works seamlessly with YAML and JSON manifests.

---

**Tip:** Always make sure your `kubectl` is configured with the correct context and namespace to avoid unintended changes!
