
# Docker Restart Policy

Docker provides **restart policies** to manage the behavior of containers when they exit or when Docker itself restarts. These policies help ensure that important containers stay up and running under various conditions.

---

## 🔁 What Is a Restart Policy?

A **restart policy** tells Docker how to handle a container after it stops running. This is useful for automatically recovering from failures, maintaining high availability, or simply reducing manual intervention.

---

## 📋 Available Restart Policies

### 1. `no` *(default)*

- **Description:** Docker will not attempt to restart the container if it stops or crashes.
- **Use Case:** Best for short-lived containers or development/testing environments.
- **Example:**
  ```bash
  docker run --restart=no my-container
  ```

---

### 2. `on-failure[:max-retries]`

- **Description:** Docker will restart the container **only if it exits with a non-zero (error) exit status**.
- **Optional Parameter:** You can specify how many times Docker should retry restarting (`max-retries`).
- **Use Case:** Useful for tasks that may fail occasionally but should not retry endlessly.
- **Example:**
  ```bash
  docker run --restart=on-failure:5 my-container
  ```
  This will restart the container up to 5 times on failure.

---

### 3. `always`

- **Description:** Docker will **always restart** the container if it stops, regardless of the exit code.
- **Note:** The container will also restart on Docker daemon restarts or host reboots.
- **Use Case:** Recommended for critical services that must always run.
- **Example:**
  ```bash
  docker run --restart=always my-container
  ```

---

### 4. `unless-stopped`

- **Description:** Like `always`, Docker restarts the container if it stops. **But it won’t restart if you manually stop the container** (e.g., via `docker stop`).
- **Use Case:** Good for persistent containers that should auto-restart unless stopped manually.
- **Example:**
  ```bash
  docker run --restart=unless-stopped my-container
  ```

---

## 🧠 Summary Table

| Policy            | Restarts on Failure | Restarts on Docker/Host Restart | Restarts on Manual Stop | Notes                                |
|-------------------|---------------------|----------------------------------|--------------------------|--------------------------------------|
| `no`              | ❌                  | ❌                               | ❌                       | Default policy                       |
| `on-failure`      | ✅                  | ❌                               | ❌                       | Optional retry count available       |
| `always`          | ✅                  | ✅                               | ✅                       | Ideal for production-critical apps   |
| `unless-stopped`  | ✅                  | ✅                               | ❌                       | Won’t restart if manually stopped    |

---

## 💡 Real-World Example

Run an Nginx server that should always be up:

```bash
docker run -d --restart=always nginx
```

This ensures the Nginx container restarts automatically, even after a crash or host reboot.

---

## 📝 Tips

- Restart policies apply only when using `docker run`. If you use Docker Compose, use the `restart:` option in your `docker-compose.yml`.
- Containers with `always` or `unless-stopped` policies will restart on daemon or host reboot automatically.

---

## ✅ Best Practices

- Use `always` for long-running production services.
- Use `on-failure` for batch jobs or temporary services with limited retries.
- Avoid `no` unless you’re managing restarts manually or during development/testing.

---
