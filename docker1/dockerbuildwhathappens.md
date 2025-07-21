# ⛔ What Happens When You Press `CTRL+C` During `docker build`?

When you run:

```bash
docker build -t myimage .
```

...and press `CTRL+C` during the build process, the following happens:

---

## 🔹 1. Build Process is Interrupted

- `CTRL+C` sends a `SIGINT` (interrupt) signal to the Docker CLI.
- The Docker **client** interrupts the build process.
- The **Docker daemon** stops the ongoing image build.

---

## 🔹 2. Partial Layers May Be Cached

- Any completed layers **before** the interruption are usually **cached**.
- If you re-run the build, Docker may **reuse** those previously built layers, unless you change the Dockerfile or files involved.

---

## 🔹 3. No Final Image is Created

- If the build was not completed, the final image **won’t exist**.
- You can verify with:

```bash
docker images
```

If the image is missing or has no tag, the build was incomplete.

---

## 🔹 4. Temporary Containers Are Cleaned Up

- Docker creates temporary intermediate containers during build.
- On interruption, these **are usually cleaned up automatically**.
- You can check with:

```bash
docker ps -a
```

To see if any were left behind (they usually are not).

---

## 🔸 Example Scenario

If your Dockerfile has multiple steps:

```dockerfile
FROM ubuntu
RUN apt update
RUN apt install -y nginx
COPY . /app


And you press `CTRL+C` during `apt install`, the previous `apt update` layer might still be cached.

Rebuilding will start from the `RUN apt install` step.

---

## 🧠 Tip

If you want to force a clean rebuild after interruption:

```bash
docker builder prune
```

Or add `--no-cache` to rebuild everything:

```bash
docker build --no-cache -t myimage .
```

---

> ✅ `CTRL+C` cancels the build safely, but you may still have cached layers unless explicitly removed.
what
