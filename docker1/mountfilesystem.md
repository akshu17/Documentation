
# 🗂️ What is a Mount (Filesystem) in a Container?

A **mount** in Docker means attaching a **filesystem location** (from the host or a volume) into a **specific path inside a container**.

This allows the container to **read and/or write** files **outside of its image**, enabling data persistence, sharing, or configuration injection.

---

## 📦 Why Use Mounts?

By default, a container's filesystem is:
- **Ephemeral**: destroyed when the container is deleted
- **Isolated**: can’t access the host or other containers’ data

Mounts solve this by giving access to:
- **Host directories** (bind mounts)
- **Named volumes** (managed by Docker)
- **Temporary filesystems** (like tmpfs)

---

## 🧱 Types of Mounts

| Type         | Description |
|--------------|-------------|
| **Bind Mount** | Mount a **host directory or file** into the container |
| **Volume**      | Use a **Docker-managed** persistent volume |
| **tmpfs**       | Mount a **temporary** filesystem in memory (Linux only) |

---

## 🔧 Example: Bind Mount

```bash
docker run -v /host/data:/container/data ubuntu
```

- Mounts the host’s `/host/data` directory into `/container/data` in the container.
- Changes made inside the container will reflect on the host, and vice versa.

---

## 🔧 Example: Named Volume

```bash
docker volume create mydata
docker run -v mydata:/app/data ubuntu
```

- `mydata` is managed by Docker.
- Stored under `/var/lib/docker/volumes/` on the host (abstracted from you).
- Great for **data persistence** across container restarts.

---

## 🔧 Example: tmpfs Mount (in-memory only)

```bash
docker run --tmpfs /app/cache:rw,size=100m ubuntu
```

- Mounts `/app/cache` as an in-memory filesystem (never hits disk).
- Good for **fast, temporary data** that shouldn’t persist.

---

## 🛑 Mount ≠ COPY

- `COPY` puts a file **inside the image** at build time.
- A mount provides **live access** to host or volume data at **run time**.

---

## ✅ Summary

| Mount Type   | Use Case                     | Persistent? | Example |
|--------------|-------------------------------|-------------|---------|
| Bind mount   | Share code or configs         | ✅ Yes       | `-v /host:/container` |
| Volume       | Persist container data safely | ✅ Yes       | `-v myvol:/app` |
| tmpfs        | Temp, fast access (no disk)   | ❌ No        | `--tmpfs /app` |

---

Let me know if you want a visual or real project example using mounts!
