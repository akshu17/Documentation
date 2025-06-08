
# Linux Namespaces vs cgroups (Control Groups)

## 🧩 Overview

| Feature        | **Namespace**                                                 | **cgroup (Control Group)**                                           |
|----------------|---------------------------------------------------------------|----------------------------------------------------------------------|
| **Purpose**     | Provides **isolation** between processes                     | Provides **resource control and limitation**                         |
| **Main Function** | Isolate **what** a process can see                         | Limit **how much** a process can use                                 |
| **Type of Control** | Logical isolation                                          | Resource usage enforcement                                           |
| **Used By Docker?** | ✅ Yes                                                      | ✅ Yes                                                               |
| **Analogy**     | Each user lives in their own **apartment (view)**            | Each user has a **quota for water, electricity (resources)**         |

---

## 🧱 1. Linux Namespaces

Namespaces provide **process isolation** by wrapping system resources so each process gets its own view.

### Types of Namespaces:
- **PID:** Process IDs (each container sees its own PID 1)
- **NET:** Network interfaces, IPs, ports
- **MNT:** Filesystems and mounts
- **UTS:** Hostname/domain isolation
- **IPC:** Interprocess communication
- **USER:** User and group IDs

✅ Used to make containers appear like isolated systems.

---

## ⚖️ 2. Linux Control Groups (cgroups)

Cgroups manage and limit the **resources** that processes can use.

### What cgroups control:
- **CPU** usage
- **Memory** allocation
- **Disk I/O**
- **Network bandwidth** (indirectly)
- **Process count limits**

✅ Docker uses cgroups to ensure containers don’t hog system resources.

---

## 🧠 Summary

| Aspect         | **Namespace**                        | **cgroup**                             |
|----------------|---------------------------------------|----------------------------------------|
| Purpose        | Isolation                             | Resource management                    |
| Example        | Each container has its own hostname   | Limit container to 512MB RAM           |
| Docker Role    | Provides container separation         | Prevents resource abuse                |
