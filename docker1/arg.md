# 🐳 ARG in Docker

## 📘 What is `ARG`?

`ARG` is a Dockerfile instruction used to define **build-time variables**. These variables are available **only during the image build** process, and not inside the running container (unless passed into `ENV`).

---

## 🛠️ Syntax

```dockerfile
ARG <variable_name>[=<default_value>]
