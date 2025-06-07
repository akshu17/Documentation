
# Docker Interview Questions and Detailed Answers

---

### 1. What is Entrypoint in Docker?

**Answer:**

`ENTRYPOINT` specifies the main command that will always run when a container starts. It defines the executable to be run.

Example:

```Dockerfile
ENTRYPOINT ["python3", "app.py"]
```

---

### 2. CMD vs ENTRYPOINT?

| Aspect         | CMD                                   | ENTRYPOINT                              |
|----------------|-------------------------------------|---------------------------------------|
| Purpose        | Default command or parameters        | Fixed executable for the container    |
| Overridable    | Yes, can be overridden by arguments  | No, runtime args appended to entrypoint|
| Form           | Shell or exec form                   | Exec form recommended                  |
| Use Case       | Provide default parameters           | Define container’s main command        |

Example:

```Dockerfile
ENTRYPOINT ["echo"]
CMD ["Hello World"]
```

Running container prints "Hello World".

---

### 3. ADD vs COPY?

- `COPY` copies files/folders from the build context to the image.

- `ADD` does the same but can also fetch from URLs and auto-extract compressed files.

Prefer `COPY` unless you need `ADD` features.

---

### 4. Press CTRL+C during `docker build -t`?

The build process is aborted immediately. Partial layers remain cached for faster future builds.

---

### 5. Dockerfile size is 2GB; how to reduce?

- Use slim or alpine base images.

- Combine RUN instructions.

- Clean up package caches.

- Use multi-stage builds.

---

### 6. Difference between layers and image?

- **Layers:** Intermediate filesystems created at each Dockerfile instruction.

- **Image:** Stack of layers making a runnable filesystem.

---

### 7. Multiple ENTRYPOINTs?

Only the last ENTRYPOINT in Dockerfile is used; previous ones are overwritten.

---

### 8. Default user for containers?

By default, containers run as `root` user.

---

### 9. Docker socket?

Unix socket `/var/run/docker.sock` that allows Docker CLI to communicate with Docker daemon.

---

### 10. Container runtime?

Software like `runc` that creates and runs containers per OCI specifications.

---

### 11. Mount filesystem in container?

```bash
docker run -v /host/path:/container/path image
```

---

### 12. Write Dockerfile and push to DockerHub

```Dockerfile
FROM python:3.9-slim
WORKDIR /app
COPY app.py .
CMD ["python", "app.py"]
```

Build and push:

```bash
docker build -t username/myapp:latest .
docker login
docker push username/myapp:latest
```

---

### 13. Dockerfile structure

- FROM

- WORKDIR

- COPY/ADD

- RUN

- ENV

- EXPOSE

- CMD/ENTRYPOINT

- USER

---

### 14. Multi-stage Dockerfile example

```Dockerfile
FROM golang:1.18 AS builder
WORKDIR /app
COPY . .
RUN go build -o myapp

FROM alpine
COPY --from=builder /app/myapp /usr/local/bin/myapp
ENTRYPOINT ["myapp"]
```

---

### 15. Dockerfile to install Java

```Dockerfile
FROM openjdk:17-jdk
WORKDIR /app
COPY . .
CMD ["java", "-jar", "myapp.jar"]
```

---

### 16. FROM command

Defines the base image. Must be the first instruction.

---

### 17. Publish & Expose

- `EXPOSE` declares ports container listens on.

- `docker run -p hostPort:containerPort` publishes ports to host.

---

### 18. Command to publish & expose ports

```bash
docker run -p 8080:80 image
```

---

### 19. Docker container?

Running instance of an image with isolated filesystem.

---

### 20. Difference between CMD and RUN?

- `RUN` executes commands during image build.

- `CMD` specifies the command to run at container start.

---

### 21. Difference between CMD and RUN

As above.

---

### 22. Collect logs if container stopped without volume?

Use:

```bash
docker logs <container_id>
```

---

### 23. Security measures for Docker images?

- Minimal base images.

- Avoid root user.

- Scan images regularly.

- Use trusted images.

- Enable Docker Content Trust.

---

### 24. Image scanning tools?

- Trivy

- Clair

- Anchore

---

### 25. Docker Swarm?

Docker’s native orchestration tool.

---

### 26. Dockerfile?

See above.

---

### 27. ENTRYPOINT and CMD?

See question 2.

---

### 28. Dockerfile?

Repeated.

---

### 29. Create image from Dockerfile?

```bash
docker build -t imagename:tag .
```

---

### 30. Difference image vs container?

- Image: Template.

- Container: Running instance with writable layer.

---

### 31. Namespace and cgroup?

- Namespace: Isolation of processes, network, etc.

- cgroup: Resource limiting.

---

### 32. Deliver custom container to others?

- Push to registry.

- Or use `docker save` and `docker load`.

---

### 33. Where store Docker images in project?

Images stored in registries.

---

### 34. What is DTR?

Docker Trusted Registry - private, secure Docker image registry.

---

### 35. Dockerfile with commands explained

```Dockerfile
FROM ubuntu:20.04
LABEL maintainer="you@example.com"
ENV APP_HOME=/app
WORKDIR $APP_HOME
COPY . .
RUN apt-get update && apt-get install -y curl
EXPOSE 80
CMD ["./start.sh"]
```

---

### 36. Dockerfile versioning?

Use image tags to version images.

---

### 37. Dockerfile structure?

Repeated.

---

### 38. Multi-stage Dockerfile?

Repeated.

---

### 39. Dockerfile to install Java?

Repeated.

---

### 40. FROM command?

Repeated.

---

### 41. Publish & Expose?

Repeated.

---

### 42. Command to publish & expose?

Repeated.

---

### 43. Docker container?

Repeated.

---

### 44. Docker multiple stage build?

Use multi `FROM` for build efficiency.

---

### 45. Troubleshooting commands?

```bash
docker logs <container_id>
docker exec -it <container_id> /bin/bash
docker inspect <container_id>
docker stats <container_id>
```

---

### 46. Docker Swarm?

Cluster orchestration tool.

---

### 47. Docker Compose?

Tool to run multi-container apps.

---

### 48. Maintain Docker & K8s in production?

CI/CD, monitoring, secrets, scaling.

---

### 49. Docker vs Kubernetes?

| Docker        | Kubernetes                  |
|---------------|-----------------------------|
| Container runtime | Container orchestration  |
| Single node   | Multi-node clusters          |

---

### 50. Best practices for Dockerfile?

Small images, multi-stage builds, .dockerignore, least privilege.

---

### 51. Scan images for vulnerabilities?

Use Trivy, Clair integrated in pipelines.

---

### 52. Docker layers; top layer is read-write?

Yes, container adds writable layer on top of image layers.

---

### 53. Docker concepts used?

Volumes, networks, multi-stage builds.

---

### 54. Where to fit Docker concepts? Network usage?

Depends on use case; bridge, host, or overlay networks.

---

### 55. CMD vs ENTRYPOINT?

See Q2.

---

### 56. COPY vs ADD?

See Q3.

---

### 57. Common Docker image issues?

Large images, cache issues, permissions, missing deps.

---

### 58. Container crash after `docker run -p`?

Check logs, port conflicts, Dockerfile commands.

---

### 59. Java container restart issues?

Check CMD/ENTRYPOINT syntax; use exec form.

---

### 60. Vanilla docker machine but container not up?

Check logs, network, volumes, resource limits.

---

### 61. Client wants custom registry, no Docker Hub?

Use private Docker Registry or DTR with access control.

---

### 62. Copy Docker image between machines?

Use:

```bash
docker save image | ssh user@host docker load
```

---

### 63. VM vs Docker?

VMs run full OS; Docker uses containers sharing OS kernel, lightweight.

---

### 64. Why not use AWS AMI instead of Docker Image?

AMI is a VM image; Docker images are lightweight, portable containers.

---

### 65. Dockerfile directives and ENTRYPOINT scenarios?

Use ENTRYPOINT for main command, CMD for default args.

---

### 66. Dockerfile size 2GB reduction?

Use minimal base, combine RUN, multi-stage builds.

---

### 67. Layers vs image?

See Q6.

---

### 68. Multiple ENTRYPOINTs?

Last one applies.

---

### 69. Default user in container?

Root.

---

### 70. Dockerfile structure?

Repeated.

---

### 71. Docker networks?

bridge, host, overlay, macvlan.

---

### 72. Attach volume command?

```bash
docker run -v host_path:container_path image
```

---

### 73. Basic container command?

```bash
docker run -it ubuntu /bin/bash
```

---

### 74. Use of `docker ps`?

List running containers.

---

### 75. Kubernetes vs Docker Swarm?

K8s more powerful orchestration; Swarm simpler.

---

### 76. Services in Docker Swarm?

Replicated services, global services.

---

### 77. Applications with Docker?

Java, Python, Node.js etc.

---

### 78. What’s Dockerfile?

Text file with build instructions.

---

### 79. CMD vs ENTRYPOINT?

See Q2.

---

### 80. Docker port mapping?

Map container port to host.

---

### 81. What’s `-p`?

Flag to publish ports.

---

### 82. Dockerfile?

Repeated.

---

### 83. Docker networking, commands, troubleshooting?

Use commands: `docker network`, `docker inspect`, `docker logs`.

---

### 84. Stateful and stateless containers?

- Stateful stores data; stateless does not.

---

### 85. Difference between them?

Stateful maintains data; stateless ephemeral.

---

### 86. Use case?

Databases (stateful), web servers (stateless).

---

### 87. Run app in Dockerfile?

Use ENTRYPOINT or CMD for app start.

---

### 88. What is containerization?

Packaging apps with dependencies into isolated containers.

---

### 89. Root permission in Dockerfile?

Use:

```Dockerfile
USER root
```

---

### 90. Dockerfile explain commands?

(See previous explanations)

---

### 91. Docker commands?

`docker build`, `docker run`, `docker ps`, `docker logs`, `docker exec`.

---

### 92. Make application accessible externally?

Publish ports with `-p`.

---

### 93. Write multistage Dockerfile?

(See Q14)

---

### 94. Diff between CMD and ENTRYPOINT?

See Q2.

---

### 95. Find background processes in container?

```bash
docker exec -it <container_id> ps aux
```

---

### 96. What is Docker Swarm & Compose?

- Swarm: Orchestration.

- Compose: Multi-container app management.

---

### 97. Applications running in your Docker containers?

Depends on use case (web, db, etc.)

---

### 98. ENTRYPOINT and CMD?

See Q2.

---

### 99. Write Dockerfile?

(See above examples)

---

# End of Document
