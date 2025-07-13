# 📄 Kubernetes - Key Definitions

Here are the fundamental definitions commonly used in Kubernetes:

---

## 🛠️ Kubernetes (K8s)

**Definition:** Kubernetes is an open-source container orchestration platform that automates the deployment, scaling, and management of containerized applications.

---

## 🚀 Pod

**Definition:** The smallest and simplest unit in Kubernetes. A Pod encapsulates one or more containers that share storage, network, and a specification for how to run the containers.

---

## 📊 Node

**Definition:** A worker machine (virtual or physical) in Kubernetes. Each node runs Pods and contains the necessary components like kubelet, kube-proxy, and a container runtime.

---

## 🛠️ Cluster

**Definition:** A set of nodes that run containerized applications managed by Kubernetes. It consists of a control plane and one or more worker nodes.

---

## ⚖️ Deployment

**Definition:** A Kubernetes object that provides declarative updates for Pods and ReplicaSets. It manages the desired state, enabling rolling updates and rollbacks.

---

## 🔢 Service

**Definition:** An abstraction that defines a logical set of Pods and a policy to access them. Services enable communication between components or external access.

---

## 🧰 ConfigMap

**Definition:** Used to store non-confidential configuration data in key-value pairs. It helps decouple configuration from application containers.

---

## 🔐 Secret

**Definition:** Similar to ConfigMap, but used for storing sensitive data such as passwords, tokens, or SSH keys. Secrets are encoded in base64.

---

## 📊 PersistentVolume (PV)

**Definition:** A piece of storage in the cluster provisioned by an administrator or dynamically. It is independent of the lifecycle of any individual Pod.

---

## 📋 PersistentVolumeClaim (PVC)

**Definition:** A request for storage by a user. It consumes a PersistentVolume resource and specifies size, access mode, etc.

---

## 🌐 Ingress

**Definition:** Manages external access to services in a cluster, typically HTTP. It provides routing rules and optional TLS termination.

---

## 👥 Namespace

**Definition:** A way to divide cluster resources between multiple users. Useful for organizing objects in a multi-team or multi-project environment.

---

## 🚒 DaemonSet

**Definition:** Ensures that a copy of a Pod runs on all (or some) Nodes. Often used for logging, monitoring, or networking tasks.

---

## ♻️ ReplicaSet

**Definition:** Ensures a specified number of Pod replicas are running at any given time. Usually managed by Deployments.

---

## 🔷 StatefulSet

**Definition:** Like Deployment, but for stateful applications. Maintains a unique identity and stable network for each Pod.

---

## 🏢 Volume

**Definition:** A directory accessible to containers in a Pod. It enables persistent storage, data sharing, and lifecycle management independent of containers.

---

## 🌟 PriorityClass

**Definition:** Assigns a priority to Pods. Used with preemption to determine which Pods can be evicted when resources are scarce.

---

## ⚠️ Taints and Tolerations

**Definition:** Mechanism to control which Pods can be scheduled on which Nodes. Taints repel Pods; tolerations allow them to be scheduled on tainted nodes.

---

## 👥 Affinity/Anti-Affinity

**Definition:** Rules that influence Pod scheduling based on labels, encouraging or preventing placement with other Pods or on specific Nodes.

---

## 🚬 kubelet

**Definition:** An agent that runs on each node and ensures containers are running in a Pod.

---

## 🤖 kube-proxy

**Definition:** Maintains network rules on each node. It enables communication between services and supports traffic routing.

---

## 🧪 etcd

**Definition:** A distributed key-value store used by Kubernetes to store all cluster data.

---

Would you like these definitions converted into flashcards or quiz format?
