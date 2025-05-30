# How to List Running Containers and Check Container Details

## Step 1: List all running containers

Use the following command to list all running containers:

```bash
docker ps
```

This command will show you all running containers with details like Container ID, image, status, ports, and names.

---

## Step 2: Check details of a specific container

To check detailed information about a container, use:

```bash
docker inspect <container_id_or_name>
```

Replace `<container_id_or_name>` with the actual container ID or name from the output of `docker ps`.

---

## Example

1. **List containers:**

```bash
$ docker ps

CONTAINER ID   IMAGE          COMMAND                  CREATED        STATUS       PORTS                    NAMES
a1b2c3d4e5f6   nginx:latest   "nginx -g 'daemon of…"   2 hours ago    Up 2 hours   0.0.0.0:8080->80/tcp     webserver
```

2. **Inspect the container:**

```bash
docker inspect a1b2c3d4e5f6
```

This outputs a JSON with detailed information such as network settings, volumes, environment variables, and more.

---

If you want help with other container runtimes like Podman or Kubernetes, feel free to ask!
