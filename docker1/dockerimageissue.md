
# 🐳 Common Docker Image Issues

## 1. 🐘 Large Image Size
**Symptoms:**
- Slow builds and deployments
- Long container startup times

**Fixes:**
- Use smaller base images (`alpine`, `distroless`)
- Clean up build tools after use
- Use `.dockerignore` to exclude unnecessary files

---

## 2. 🛑 Using `latest` Tag
**Symptoms:**
- Unexpected behavior when base image updates
- Hard to reproduce builds

**Fixes:**
- Always pin versions (`python:3.10-slim`)
- Use semantic versioning for your own images (`myapp:1.0.2`)

---

## 3. 🔐 Running as Root User
**Symptoms:**
- Security risks
- Denied access in secure environments

**Fixes:**
- Add and switch to a non-root user in Dockerfile:
```dockerfile
RUN adduser -D appuser
USER appuser
```

---

## 4. 🔄 Not Using Multi-Stage Builds
**Symptoms:**
- Image contains unnecessary build tools, tests, docs
- Large final image size

**Fixes:**
- Use multi-stage builds to separate build and runtime environments

---

## 5. 💣 Build Fails Due to Caching Issues
**Symptoms:**
- Incorrect dependencies
- Old code used during build

**Fixes:**
- Clear cache: `docker builder prune`
- Copy dependency files first, then app source to leverage caching:
```dockerfile
COPY package*.json ./
RUN npm install
COPY . .
```

---

## 6. 🕵️‍♂️ Image Has Known Vulnerabilities
**Symptoms:**
- Fails security scans
- Insecure packages in use

**Fixes:**
- Use tools like `Trivy`, `Grype`, `Docker Scout` to scan and fix vulnerabilities
- Use minimal, frequently updated base images

---

## 7. 🔥 Application Fails to Start
**Symptoms:**
- Container exits immediately
- Logs show config/env errors

**Fixes:**
- Check `CMD` and `ENTRYPOINT` usage
- Ensure dependencies (env vars, ports, volumes) are set
- Use `docker logs <container>` to debug

---

## 8. 🔄 Improper Layer Caching
**Symptoms:**
- Long build times even for small changes

**Fixes:**
- Reorder `COPY` and `RUN` commands in Dockerfile to optimize cache usage

---

## 9. 🧪 Missing `.dockerignore` File
**Symptoms:**
- Large context sent to daemon
- Sensitive or unnecessary files in image

**Fixes:**
- Create a `.dockerignore` file to exclude:
```
.git
node_modules
*.md
tests/
```

---

## 10. 🚫 Incorrect File Permissions
**Symptoms:**
- App can't read/write files
- Permission denied errors

**Fixes:**
- Set correct ownership/permissions in Dockerfile:
```dockerfile
RUN chown -R appuser:appuser /app
```
