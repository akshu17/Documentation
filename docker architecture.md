
# 🏗️ Docker Architecture

Docker follows a **client-server architecture** with key components working together to build, run, and manage containers.

---

## 🔧 Main Components

### 1. **Docker Client (`docker`)**
- Command-line interface (`docker run`, `docker build`, etc.)
- Talks to the Docker daemon via REST API (usually over UNIX socket or TCP)
- Acts as the user's gateway to Docker

```bash
docker run nginx
```

➡️ Sends request to Docker daemon

---

### 2. **Docker Daemon (`dockerd`)**
- Core service running on the Docker Host
- Builds, runs, and manages containers
- Handles images, volumes, networks, etc.
- Listens to Docker API requests from the client

---

### 3. **Docker Objects**
- **Images**: Read-only templates used to create containers
- **Containers**: Runnable instances of images
- **Volumes**: Persist and share data
- **Networks**: Enable container communication
- **Plugins**: Extend Docker capabilities

---

### 4. **Docker Registries**
- Storage and distribution system for Docker images
- Public: Docker Hub (default)
- Private: Self-hosted registries

When you run:

```bash
docker pull ubuntu
```

➡️ Docker daemon fetches the image from Docker Hub

---

## 📊 Diagram Overview (Text Representation)

```
+----------------------+
|   Docker CLI (Client)|
+----------+-----------+
           |
           v
+----------------------+
|   Docker Daemon      |
|   (dockerd)          |
+----------+-----------+
           |
  ------------------------
  |      |       |       |
  v      v       v       v
Images Containers Networks Volumes
           |
           v
   Underlying OS (Linux/Windows)
```

---

## ⚙️ How It Works (Flow)

1. **You run a command** using Docker CLI.
2. **Docker Client sends API request** to the Docker Daemon.
3. **Daemon processes** the request:
   - Pulls image (if needed)
   - Creates a container from the image
   - Allocates resources, mounts volumes, etc.
4. Container is started and managed by the Daemon.

---

## 🔐 Additional Concepts

| Feature            | Description                                     |
|--------------------|-------------------------------------------------|
| Namespaces         | Provide container isolation                    |
| cgroups            | Limit container resource usage                 |
| Union file system  | Efficient image layering (AUFS, OverlayFS)     |
| Docker Engine API  | REST API used internally and by 3rd parties     |
