
# 🐳 Docker Networking: Bridge, Host, and None

Docker provides various networking drivers to manage how containers communicate with each other and the host. The three most commonly used network types are:

---

## 🔹 1. Bridge Network *(default)*

### ✅ Definition:
The **bridge** network is the default network driver for containers. When you create a container, it is connected to a virtual bridge (`docker0`) that allows communication with other containers on the same network via internal IPs.
# Docker Network: Bridge

1. **Bridge**

- This is a private internal network created by Docker on the host machine by the name `docker0`.
- This is the default network type for all containers which are created without any network configurations.
- By default, all the containers in the same bridge can communicate with each other without any extra configuration.
- We **cannot use container names** for communication; only **IP addresses** are allowed in the default bridge.


### 📦 Use Case:
Use this when you want **container-to-container communication** without exposing all ports to the host.

### 🔧 Example:
```bash
docker network create my_bridge_net
docker run -d --name app1 --network my_bridge_net alpine sleep 3600
docker run -it --name app2 --network my_bridge_net alpine ping app1
```


---

## 🔹 3. None Network

### ✅ Definition:
The **none** network isolates the container **completely** — no external network, no DNS, no internet access. The container only has a loopback interface (`localhost`).

### 📦 Use Case:
Use this when you want to **completely isolate** the container from all networks — for security or testing.

### 🔧 Example:
```bash
docker run -it --network none alpine
```

### 📌 Result:
No internet access, no pinging other containers, only access to `localhost`.

---

## 🔄 Summary Table

| Network Type | Container Gets IP? | Can Access Host? | Can Access Internet? | Use Case |
|--------------|--------------------|------------------|-----------------------|----------|
| `bridge`     | ✅ Yes (virtual)    | ✅ With ports     | ✅ Yes                 | Default, safe isolation |
| `host`       | ❌ Uses host IP     | ✅ Fully          | ✅ Yes                 | High-perf or native net access |
| `none`       | ❌ Loopback only    | ❌ No             | ❌ No                  | Max isolation |

---

## ✅ Best Practices

- Use `bridge` for most apps.
- Use `host` for high-performance networking.
- Use `none` for security-critical or compute-only containers.
