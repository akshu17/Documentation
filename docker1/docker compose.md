
# Docker Compose

**Docker Compose** is a tool for defining and running multi-container Docker applications. Instead of running each container manually with `docker run`, you can define them all in a simple **YAML file** (`docker-compose.yml`) and run everything with a single command.

---

## ✅ Key Features

- Define services, networks, and volumes in one file.
- Easily scale services (e.g., multiple instances of a web app).
- Useful for local development and testing environments.
- Compatible with Docker Swarm (for orchestration).

---

## 📄 Basic Example: `docker-compose.yml`

```yaml
version: "3.8"

services:
  web:
    image: nginx
    ports:
      - "8080:80"

  app:
    build: .
    ports:
      - "5000:5000"
    volumes:
      - .:/app
    depends_on:
      - db

  db:
    image: postgres
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: pass
      POSTGRES_DB: example
```

---

## 🛠 Common Commands

| Command | Description |
|--------|-------------|
| `docker-compose up` | Starts all services. |
| `docker-compose up -d` | Starts in detached mode (background). |
| `docker-compose down` | Stops and removes all services. |
| `docker-compose build` | Builds the services defined in the Compose file. |
| `docker-compose logs` | Shows logs from services. |
| `docker-compose ps` | Lists running services. |

---

## 📌 When to Use Docker Compose

- Local development with multiple services (e.g., web + DB + cache).
- CI/CD pipelines to spin up temporary environments.
- Testing microservices locally.
