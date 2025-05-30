# Streaming Live Logs from a Container

To get live logs of a container, you typically use the container runtime’s logging command that streams logs in real time.

Here are the most common ways for popular container runtimes:

## 1. Docker

To stream live logs from a running Docker container:

```bash
docker logs -f <container_id_or_name>


-f or --follow flag means follow the logs (like tail -f).
You can add --tail N to show last N lines before following.


docker logs -f my-app-container
