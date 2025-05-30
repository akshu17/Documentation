# How do you use docker for multiple environments?
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

`docker-compose.prod.yml`
```yaml
version: '3.8'

services:
  app:
    environment:
      - ENV=production
    ports:
      - "80:8080"
    volumes: []
```

**Run for development (default):**
```bash
docker-compose up
```

**Run for production:**
```bash
docker-compose -f docker-compose.yml -f docker-compose.prod.yml up -d
```

This way, the prod file overrides or adds specific settings for production.

---

## 2. Use Environment Variables (.env files)

Docker Compose supports loading environment variables from a `.env` file in the same directory.

You can have multiple `.env` files:

- `.env.dev`
- `.env.prod`
- `.env.test`

Then you specify which one to load when running:

```bash
ENV_FILE=.env.prod docker-compose --env-file $ENV_FILE up -d
```

Inside your `docker-compose.yml`, use variables:

```yaml
services:
  app:
    environment:
      - NODE_ENV=${NODE_ENV}
      - DB_HOST=${DB_HOST}
```

Your `.env.prod` might have:

```
NODE_ENV=production
DB_HOST=prod-db.example.com
```

Your `.env.dev` might have:

```
NODE_ENV=development
DB_HOST=localhost
```

---

## 3. Use Different Dockerfiles (Optional)

If your build process changes per environment, you can have multiple Dockerfiles like:

- `Dockerfile.dev`
- `Dockerfile.prod`

And specify which to use during build:

```bash
docker build -f Dockerfile.prod -t myapp:prod .
```

Then update your `docker-compose.prod.yml` to use the correct image or build args.

---

## 4. Summary of Best Practices

- Keep common config in `docker-compose.yml`
- Use override compose files per environment
- Use `.env` files for environment-specific variables
- Consider separate Dockerfiles if build steps vary
- Use scripts or Makefiles to automate environment-specific commands

---

**Bonus:** Sample command to run production setup with a specific `.env` file:

```bash
docker-compose --env-file .env.prod -f docker-compose.yml -f docker-compose.prod.yml up -d
```
