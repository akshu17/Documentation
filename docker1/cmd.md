# 🧩 CMD in Docker

## What is `CMD`?

The `CMD` instruction in a Dockerfile **specifies the default command** that should be run when a container is started from the image.

> 📝 If you run a container **without providing a command**, Docker will use the `CMD`.

---

## 🛠️ Syntax

Docker supports two forms of `CMD`:

### 1. **Exec form** (recommended)
```dockerfile
CMD ["executable", "param1", "param2"]
