# 🐳 ENTRYPOINT in Docker

---

## 🔹 What is `ENTRYPOINT`?

The `ENTRYPOINT` instruction in a Dockerfile defines the **main command** that will always run when a container starts.

It is used to **set the default executable**, and unlike `CMD`, it is **not overridden** when arguments are passed to the container (unless explicitly done).

---

## 🧱 Syntax

There are **two forms**:

### 1️⃣ Exec Form (Preferred)
```dockerfile
ENTRYPOINT ["executable", "param1", "param2"]
```

- Does **not invoke a shell**.
- More predictable.
- Example:
```dockerfile
ENTRYPOINT ["/usr/bin/python3", "app.py"]
```

### 2️⃣ Shell Form
```dockerfile
ENTRYPOINT command param1 param2
```

- Runs using `/bin/sh -c`.
- Allows shell features (e.g., pipes, `&&`).
- Example:
```dockerfile
ENTRYPOINT python3 app.py
```

---

## 🆚 ENTRYPOINT vs CMD

| Aspect       | `ENTRYPOINT`                         | `CMD`                                |
|--------------|---------------------------------------|---------------------------------------|
| Purpose      | Main command to run                  | Default arguments for ENTRYPOINT or command |
| Overridable  | ❌ No (unless `--entrypoint` used)    | ✅ Yes (overridden by `docker run`)   |
| Combination  | Used with CMD as arguments            | Can be overridden entirely            |

### ✅ Using both together:
```dockerfile
ENTRYPOINT ["python3"]
CMD ["app.py"]
```

Then:
```bash
docker run myimage             # Runs: python3 app.py
docker run myimage script.py   # Runs: python3 script.py
```

---

## 🛠 Overriding ENTRYPOINT

You can override ENTRYPOINT at runtime:
```bash
docker run --entrypoint /bin/bash myimage
```

---

## 🧠 Best Practice

- Use **exec form ENTRYPOINT** for scripts or binaries.
- Use `CMD` for **default arguments** to the entrypoint.
- Create a wrapper script if you need to do setup before execution.

---

> ✅ `ENTRYPOINT` is essential when your container is meant to run a specific application or script every time it starts.
