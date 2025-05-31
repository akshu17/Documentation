# Explanation of `docker run -it ubuntu`

## The Command:

```bash
docker run -it ubuntu
```

This command starts a new Ubuntu container and gives you an interactive shell to work inside it.

---

## 🚀 What it does:

It **starts a new Ubuntu container** and gives you an **interactive terminal session** inside it.

---

## 🔍 Breakdown:

* **`docker run`**
  Creates and starts a new container from an image.

* **`-it`**
  Two flags combined:

  * `-i` (**interactive**): Keeps STDIN open so you can type into the container.
  * `-t` (**TTY**): Allocates a terminal so the shell behaves like a real one.

* **`ubuntu`**
  Tells Docker to use the official **Ubuntu** image.

---

## 🧪 What Happens:

* Docker pulls the `ubuntu` image if it's not already on your system.
* A new container starts with a shell (`/bin/bash`) by default.
* You’re placed **inside the Ubuntu container’s terminal**, where you can run commands like:

```bash
apt update
ls
echo "Hello from inside the container"
```

You’ll see a prompt like:

```bash
root@container-id:/#
```

---

## 🔚 To Exit the Container:

Type:

```bash
exit
```

Or press `Ctrl + D`.

---

## Analogy

* `-i` = You have a keyboard (you can type).
* `-t` = You have a monitor (you can see terminal output clearly).
