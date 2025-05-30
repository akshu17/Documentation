# 🖥️ Hypervisor Documentation

## 📘 What is a Hypervisor?

A **hypervisor** is software, firmware, or hardware that enables a single physical machine to run **multiple virtual machines (VMs)**. Each VM functions as an independent system with its own operating system and resources.

---

## 🧩 Why Use a Hypervisor?

Hypervisors enable:

- Efficient hardware utilization
- Running multiple OSes on one physical machine
- Isolation between environments (great for testing, development, and production)
- Virtual infrastructure for cloud platforms

# 📘 Definitions

## 🧠 Virtualization

**Virtualization** is the process of creating a **virtual version** of something—such as a server, storage device, network resource, or operating system—so that it can run independently from the physical hardware.

---

## 📦 Containerization

**Containerization** is a lightweight form of virtualization that involves **packaging an application and all its dependencies** (code, libraries, configuration files, etc.) into a single unit called a **container**.

---

## 🖼️ Docker Image

A **Docker image** is a **read-only template** that contains the application code, libraries, dependencies, and configuration needed to run a program. It serves as the blueprint for creating Docker containers.

---

## 📦 Docker Container

A **Docker container** is a **running instance of a Docker image**. It is an isolated environment where the application runs, with its own filesystem, processes, and network, separate from the host system.

---

## 🖥️ Hypervisor

A **hypervisor** is software, firmware, or hardware that enables a single physical machine to run **multiple virtual machines (VMs)**, each functioning like a separate computer with its own operating system.


# 📘 Difference Between Docker Image and Docker Container

## 🖼️ Docker Image

A **Docker image** is a **read-only template** that contains:

- Application code
- Dependencies
- Runtime
- Configuration files
- Environment settings

It serves as a **blueprint** for creating Docker containers.

---

## 📦 Docker Container

A **Docker container** is a **running instance** of a Docker image. It is:

- Isolated from the host system
- Writable (unlike the image)
- Temporary or persistent based on usage

---

## 🔍 Comparison Table

| Feature             | Docker Image                   | Docker Container                      |
|---------------------|---------------------------------|----------------------------------------|
| Type                | Blueprint / Template            | Running instance                       |
| State               | Static (read-only)              | Dynamic (read/write)                   |
| Created using       | `docker build`                  | `docker run <image>`                   |
| Purpose             | To define what to run           | To actually run the application        |
| Persistence         | Stored permanently              | Temporary unless committed             |
| Isolation           | Not applicable                  | Isolated environment                   |

---

## 🧪 Example

1. **Build Image**  
   ```bash
   docker build -t myapp .


