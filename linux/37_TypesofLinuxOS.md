# 🐧 Types of Linux OS and Package Manager for Ubuntu

---

## ✅ Types of Linux OS Used

Here are common Linux distributions (distros) and what they are typically used for:

| Distro        | Base       | Purpose / Usage                                   |
|---------------|------------|---------------------------------------------------|
| **Ubuntu**    | Debian     | Most popular desktop/server; beginner-friendly    |
| **Debian**    | Debian     | Stable and minimal; often used on servers         |
| **CentOS**    | RHEL       | Enterprise-grade server OS (now replaced by Stream)|
| **RHEL**      | Red Hat    | Commercial enterprise Linux                        |
| **Fedora**    | Red Hat    | Cutting-edge; often used by developers             |
| **Arch Linux**| Independent| Lightweight, customizable, bleeding-edge           |
| **Kali Linux**| Debian     | Security testing and penetration testing           |
| **Alpine**    | Independent| Minimal image, used in containers like Docker      |

---

## 📦 What Is the Package Manager for Ubuntu?

Ubuntu uses the **APT (Advanced Package Tool)** system.

### Common APT Commands:

```bash
sudo apt update          # Refresh package list
sudo apt upgrade         # Upgrade installed packages
sudo apt install <pkg>   # Install a package
sudo apt remove <pkg>    # Remove a package
sudo apt search <pkg>    # Search for a package
```

APT uses `.deb` (Debian package) files under the hood.

### Related Tools:

| Tool         | Description                           |
|--------------|---------------------------------------|
| `apt`        | High-level package management         |
| `dpkg`       | Low-level Debian package tool         |
| `snap`       | Used for Snap packages (sandboxed)    |

---

> ✅ Ubuntu primarily uses `apt` for package management, making it easy to install, update, and remove software.
