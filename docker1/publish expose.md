
# 🌐 Docker `EXPOSE` vs Publishing Ports

Understanding the difference between the `EXPOSE` instruction in a Dockerfile and publishing a port using the `docker run` command is crucial for networking in Docker.

---

## 🔓 `EXPOSE` — Documentation Only

The `EXPOSE` instruction in a `Dockerfile`:

- **Documents** that the container listens on a specific port
- **Does NOT publish** the port to the host
- Is mainly **for informational purposes**

### Example

```dockerfile
EXPOSE 3000
```

🧠 This means: “The app inside the container listens on port 3000.”

But this port won’t be accessible from outside unless you explicitly **publish** it when running the container.

---

## 🌐 Publishing a Port

To actually make a container’s port accessible from your host machine, use:

```bash
docker run -p 8080:3000 my-app
```

### Breakdown

- `3000`: port **inside** the container
- `8080`: port **on the host**
- This maps `localhost:8080` to container port `3000`

---

## 🧠 Summary Table

| Concept      | Dockerfile Example | Runtime Flag | Purpose                          |
|--------------|---------------------|--------------|----------------------------------|
| `EXPOSE`     | `EXPOSE 3000`       | ❌            | Informational/documentation only |
| Publish Port | ❌                  | `-p 8080:3000`| Maps container port to host port |

---

## ✅ Best Practice

Use both:

- Include `EXPOSE` in your `Dockerfile` for documentation and tooling (e.g., Docker Compose)
- Use `-p` when running the container to access it from outside

---

Let me know if you'd like a visual diagram or Docker Compose example too!
