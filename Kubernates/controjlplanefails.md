## 📌 What Happens If There Is Only One Master Node and It Fails?

### 👉 Master Node Role

In Kubernetes, the **master node** (control plane) runs core components:

* **kube-apiserver**: Handles API requests.
* **kube-scheduler**: Schedules Pods to nodes.
* **kube-controller-manager**: Runs background controllers.
* **etcd**: Stores cluster state.

### 👉 What Happens If It Fails?

✅ **What keeps working:**

* Existing Pods and containers on worker nodes continue running.
* Local restarts within Pods (handled by kubelet and container runtime).

❌ **What stops working:**

* Cannot deploy new Pods, Services, or make cluster changes.
* No scheduling of new Pods or rescheduling failed Pods.
* No autoscaling or self-healing.

### 👉 Impact Table

| Works                       | Breaks                 |
| --------------------------- | ---------------------- |
| Existing running containers | Deployments & scaling  |
| Local container restarts    | New Pod scheduling     |
| Node networking             | Cluster config updates |

### 👉 Best Practice

* **Production clusters should have multiple master nodes (usually 3)** to ensure **high availability (HA)**.
* This eliminates a single point of failure.

### ✅ Summary

| Scenario                        | Result                                                   |
| ------------------------------- | -------------------------------------------------------- |
| **One master fails**            | Running Pods continue, but no new scheduling or changes. |
| **Multiple masters, one fails** | Cluster remains healthy and operational.                 |
