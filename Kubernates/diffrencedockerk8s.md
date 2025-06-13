## 🚢 Docker vs Kubernetes

| Aspect                   | **Docker**                                                                               | **Kubernetes**                                                                                       |
| ------------------------ | ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| **What it is**           | A platform to build, ship, and run containers.                                           | A container orchestration system to manage many containers running on multiple machines.             |
| **Primary Purpose**      | Create and run **individual containers**.                                                | Automate **deployment, scaling, networking, and management** of containerized applications.          |
| **Level**                | Runs on a **single host** (laptop, server, or VM).                                       | Runs across a **cluster of hosts** (many servers working together).                                  |
| **Components**           | Docker Engine, Docker CLI, Docker Images, Docker Hub.                                    | Control plane (API server, scheduler, etcd) + Worker nodes (kubelet, kube-proxy, container runtime). |
| **Networking**           | Provides basic container networking on a single host.                                    | Provides advanced networking between containers **across nodes** (Services, DNS, Ingress).           |
| **Scaling**              | Manual: run more containers yourself.                                                    | Automatic: scale pods up/down automatically with controllers.                                        |
| **Fault Tolerance**      | Limited: if a container dies, you must restart it manually or with Docker Compose/Swarm. | High: auto-restarts failed containers, reschedules on healthy nodes.                                 |
| **Load Balancing**       | Basic: needs manual setup or external tools.                                             | Built-in: Services distribute traffic to healthy pods automatically.                                 |
| **Monitoring & Logging** | Basic logs per container.                                                                | Integrated monitoring, health checks, logs, and events at cluster level.                             |
| **Use Case**             | Running a **few containers** locally or on a single server.                              | Running **large, production-grade applications** with hundreds or thousands of containers.           |

---

## ✅ Quick Summary

* **Docker**: Great for packaging and running containers on a single machine.
* **Kubernetes**: Great for running **many containers** on **many machines**, with auto-scaling, self-healing, and rolling updates.
