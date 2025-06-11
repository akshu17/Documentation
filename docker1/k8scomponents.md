## Components of Kubernetes

Kubernetes has a modular architecture, consisting of multiple components working together to manage containerized applications.

---

### 🧠 Control Plane Components (Master Node)

These components manage the overall state and orchestration of the cluster.

#### 1. **kube-apiserver**
- Acts as the frontend for the Kubernetes control plane.
- Handles all RESTful API requests.
- Validates and processes cluster configuration.

#### 2. **etcd**
- A consistent and distributed key-value store.
- Stores all cluster data (configuration, state, metadata).
- Acts as the **source of truth** for the cluster.

#### 3. **kube-scheduler**
- Assigns new pods to available nodes based on resource availability and constraints.
- Considers factors like CPU, memory, affinity, taints, and tolerations.

#### 4. **kube-controller-manager**
- Runs various controller processes to regulate the cluster state:
  - Node Controller
  - Replication Controller
  - Endpoints Controller
  - Service Account & Token Controller

#### 5. **cloud-controller-manager** (optional)
- Allows integration with cloud providers (e.g., AWS, GCP, Azure).
- Manages cloud-specific components like load balancers, volumes, etc.

---

### 🧱 Node Components (Worker Nodes)

These components run on each node and manage the workloads (Pods).

#### 1. **kubelet**
- Agent that ensures containers are running in a Pod.
- Communicates with the API server and executes Pod specifications.

#### 2. **kube-proxy**
- Manages network rules on nodes.
- Enables communication between services and external access.

#### 3. **Container Runtime**
- Software that runs containers (e.g., **containerd**, **CRI-O**, **Docker**).
- Kubernetes uses the **Container Runtime Interface (CRI)** to support different runtimes.

---

### 📦 Additional Kubernetes Objects (Not Components, But Crucial)

- **Pod**: Smallest deployable unit. Encapsulates one or more containers.
- **Service**: Provides stable networking endpoint and load balancing for Pods.
- **ConfigMap & Secret**: Manage application configuration and sensitive data.
- **Deployment**: Manages stateless application updates.
- **StatefulSet**: Manages stateful applications with persistent identity and storage.
- **DaemonSet**: Ensures a Pod runs on all (or specific) nodes.
- **Job & CronJob**: For batch and scheduled jobs.

---

### ✅ Summary

| Category          | Component              | Description                                      |
|------------------|------------------------|--------------------------------------------------|
| Control Plane     | kube-apiserver         | Entry point to the cluster (API gateway)         |
| Control Plane     | etcd                   | Cluster's data store                             |
| Control Plane     | kube-scheduler         | Schedules Pods onto nodes                        |
| Control Plane     | kube-controller-manager| Maintains desired state                          |
| Node              | kubelet                | Ensures Pods are running                         |
| Node              | kube-proxy             | Handles networking on the node                   |
| Node              | Container Runtime      | Runs the actual containers                       |

