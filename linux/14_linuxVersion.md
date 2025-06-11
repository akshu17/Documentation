# How to Find Complete Details of the Linux Version You Are Using

---

## 📌 1️⃣ `cat /etc/os-release`
Displays detailed information about the OS version:
```bash
cat /etc/os-release
```
Example output:
```
NAME="Ubuntu"
VERSION="22.04.4 LTS (Jammy Jellyfish)"
ID=ubuntu
ID_LIKE=debian
PRETTY_NAME="Ubuntu 22.04.4 LTS"
VERSION_ID="22.04"
```

---

## 📌 2️⃣ `lsb_release -a`
If available, gives distribution-specific information:
```bash
lsb_release -a
```
Example output:
```
No LSB modules are available.
Distributor ID: Ubuntu
Description:    Ubuntu 22.04.4 LTS
Release:        22.04
Codename:       jammy
```
If the command is not found, install with:
```bash
sudo apt install lsb-release       # Debian/Ubuntu
sudo yum install redhat-lsb-core   # RHEL/CentOS
```

---

## 📌 3️⃣ `hostnamectl`
Displays OS version, kernel, and architecture:
```bash
hostnamectl
```
Example output:
```
Operating System: Ubuntu 22.04.4 LTS
Kernel: Linux 5.15.0-105-generic
Architecture: x86-64
```

---

## 📌 4️⃣ View Kernel Version Only
```bash
uname -r
```
Example output:
```
5.15.0-105-generic
```
Or complete details:
```bash
uname -a
```
Example output:
```
Linux ubuntu 5.15.0-105-generic #115-Ubuntu SMP ... x86_64 x86_64 x86_64 GNU/Linux
```

---

## ✅ Summary Table

| **Command**         | **Purpose**                          |
|---------------------|--------------------------------------|
| `cat /etc/os-release` | Detailed OS info                  |
| `lsb_release -a`    | Distribution-specific details       |
| `hostnamectl`       | OS, kernel, architecture            |
| `uname -r`          | Kernel version only                 |
| `uname -a`          | Full kernel/system details          |

---
