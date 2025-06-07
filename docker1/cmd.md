
# Docker CMD vs ENTRYPOINT

In the context of **Docker**, both `CMD` and `ENTRYPOINT` are instructions used in a Dockerfile to specify the command that should run when a container starts. However, they serve slightly different purposes and behave differently.

---

## 🔹 CMD — *Default Command*

### **Definition:**
The `CMD` instruction provides **default arguments** for the container's execution. It can be overridden by arguments passed when running the container with `docker run`.

### **Syntax:**
```dockerfile
CMD ["executable", "param1", "param2"]  # exec form (preferred)
CMD command param1 param2               # shell form
```

### **Example:**
```dockerfile
FROM node:20
WORKDIR /app
COPY . .
CMD ["node", "app.js"]
```

If you run:
```bash
docker run mynodeapp
```
It runs: `node app.js`.

But if you run:
```bash
docker run mynodeapp node other.js
```
It overrides `CMD` and runs `node other.js`.

---

## 🔹 ENTRYPOINT — *Fixed Command*

### **Definition:**
The `ENTRYPOINT` instruction sets the **main command** to run in the container. Unlike `CMD`, it is **not overridden** by `docker run` arguments (those are passed as arguments to `ENTRYPOINT`).

### **Syntax:**
```dockerfile
ENTRYPOINT ["executable", "param1", "param2"]  # exec form (preferred)
ENTRYPOINT command param1 param2               # shell form
```

### **Example:**
```dockerfile
FROM ubuntu
ENTRYPOINT ["echo", "Hello"]
```

If you run:
```bash
docker run myubuntu World
```

It runs:
```bash
echo Hello World
```

You **can’t override `ENTRYPOINT`** the same way as `CMD`, unless you use the `--entrypoint` flag.

---

## 🔀 Difference Between CMD and ENTRYPOINT

| Feature             | `CMD`                                | `ENTRYPOINT`                           |
|---------------------|----------------------------------------|-----------------------------------------|
| Purpose             | Default command/arguments              | Fixed main command                      |
| Overridable         | Yes, via `docker run` args             | No, unless `--entrypoint` is used       |
| Use case            | Provide defaults that can be changed   | Set a command that always runs          |
| Combination         | Can be used with `ENTRYPOINT` to pass default args | Receives args from `CMD` or `docker run` |

---

## 🔧 Using CMD + ENTRYPOINT Together

```dockerfile
FROM ubuntu
ENTRYPOINT ["echo"]
CMD ["Hello World"]
```

If you run:
```bash
docker run myimage
```

It executes:
```bash
echo Hello World
```

If you run:
```bash
docker run myimage Goodbye
```

It executes:
```bash
echo Goodbye
```

---

## ✅ Best Practice

- Use `ENTRYPOINT` to define the **main behavior**.
- Use `CMD` to provide **default arguments**.
