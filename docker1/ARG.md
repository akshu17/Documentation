# 🧩 ARG in Docker

## What is `ARG`?

`ARG` is a Dockerfile instruction used to **define variables that are passed at build time**, not at runtime.

> 🔧 Think of `ARG` as a **build-time variable** — it's only available **while building** the image, not inside the running container.

---

## 🛠️ Syntax

```dockerfile
ARG variable_name[=default_value]
