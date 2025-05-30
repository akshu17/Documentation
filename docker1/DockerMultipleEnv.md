# Using Docker for Multiple Environments

Great question! Using Docker for multiple environments (like development, testing, staging, and production) is a very common scenario. The idea is to keep your Docker setup flexible so you can easily switch or customize configurations for each environment without duplicating too much code.

---

## 1. Use Multiple Docker Compose Files

You typically have a **base `docker-compose.yml`** file with common service definitions, and then **override files** for each environment:

- `docker-compose.yml` — base configuration  
- `docker-compose.override.yml` — local development overrides (Docker Compose uses this by default)  
- `docker-compose.prod.yml` — production-specific overrides  
- `docker-compose.test.yml` — test environment overrides  

### Example

`docker-compose.yml`
```yaml
version: '3.8'

services:
  app:
    image: myapp:latest
    environment:
      - ENV=development
    ports:
      - "8080:8080"
    volumes:
      - .:/app
```

