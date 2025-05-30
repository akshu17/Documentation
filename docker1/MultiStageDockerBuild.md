

# What is Multi-stage Docker Build?

A **multi-stage Docker build** is a technique used to create **smaller, optimized Docker images** by using multiple intermediate build stages within a single Dockerfile. Instead of creating a large image with all the build tools and dependencies, multi-stage builds allow you to separate the build environment from the final runtime environment.

---

## Why Use Multi-stage Builds?

- **Reduce image size:** Only the final artifacts needed to run the app are included.
- **Improve security:** Build tools and sensitive files don’t get shipped in the final image.
- **Simplify Dockerfiles:** One Dockerfile can handle both build and production stages.
- **Better caching:** Each stage can cache layers efficiently, speeding up builds.

---

## How Does It Work?

A multi-stage build uses multiple `FROM` statements in a single Dockerfile. Each `FROM` starts a new build stage.

- The **first stage(s)** build the application.
- The **last stage** is the runtime environment that copies only the necessary files from previous stages.

---

## Example Explained

Suppose you want to build a Go application.

```dockerfile
# Stage 1: Build the Go binary
FROM golang:1.20 AS builder
WORKDIR /app
COPY . .
RUN go build -o myapp

# Stage 2: Create a lightweight image with only the binary
FROM alpine:latest
WORKDIR /app
COPY --from=builder /app/myapp .
CMD ["./myapp"]
```

- **Stage 1 (`builder`):** Uses the official Go image to compile the Go program.
- **Stage 2:** Starts a fresh, minimal Alpine Linux image and copies only the compiled binary from the builder stage.
- The final image is very small because it does not include the Go compiler or source code.

---

## Benefits in Detail

| Benefit                    | Description                                                                                  |
|----------------------------|----------------------------------------------------------------------------------------------|
| **Smaller images**         | By excluding build tools and unnecessary files, the image size can be dramatically reduced. |
| **Faster deployment**      | Smaller images mean faster transfer times and quicker container startup.                    |
| **Security improvements**  | Fewer tools and files reduce the attack surface inside the container.                       |
| **Cleaner Dockerfiles**    | Manage build and runtime stages clearly in one file.                                        |
| **Reusability**            | Use build stages for multiple steps, like compiling, testing, and packaging.                |

---

## When to Use Multi-stage Builds?

- Compiling code (Go, Java, C++, etc.)
- Building frontend assets (React, Angular, Vue)
- Creating optimized images without build dependencies
- Complex applications needing multiple build steps

---

## Summary

Multi-stage Docker builds enable you to **create clean, small, and secure images** by splitting the build and runtime environments inside a single Dockerfile. It’s a powerful way to optimize your Docker workflows and production images.

---

> 💡 **Quote:**  
> *“Multi-stage builds are the future of efficient container images — build once, ship slim, run fast.”*
