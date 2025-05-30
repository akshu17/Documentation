# Port Mapping in Docker

**Port mapping in Docker** allows you to expose ports from a Docker container to your host machine, so that services running inside the container (like a web server) can be accessed from outside the container.

---

### 🔧 **What is Port Mapping?**

Port mapping connects a **host port** to a **container port**. This is essential when a containerized app (like an API or database) needs to communicate with the outside world or your local machine.

---

### 🧪 **Basic Syntax**

```bash
docker run -p <host_port>:<container_port> <image>
```

For example:

```bash
docker run -p 8080:80 nginx
```

* `8080`: Port on the host machine
* `80`: Port inside the container where Nginx listens
* This makes the Nginx server accessible at `http://localhost:8080`

---

### 🔀 **Multiple Port Mappings**

You can map multiple ports by repeating `-p`:

```bash
docker run -p 8080:80 -p 4430:443 nginx
```

---

### 💕 **What If You Don't Use Port Mapping?**

Without `-p`, the container's ports are not accessible from the host. For example:

```bash
docker run nginx
```

You won’t be able to access Nginx from your browser unless you exec into the container or do internal container networking.

---

### ⚠️ **Port Mapping vs. Exposing**

* `EXPOSE` in a Dockerfile documents which ports a container **might** use.
* `-p` or `--publish` actually **binds** container ports to host ports.

You still need `-p` at runtime to make ports accessible, regardless of `EXPOSE`.

---

### 📦 **Docker Compose Example**

In `docker-compose.yml`:

```yaml
services:
  web:
    image: nginx
    ports:
      - "8080:80"
```

---

### 📌 Summary

| Term         | Meaning                                          |
| ------------ | ------------------------------------------------ |
| `-p 8080:80` | Host port 8080 maps to container port 80         |
| `EXPOSE`     | Metadata about which ports a container uses      |
| Without `-p` | Container services are not accessible externally |

---

Would you like a visual diagram or real-world use case (e.g., mapping a Spring Boot app)?
