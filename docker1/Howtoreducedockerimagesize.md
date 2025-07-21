# 🐳 How to Reduce Docker Image Size (From 2GB or More)

A 2GB Docker image is often bloated due to unnecessary layers, dependencies, or inefficient base images. Here are steps to reduce it:

---

## 🔹 1. Use a Minimal Base Image

| Image        | Size       | Notes                          |
|--------------|------------|--------------------------------|
| `alpine`     | ~5MB       | Very small, best for lightweight apps |
| `debian:slim`| ~20–30MB   | Lighter version of Debian      |
| `ubuntu`     | ~29MB–60MB | Consider `ubuntu:minimal`      |

```dockerfile
FROM alpine
```

---

## 🔹 2. Combine Layers

Each `RUN`, `COPY`, `ADD` creates a new layer.

Combine them like this:

```dockerfile
RUN apt update && apt install -y \
    curl \
    git \
 && apt clean && rm -rf /var/lib/apt/lists/*
```

This avoids leftover cache and reduces layer count.

---

## 🔹 3. Remove Unnecessary Files

Clean up temporary files and build tools:

```dockerfile
RUN rm -rf /tmp/* /var/tmp/* \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*
```

---

## 🔹 4. Use `.dockerignore`

Prevent unnecessary files from being copied into the image (e.g., `.git`, `node_modules`, logs).

Example `.dockerignore`:

```
.git
*.log
node_modules
*.md
```

---

## 🔹 5. Use Multi-Stage Builds

Split build and runtime to discard dev dependencies:

```dockerfile
# Stage 1: Build
FROM node:18 AS builder
WORKDIR /app
COPY . .
RUN npm install && npm run build

# Stage 2: Runtime
FROM node:18-slim
WORKDIR /app
COPY --from=builder /app/dist /app
CMD ["node", "index.js"]
```

Only final artifacts go into the runtime image.

---

## 🔹 6. Avoid Installing Unnecessary Packages

Don’t use `apt install` or `npm install` for packages/tools that aren’t needed at runtime.

---

## 🔹 7. Use `docker-slim` (Optional)

You can use [`docker-slim`](https://github.com/docker-slim/docker-slim) to automatically reduce image size by stripping unneeded binaries and files.

---

## ✅ Summary

| Optimization Step            | Benefit                         |
|-----------------------------|----------------------------------|
| Use smaller base image      | Major size reduction             |
| Combine RUN commands        | Fewer layers                    |
| Clean up cache/temp files   | Reduce filesystem bloat         |
| Use `.dockerignore`         | Avoids copying junk             |
| Multi-stage builds          | Keep runtime lean               |
| Prune unused dependencies   | Only ship what’s needed         |

---

> 🧠 Reducing image size leads to **faster builds**, **quicker deployments**, and **less attack surface**.
