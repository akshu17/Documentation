
# 🐳 What is a Docker Container?

A **Docker container** is a **lightweight, standalone, and executable package** that includes:

- Your application code
- All its dependencies (libraries, runtime, configs)
- The filesystem and environment it needs

Think of it as a **mini-computer running only your app**, isolated from everything else.

---

## 🧱 Key Concepts

| Feature         | Description                                           |
|-----------------|-------------------------------------------------------|
| 🧩 Isolated      | Runs in its own environment (CPU, memory, filesystem) |
| 🚀 Portable      | Runs the same on any system with Docker installed     |
| 🏃‍♂️ Fast         | Starts in milliseconds — no OS boot needed            |
| 🔁 Reproducible | Same container = same behavior every time             |

---

## ⚙️ How It Works

Containers run from **images**, which are built using a **Dockerfile**.  
The image includes everything your app needs. Once created, you **run** it to start a container.

```bash
docker build -t myapp .
docker run myapp
```

---

## 🗂️ Example: Running a Web Server

```bash
docker run -d -p 8080:80 nginx
```

This command:

- Starts a container from the `nginx` image
- Runs it in detached mode (`-d`)
- Maps port `80` in the container to `8080` on the host

Access it via: `http://localhost:8080`

---

## 🔍 What’s Inside a Container?

- OS filesystem (from base image)
- App code (copied during build)
- Environment variables
- Metadata and configuration

---

## 🧠 Summary

| Feature         | Docker Container                          |
|-----------------|--------------------------------------------|
| Runs            | From an image                              |
| Lightweight     | Uses host OS kernel, not a full VM         |
| Isolated        | Has its own process and network namespace  |
| Portable        | Same container runs on any OS w/ Docker    |
