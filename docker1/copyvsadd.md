# 📦 Dockerfile: `ADD` vs `COPY`

Both `ADD` and `COPY` are Dockerfile instructions used to copy files and directories into a Docker image. However, they have **different capabilities** and **recommended use cases**.

---

## 🔹 `COPY`

- Copies **files and directories** from the **host** into the **Docker image**.
- **Simple and predictable**.
- Recommended for most use cases.

### ✅ Example:
```dockerfile
COPY ./app /usr/src/app
```

---

## 🔸 `ADD`

- Has all the features of `COPY`, **plus extra capabilities**:
  - Can **automatically extract** local `.tar`, `.tar.gz`, `.zip` files.
  - Can fetch files from **remote URLs** (not recommended).
- More **powerful**, but less predictable.

### ✅ Example:
```dockerfile
ADD ./archive.tar.gz /app/       # Extracts archive into /app
ADD https://example.com/file /tmp/file  # Downloads file
```

---

## ⚖️ Summary Table

| Feature                  | `COPY`        | `ADD`           |
|--------------------------|---------------|-----------------|
| Local file copy          | ✅ Yes         | ✅ Yes          |
| Remote URL support       | ❌ No          | ✅ Yes (not best practice) |
| Auto extract archives    | ❌ No          | ✅ Yes          |
| Simplicity               | ✅ Very simple | ❌ More complex |
| Best for                 | Local assets  | Archives or remote files (sparingly) |

---

## 🧠 Best Practice

> ✅ Use `COPY` for all straightforward file copying.  
> 🚫 Only use `ADD` when you **need** its archive extraction or remote-fetch capabilities.

---

## 💡 Tip

You can manually extract archives using `COPY` + `RUN`:

```dockerfile
COPY archive.tar.gz /tmp/
RUN tar -xzf /tmp/archive.tar.gz -C /app/
```

This approach is more explicit and often preferred in production Dockerfiles.

