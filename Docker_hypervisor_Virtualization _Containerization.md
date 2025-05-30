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
functionality of an hypervisor
# 🖥️ Functionality of a Hypervisor

A **hypervisor** is a virtualization layer that allows multiple virtual machines (VMs) to run on a single physical host by abstracting and managing the underlying hardware resources.

---

## ⚙️ Key Functionalities

### 1. **Hardware Abstraction**
- Abstracts CPU, memory, storage, and networking resources from the physical machine.
- Provides each VM with virtual hardware.

### 2. **Resource Allocation**
- Dynamically allocates resources like CPU cycles, RAM, and storage to virtual machines based on demand or policies.

### 3. **Isolation**
- Ensures each virtual machine is isolated from others.
- Prevents crashes or malware in one VM from affecting others.

### 4. **VM Lifecycle Management**
- Supports creation, start, stop, pause, snapshot, and deletion of VMs.
- Manages the full lifecycle of virtual machines.

### 5. **Performance Monitoring**
- Tracks and logs performance of VMs and resource usage.
- Helps in optimizing the environment and detecting issues.

### 6. **Hardware Emulation**
- Emulates devices and hardware interfaces for VMs.
- Makes it possible for VMs to run different operating systems.

### 7. **Migration and Scalability**
- Supports **live migration** of VMs from one host to another.
- Enables scaling workloads without downtime.

### 8. **Security and Access Control**
- Implements access control policies.
- Manages VM-level firewalls, isolation, and user permissions.






