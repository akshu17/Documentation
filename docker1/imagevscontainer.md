
# Difference Between Docker Image and Container

## 🆚 Docker Image vs Container

| Feature           | **Docker Image**                                         | **Docker Container**                                     |
|-------------------|----------------------------------------------------------|-----------------------------------------------------------|
| **Definition**     | A **blueprint/template** for creating containers.        | A **running instance** of an image.                       |
| **State**          | **Static** – does not change.                            | **Dynamic** – can change during execution.                |
| **Persistence**    | **Immutable** – cannot be modified once built.           | Can be modified during runtime (temporary changes).       |
| **Use Case**       | Used to **create containers**.                           | Used to **run applications** in isolation.                |
| **Storage**        | Stored as layers on disk.                                | Lives in memory while running, unless persisted.          |
| **Examples**       | `python:3.11`, `nginx`, `ubuntu:latest`                 | A running app based on `python:3.11` image.               |
| **Analogy**        | Think of it as a **recipe or template**.                | Think of it as a **meal prepared from the recipe**.       |

---

## 🧠 Summary

- A **Docker image** is like a *frozen snapshot* of your application and its environment.
- A **Docker container** is a *live, running instance* created from that image.
