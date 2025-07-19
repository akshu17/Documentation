# 🧱 Namespaces in Linux

Linux **namespaces** are a feature of the kernel that isolate and virtualize system resources for processes. They are essential for **containers**, **sandboxing**, and **security**.

---

## 🧭 What Are Namespaces?

A namespace creates an isolated instance of a global system resource — processes inside a namespace **see and interact only** with resources in the same namespace.

---

## 🔧 Types of Namespaces

| Namespace   | Isolates                        | Description                                              |
|-------------|----------------------------------|----------------------------------------------------------|
| `mnt`       | Mount points                    | Isolates filesystem mount points                         |
| `pid`       | Process IDs                     | Each container sees only its own processes               |
| `net`       | Network interfaces, ports       | Provides isolated network stacks                         |
| `ipc`       | Inter-process communication     | Isolates message queues, semaphores, etc.                |
| `uts`       | Hostname and domain name        | Allows separate host/domain per container                |
| `user`      | User and group IDs              | Enables UID mapping (e.g., root inside container)        |
| `cgroup`    | Control groups                  | Isolates resource limits (CPU, memory, etc.)             |
| `time`      | System clocks                   | Isolates system and monotonic clocks                     |

---

## 🔍 How to View Namespaces

### Check all current namespaces:
```bash
lsns
```

### View namespaces of a process:
```bash
ls -l /proc/<PID>/ns
```

### Example:
```bash
ls -l /proc/1/ns
```

---

## ⚙️ Create a New Namespace (Example with `unshare`)

```bash
sudo unshare --net --pid --mount --uts --ipc --fork bash
```

This launches a new shell in isolated namespaces.

---

## 🐳 Use in Containers

Linux namespaces form the **foundation of Docker, Podman, LXC**, and other container technologies.

- Docker uses **all** major namespaces to create isolated environments.

---

## 🧠 Summary

Linux namespaces provide:
- **Security** through isolation
- **Scalability** for containerized environments
- **Flexibility** in multi-tenant systems

> 🔐 Without namespaces, containers would not exist as we know them.

---
