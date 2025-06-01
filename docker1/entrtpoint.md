# Understanding ENTRYPOINT in Docker

In Docker, the `ENTRYPOINT` instruction defines the command that will always run when a container starts. It sets the main command to be executed and is typically used when you want your container to run a specific executable.

## Purpose of ENTRYPOINT

* Ensures a specific command is always executed
* Useful for setting up containers with a dedicated purpose (e.g., a web server, a CLI tool)
* Allows parameters to be passed dynamically via `docker run`

## Syntax

There are two forms of the `ENTRYPOINT` instruction:

### 1. Exec form (preferred)

```Dockerfile
ENTRYPOINT ["executable", "param1", "param2"]
```

* Does not invoke a shell
* Allows signal handling (important for PID 1)

### 2. Shell form

```Dockerfile
ENTRYPOINT command param1 param2
```

* Executes in `/bin/sh -c`
* Does not handle signals well

## ENTRYPOINT vs CMD

* `ENTRYPOINT` sets the **main command** to run
* `CMD` provides **default arguments** to the `ENTRYPOINT`
* If both are defined, `CMD` arguments are appended to the `ENTRYPOINT`

### Example

```Dockerfile
FROM ubuntu
ENTRYPOINT ["echo"]
CMD ["Hello from Docker!"]
```

Running this container will output:

```
Hello from Docker!
```

## Overriding ENTRYPOINT

You can override the `ENTRYPOINT` at runtime with:

```bash
docker run --entrypoint <new_command> image_name
```

## Best Practices

* Use exec form to ensure proper signal handling
* Combine `ENTRYPOINT` with `CMD` for flexible container configurations
* Avoid using shell form unless necessary

---

This ensures consistent container behavior and enables reusable and modular Docker images.
