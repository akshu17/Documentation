# Installing Packages on Multiple Remote Servers Using a Shell Script

---

## ✅ Overview

If you have **SSH access** to multiple servers (e.g., 100 servers with **username** and **password**), you can automate package installation using:

- `sshpass` → to provide password non-interactively
- `ssh` → to connect to the remote server
- `for` loop in a shell script → to iterate over all servers
- **Package manager command** → `apt`, `yum`, or others depending on the OS

> ⚠ **Note:** Using passwords in scripts is insecure. Prefer **SSH key-based authentication** for production setups.

---

## 📌 1️⃣ Installing `sshpass`

```bash
sudo apt-get install sshpass      # Debian/Ubuntu
sudo yum install sshpass          # RHEL/CentOS
```

---

## 📌 2️⃣ Example Shell Script Using `sshpass`

```bash
#!/bin/bash

SERVER_LIST="servers.txt"
USERNAME="your_username"
PASSWORD="your_password"
PACKAGE_NAME="htop"  # Example package

while IFS= read -r SERVER
do
    echo "Installing package on $SERVER"

    sshpass -p "$PASSWORD" ssh -o StrictHostKeyChecking=no "$USERNAME@$SERVER" "sudo apt-get update && sudo apt-get install -y $PACKAGE_NAME"

done < "$SERVER_LIST"
```

---

## 📌 3️⃣ Example `servers.txt`
```
192.168.1.101
192.168.1.102
192.168.1.103
```

---

## 📌 4️⃣ For RedHat/CentOS Servers

Replace installation command with:
```bash
sudo yum install -y $PACKAGE_NAME
```
Or for newer systems:
```bash
sudo dnf install -y $PACKAGE_NAME
```

---

## 📌 5️⃣ Using SSH Keys (Recommended)

1️⃣ Generate SSH key:
```bash
ssh-keygen -t rsa
```

2️⃣ Copy public key to all servers:
```bash
ssh-copy-id user@server
```

3️⃣ Run the script **without passwords**:
```bash
ssh user@server "sudo apt-get install -y htop"
```

---

## ✅ Summary Table

| **Method**        | **Security**  | **Ease of Use**     |
|-------------------|---------------|---------------------|
| `sshpass` + `ssh` | ❗ Less secure | ✅ Easy, quick setup |
| SSH keys          | ✅ More secure | ⚠ Needs setup       |

> ⚡ **Pro Tip:** For **large-scale** setups, use **Ansible** for managing configurations and package installations across hundreds of servers efficiently.

---
