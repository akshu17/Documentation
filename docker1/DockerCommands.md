# 🐳 Docker Command Cheat Sheet

## Basic Docker Commands
| Command | Description |
|--------|-------------|
| `docker version` | Show Docker version info |
| `docker info` | Display system-wide information |
| `docker help` | Show help for Docker commands |

---

## 📦 Image Management
| Command | Description |
|--------|-------------|
| `docker images` | List all local images |
| `docker pull <image>` | Download an image from Docker Hub |
| `docker build -t <name> .` | Build an image from a Dockerfile |
| `docker rmi <image>` | Remove an image |
| `docker tag <image> <new-name>` | Tag an image |
| `docker save -o <file.tar> <image>` | Save image to a tar file |
| `docker load -i <file.tar>` | Load image from tar file |
| `docker import <url\|file>` | Import an image from a tarball |
| `docker export <container>` | Export a container's filesystem as a tar archive |

---

## 🚀 Container Management
| Command | Description |
|--------|-------------|
| `docker ps` | List running containers |
| `docker ps -a` | List all containers (running + stopped) |
| `docker run <image>` | Run a new container |
| `docker run -d <image>` | Run container in detached mode |
| `docker run -it <image> bash` | Run container interactively |
| `docker start <container>` | Start a stopped container |
| `docker stop <container>` | Stop a running container |
| `docker restart <container>` | Restart a container |
| `docker kill <container>` | Forcefully stop a container |
| `docker rm <container>` | Remove a container |
| `docker exec -it <container> bash` | Run command inside a running container |
| `docker attach <container>` | Attach to a running container |
| `docker logs <container>` | View logs from a container |
| `docker inspect <container>` | Show detailed container info |
| `docker cp <container>:<path> <local>` | Copy files from container to host |
| `docker rename <old> <new>` | Rename a container |
| `docker pause <container>` | Pause all processes in a container |
| `docker unpause <container>` | Unpause a paused container |
| `docker top <container>` | Show running processes in container |
| `docker update <container>` | Update resource limits of a container |
| `docker stats` | Show container resource usage statistics |

---

## 🗃️ Volume Management
| Command | Description |
|--------|-------------|
| `docker volume create <name>` | Create a new volume |
| `docker volume ls` | List all volumes |
| `docker volume inspect <name>` | Show details about a volume |
| `docker volume rm <name>` | Remove a volume |
| `docker volume prune` | Remove all unused volumes |

---

## 🌐 Network Management
| Command | Description |
|--------|-------------|
| `docker network ls` | List all networks |
| `docker network create <name>` | Create a new network |
| `docker network inspect <name>` | Inspect network details |
| `docker network connect <network> <container>` | Connect a container to a network |
| `docker network disconnect <network> <container>` | Disconnect container from network |
| `docker network rm <name>` | Remove a network |
| `docker network prune` | Remove unused networks |

---

## 🔧 Docker System Commands
| Command | Description |
|--------|-------------|
| `docker system df` | Show disk usage by Docker |
| `docker system prune` | Remove unused data (images, containers, volumes, etc.) |
| `docker system info` | Display system-wide information |

---

## 🐳 Docker Compose (Bonus)
| Command | Description |
|--------|-------------|
| `docker-compose up` | Start services defined in `docker-compose.yml` |
| `docker-compose up -d` | Start services in detached mode |
| `docker-compose down` | Stop and remove containers, networks, and volumes |
| `docker-compose build` | Build services |
| `docker-compose ps` | List containers |
| `docker-compose logs` | View output logs |
| `docker-compose exec <service> bash` | Run a command inside a service container |
