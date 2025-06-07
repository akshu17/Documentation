# ARG in Docker

## 🔹 What is `ARG`?

`ARG` is a Dockerfile instruction used to define **build-time variables**. These variables can be passed to the Docker build process using the `--build-arg` flag and are available **only during the image build**, not in the running container.

---

## 🧠 Key Points

| Feature             | Details                                           |
|---------------------|---------------------------------------------------|
| Scope               | Build-time only (not available after container starts) |
| Default Value       | Can be set in the Dockerfile                     |
| Overridable         | Yes, via `--build-arg` during `docker build`     |
| Visibility          | Not visible inside the container after build     |

---

## 🧪 Example 1

### Dockerfile

```dockerfile
# Define build-time argument
ARG VERSION=1.0

# Use the ARG
FROM ubuntu:${VERSION}

RUN echo "Building with Ubuntu version: ${VERSION}"
