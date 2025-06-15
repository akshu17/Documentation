## ✅ Kubernetes Networking & Control Plane Questions

### 9️⃣ **Networking solutions in Kubernetes**

In Kubernetes, networking solutions ensure pods can communicate with each other and with services. Popular solutions:

* **Calico** — advanced networking & network policies.
* **Flannel** — simple overlay network.
* **Weave Net** — encrypted mesh network.
* **Cilium** — uses eBPF for performance and security.
* **Kube-Router** — integrates routing, firewall, and load balancing.

---

### 🔟 **Which network solutions are commonly used?**

* **Calico** — for production clusters needing network policies.
* **Flannel** — for development or small clusters.
* **Cilium** — for high-security, modern clusters.
* **Cloud-native CNIs** — like AWS VPC CNI, Azure CNI.

---

### 1️⃣1️⃣ **If the scheduler fails, what happens?**

* Running pods continue running.
* New pods **cannot be scheduled**.
* Failed pods **won’t be rescheduled**.
* Cluster self-healing stops until scheduler is back.

---

### 1️⃣2️⃣ **Can I create my own scheduler?**

✅ Yes!

* Kubernetes supports custom schedulers.
* You can run multiple schedulers in parallel.
* Pods can choose a scheduler via `spec.schedulerName`.

---

### 1️⃣3️⃣ **Can I create my own controller manager?**

✅ Yes!

* Kubernetes lets you create custom controllers.
* Controllers manage resources by watching them and reconciling state.
* Common way: use Operators (Operator SDK, Kubebuilder).

---

### 1️⃣4️⃣ **What is a Static Pod?**

* A pod managed **directly by kubelet** on the node.
* Defined via manifest files in `/etc/kubernetes/manifests`.
* Used for core components: kube-apiserver, etcd, controller-manager.
* Runs **even if the API server is down** — kubelet ensures it stays alive.

---

✅ **These answers help you handle interviews & troubleshooting scenarios involving networking and Kubernetes control plane components.**
