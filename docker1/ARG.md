# 🧩 ARG in Docker

## What is `ARG`?

`ARG` is a Dockerfile instruction used to **define variables that are passed at build time**, not at runtime.

> 🔧 Think of `ARG` as a **build-time variable** — it's only available **while building** the image, not inside the running container.

---

## 🛠️ Syntax

```dockerfile
ARG variable_name[=default_value]


ARG in Docker
ARG is a Dockerfile instruction used to define variables that users can pass at build-time to the Docker image with the --build-arg flag.

Key Points:

ARG values are only available during the image build process.
Unlike ENV, they do not persist in the final image.
You can define a default value for an ARG.
Syntax
ARG <variable-name>[=<default-value>]
Example
Dockerfile:

# syntax=docker/dockerfile:1
FROM alpine

# Define a build-time argument with default value
ARG VERSION=1.0

# Use the argument in a command
RUN echo "Building version $VERSION"
Build the image with a custom version:

docker build --build-arg VERSION=2.5 -t myapp:2.5 .
Output:

Building version 2.5
If no build argument is passed, the default value 1.0 will be used.
