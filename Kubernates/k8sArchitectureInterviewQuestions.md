## 📌 Kubernetes Architecture — Interview Questions

### 1️⃣ What are the main components of the Kubernetes control plane?

* **API Server:** The front-end that exposes the Kubernetes API.
* **etcd:** A key-value store for all cluster data.
* **Controller Manager:** Runs controllers to reconcile the state of the cluster.
* **Scheduler:** Assigns Pods to nodes based on resource availability.
* **Cloud Controller Manager (optional):** Integrates with cloud providers.

---

### 2️⃣ What is etcd and why is it important?

* `etcd` is a **distributed key-value store** that stores **all cluster configuration and state**. It acts as the single source of truth for the cluster.

---

### 3️⃣ What are Kubernetes nodes?

* Nodes are the **worker machines** (physical or virtual) that run containers using **kubelet**, **kube-proxy**, and container runtime.

---

### 4️⃣ What does kubelet do?

* The `kubelet` is an agent on each node that ensures containers are running in a Pod as specified.

---

### 5️⃣ Explain the role of kube-proxy.

* `kube-proxy` maintains network rules on each node, enabling **Pod-to-Pod communication** and routing cluster traffic.

---

### 6️⃣ How does the Kubernetes Scheduler work?

* It watches for **unscheduled Pods** and assigns them to the most suitable nodes based on resource requirements, affinity rules, taints, and tolerations.

---

### 7️⃣ What are controllers in Kubernetes?

* Controllers are control loops that **watch desired vs. actual state** and make changes to reach the desired state. Examples: ReplicaSet Controller, Node Controller, Job Controller.

---

### 8️⃣ What is a Pod in Kubernetes?

* A Pod is the **smallest deployable unit** in Kubernetes. It can contain one or more tightly coupled containers that share storage, network, and runtime settings.

---

### 9️⃣ Can you explain the architecture flow when you run `kubectl apply`?

* `kubectl` sends the request to the API Server → API Server validates and persists the data in `etcd` → appropriate controllers detect the change and take actions → scheduler schedules Pods → kubelet runs the containers.

---

### 1️⃣0️⃣ What is the difference between Master Node and Worker Node?

* **Master Node:** Runs the control plane components (API Server, etcd, Controller Manager, Scheduler).
* **Worker Node:** Runs the containerized workloads (Pods) and node agents like kubelet and kube-proxy.

---

### 1️⃣1️⃣ What happens if the API Server goes down?

* The cluster cannot accept new changes, but existing workloads continue to run as kubelet directly manages the containers.

---

### 1️⃣2️⃣ How do you achieve High Availability (HA) for the control plane?

* By running multiple API Servers, Controller Managers, and Schedulers behind a load balancer, and using an HA `etcd` cluster.
