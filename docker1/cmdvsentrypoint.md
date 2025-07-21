# 🐳 CMD vs ENTRYPOINT in Docker

Both `CMD` and `ENTRYPOINT` are Dockerfile instructions used to define what **command** should run in a Docker container — but they behave differently.

---

## 🔸 CMD

- Provides **default arguments** to the container.
- Can be **overridden** at runtime using `docker run` command arguments.
- Used when you want the container to have **optional behavior**.

### ✅ Example:
```dockerfile
FROM ubuntu
CMD ["echo", "Hello from CMD"]
```

```bash
docker run myimage              # Outputs: Hello from CMD
docker run myimage "Hi there!" # Outputs: Hi there!
```

---

## 🔹 ENTRYPOINT

- Defines the **main command** to run.
- Is **not overridden** by command-line arguments (unless using `--entrypoint`).
- Used when your container should **always run a specific program**.

### ✅ Example:
```dockerfile
FROM ubuntu
ENTRYPOINT ["echo", "Hello from ENTRYPOINT"]
```

```bash
docker run myimage              # Outputs: Hello from ENTRYPOINT
docker run myimage "Extra arg" # Outputs: Hello from ENTRYPOINT Extra arg
```

---

## 🔁 CMD + ENTRYPOINT Together

- `CMD` provides **default arguments**.
- `ENTRYPOINT` defines the **fixed executable**.

### ✅ Example:
```dockerfile
ENTRYPOINT ["echo"]
CMD ["Hello from CMD"]
```

```bash
docker run myimage             # Outputs: Hello from CMD
docker run myimage "Hi!"       # Outputs: Hi!
```

---

## ⚖️ Summary Table

| Feature            | `CMD`                          | `ENTRYPOINT`                       |
|--------------------|--------------------------------|------------------------------------|
| Purpose            | Default arguments              | Main command to run                |
| Overridable        | ✅ Yes (via `docker run`)      | ❌ No (unless `--entrypoint` used) |
| Typical Usage      | Optional defaults              | Fixed behavior like app execution  |
| Can be combined?   | ✅ Yes                         | ✅ Yes                             |
| Shell Form Support | Yes                            | Yes                                |

---

> ✅ Use `ENTRYPOINT` when your container is designed to always run the same program.
>  
> ✅ Use `CMD` when you want to allow customization at runtime or set defaults.

