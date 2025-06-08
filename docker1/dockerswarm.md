# Docker Swarm

## What is Docker Swarm?

**Docker Swarm** is Docker’s native clustering and orchestration tool. It allows you to manage a cluster of Docker nodes (hosts) as a single virtual system, enabling you to deploy, manage, and scale containerized applications easily.

---

## Key Features of Docker Swarm

- **Clustering:** Groups multiple Docker engines into a single, virtual Docker engine.
- **Decentralized Design:** Multiple manager nodes to avoid single points of failure.
- **Service Orchestration:** Defines services that can run multiple container instances (replicas) across the swarm.
- **Load Balancing:** Automatically distributes incoming requests among containers.
- **Scaling:** Scale services up or down with simple commands.
- **Rolling Updates:** Update services without downtime by incrementally updating containers.
- **Security:** Uses mutual TLS for secure node communication.

---

## Basic Concepts

| Term           | Description                                |
|----------------|--------------------------------------------|
| **Node**       | A single Docker engine participating in the swarm (manager or worker). |
| **Manager Node** | Controls and manages the swarm, dispatches tasks. |
| **Worker Node** | Executes tasks assigned by manager nodes. |
| **Service**    | Defines the desired state for containers running in the swarm (e.g., number of replicas). |
| **Task**       | A container running as part of a service. |

---

## Example Workflow

1. **Initialize Swarm:**
   ```bash
   docker swarm init
