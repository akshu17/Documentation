## Kubernetes Architecture

Kubernetes follows a **master-slave architecture** (also referred to as **control plane and worker nodes**). It is designed to manage containerized applications across a cluster of machines.

---

### 📌 1. Control Plane Components (Master Node)

These components manage the Kubernetes cluster.

- **API Server (`kube-apiserver`)**  
  Exposes the Kubernetes API. It's the entry point for all administrative tasks and handles RESTful requests.

- **Controller Manager (`kube-controller-manager`)**  
  Runs controller processes that handle routine tasks in the cluster, such as:
  - Node controller
  - Replication controller
  - Endpoints controller

- **Scheduler (`kube-scheduler`)**  
  Assigns newly created pods to suitable nodes based on resource availability, constraints, and policies.

- **etcd**  
  A consistent and distributed key-value store used to store all cluster data (state, configuration, etc.). Acts as the single source of truth.

---

### 📌 2. Node Components (Worker Nodes)

These components run the actual applications (pods).

- **Kubelet**  
  Agent running on each node. Ensures containers are running in a Pod as expected.

- **Kube-proxy**  
  Maintains network rules on nodes and enables communication between pods and external services using IPs and ports.

- **Container Runtime**  
  Software responsible for running containers (e.g., Docker, containerd, CRI-O).

---

### 📌 3. Additional Concepts

- **Pod**  
  The smallest deployable unit in Kubernetes, encapsulating one or more containers.

- **Service**  
  An abstraction layer that defines a set of Pods and a policy to access them.

- **Namespace**  
  Provides logical separation of cluster resources for different teams/projects.

- **Volumes / Persistent Volumes**  
  Used to manage storage for pods that need data persistence.

---

### 🖼️ Diagram Overview

