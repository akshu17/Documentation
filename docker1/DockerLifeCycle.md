# Life Cycle of a Docker Container

A Docker container goes through several stages from creation to removal. The key phases are:

## 1. Create
- When you run a command like `docker create` or `docker run`, Docker creates a new container from a specified image.
- The container is created but **not yet started** (in the case of `docker create`).
- The container has its own writable layer on top of the image layers.

## 2. Start
- When you start a container (`docker start` or `docker run`), Docker allocates resources and starts the container’s process.
- The container runs the specified command or entrypoint.

## 3. Running
- The container is executing and doing its job.
- You can interact with it (attach, exec, logs).
- The container continues running until the process exits or it is stopped.

## 4. Stop
- The container is asked to stop gracefully (`docker stop`).
- Docker sends a SIGTERM signal to the process inside the container, giving it some time to terminate cleanly.
- If it doesn’t stop within the timeout, Docker sends SIGKILL to force terminate it.

## 5. Restart (optional)
- Depending on restart policies (`--restart` flag), the container may automatically restart after stopping.
- Useful for ensuring high availability.

## 6. Pause / Unpause (optional)
- You can temporarily pause container processes (`docker pause`).
- Later, you can unpause to resume processes (`docker unpause`).

## 7. Remove
- Once you no longer need the container, you can remove it using `docker rm`.
- This deletes the container and its writable layer.
- You cannot remove a running container (need to stop it first).

---

## Summary Table

| Stage      | Description                                              | Commands              |
|------------|----------------------------------------------------------|-----------------------|
| **Create** | Creates a container but doesn’t start it                 | `docker create`       |
| **Start**  | Starts the container process                              | `docker start`        |
| **Running**| Container runs the specified application/process         | `docker run` / running|
| **Stop**   | Gracefully stops the container                            | `docker stop`         |
| **Restart**| Automatically or manually restarts container              | `docker restart`      |
| **Pause**  | Temporarily suspends container processes                  | `docker pause`        |
| **Unpause**| Resumes paused container processes                        | `docker unpause`      |
| **Remove** | Deletes the container permanently                          | `docker rm`           |

