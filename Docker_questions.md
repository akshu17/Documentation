# 📘 Docker Basics: Images vs Containers

## 🖼️ What is a Docker Image?

A **Docker image** is a lightweight, standalone, and executable package that includes:

- Application code
- Libraries and dependencies
- Runtime (e.g., Python, Node.js)
- Configuration files
- Environment variables

### ✅ Uses of Docker Images

1. **Package Applications with Dependencies**
   - Ensures consistent environments across development, testing, and production.

2. **Create Containers Consistently**
   - Containers are launched from images, enabling reproducible deployments.

3. **Enable Portability**
   - Docker images can be shared via Docker Hub or private registries.

4. **Version Control**
   - You can tag images with specific versions (e.g., `myapp:1.0`, `myapp:latest`).

5. **CI/CD Integration**
   - Images are used in pipelines for building, testing, and deploying applications.

---

## 📦 What is a Docker Container?

A **Docker container** is a **running instance** of a Docker image. It includes:

- An isolated filesystem
- Its own network and process space
- A writable layer on top of the image

### 🆚 Image vs Container

| Feature        | Docker Image            | Docker Container             |
|----------------|--------------------------|-------------------------------|
| Type           | Blueprint / Template     | Running instance              |
| State          | Static (read-only)       | Dynamic (read/write)          |
| Created using  | `docker build`           | `docker run <image>`          |
| Usage          | To create containers     | To run apps in isolation      |
| Persistence    | Stored on disk           | Lives while running (unless committed) |

---

## 🧪 Example
