# 🐳 How to Reduce a Large Docker Image (e.g., 2GB)

A 2GB Docker image is usually a result of unnecessary dependencies, large base images, or inefficient layering. Here’s how to reduce its size.

---

## ✅ 1. Use a Minimal Base Image

Choose a smaller base image to start with:

| Image         | Size   | Notes                          |
| ------------- | ------ | ------------------------------ |
| `alpine`      | \~5MB  | Smallest official Linux image  |
| `debian:slim` | \~22MB | Reduced Debian image           |
| `ubuntu`      | \~29MB | Use `ubuntu:minimal` if needed |

### Example:

```dockerfile
FROM alpine
```

---

## ✅ 2. Clean Up After Package Installs

Temporary files and cache should be removed to prevent image bloat.

### Before:

```dockerfile
RUN apt update && apt install -y curl git
```

### After:

```dockerfile
RUN apt update && apt install -y curl git \
 && apt clean \
 && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*
```

---

## ✅ 3. Use Multi-Stage Builds

Split the build environment from the runtime to exclude unnecessary files.

### Example:

```dockerfile
# Build stage
FROM node:18 AS builder
WORKDIR /app
COPY . .
RUN npm install && npm run build

# Runtime stage
FROM node:18-slim
WORKDIR /app
COPY --from=builder /app/dist /app
CMD ["node", "index.js"]
```

---

## ✅ 4. Minimize Layers

Combine commands to reduce image layers:

### Inefficient:

```dockerfile
RUN apt update
RUN apt install -y curl
```

### Efficient:

```dockerfile
RUN apt update && apt install -y curl && apt clean && rm -rf /var/lib/apt/lists/*
```

---

## ✅ 5. Use `.dockerignore`

Prevent large or unnecessary files from being added to the image.

### Example `.dockerignore`:

```
node_modules
.git
*.log
Dockerfile
README.md
```

---

## ✅ 6. Use Tools like `docker-slim`

* [`docker-slim`](https://github.com/docker-slim/docker-slim) analyzes and shrinks your image automatically.

```bash
docker-slim build myapp:latest
```

---

## ✅ 7. Avoid Installing Dev Dependencies

Use `NODE_ENV=production` or similar flags to skip development tools.

```dockerfile
ENV NODE_ENV=production
RUN npm install --only=production
```

---

## ✅ 8. Analyze Image Size

Use `dive` or `docker image inspect` to see what's taking up space.

```bash
# Install dive
brew install dive

# Analyze image
dive myapp:latest
```

---

## 🧠 Summary

| Tip                    | Result                       |
| ---------------------- | ---------------------------- |
| Use smaller base image | Reduces base size            |
| Clean cache/temp files | Avoids storage waste         |
| Use multi-stage builds | Removes build-time artifacts |
| Combine commands       | Fewer layers                 |
| Use `.dockerignore`    | Prevents unnecessary files   |
| Analyze and slim       | Optimize layers and contents |

> 🎯 Goal: Reduce size while preserving function and security.
