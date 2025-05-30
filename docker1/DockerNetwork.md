# Docker Networks

## 🧠 What is a Docker Network?

In Docker, **networks** allow containers to communicate with each other, with the host machine, and with the outside world (like the internet). It’s Docker’s way of managing **inter-container communication** securely and efficiently.

---

## 🧱 Why Docker Networks Matter

- Let containers **talk to each other** (e.g., a web server talking to a database)
- Allow or block **external access** to containers
- Provide **isolation** and **security**
- Simulate **real-life environments** with multiple services

---

## 🔌 Types of Docker Networks

Docker provides several built-in network drivers:

### 1. **Bridge** (default for containers)
- Used when you don't specify a network.
- Containers can communicate **within the same host**.
- Best for **single-host setups**.

```bash
docker network ls
docker run -d --name web nginx
docker network inspect bridge
```

### 2. **Host**
- Removes network isolation between container and host.
- The container shares the host’s network stack.
- Used when **low latency or port sharing** is needed.

```bash
docker run --network host nginx
```

### 3. **None**
- No networking — the container is **completely isolated**.
- Useful for **security testing** or specialized scenarios.

```bash
docker run --network none nginx
```

### 4. **Overlay**
- Used in Docker Swarm.
- Enables communication between containers **across multiple Docker hosts**.
- Ideal for **distributed applications**.

```bash
docker network create -d overlay my_overlay
```

### 5. **Macvlan**
- Assigns a MAC address to the container so it appears as a **real device** on the network.
- Use for **legacy apps** that need direct access to the physical network.

---

## 🧪 Custom Networks (Bridge Type)

Custom bridge networks allow you to:

- Use **container names as DNS**.
- Better isolate environments.
- Automatically connect containers.

### Create a custom bridge network:

```bash
docker network create my_custom_net
docker run -d --name db --network my_custom_net postgres
docker run -d --name app --network my_custom_net myapp
```

Now `app` can reach `db` using the hostname `db`.

---

## 📦 Example: Web App + Database

```bash
docker network create webapp_net

docker run -d --name db \
  --network webapp_net \
  -e POSTGRES_PASSWORD=secret \
  postgres

docker run -d --name app \
  --network webapp_net \
  -e DB_HOST=db \
  myapp
```

> The app container connects to the database using the name `db`, thanks to Docker’s built-in DNS.

---

## 🧼 Cleaning Up

```bash
docker network ls                # List networks
docker network inspect <name>   # See details
docker network rm <name>        # Remove custom network
```

> 🚨 Note: You can't remove a network while containers are using it.

---

## 🛠️ Tips & Best Practices

- Use **custom networks** instead of the default bridge for better control.
- Name your networks clearly based on the app/environment.
- Keep services that need to talk to each other on the **same network**.
- Use **environment variables** or Docker secrets for credentials.

---

## 🧵 Want a Deep-Dive Blog?

Let me know if you want this converted into a **storytelling-style Medium blog** with real-life scenarios (like microservices or CI/CD pipelines). I'd be happy to craft it!

---

Would you like code examples for **Docker Compose** networks too?
