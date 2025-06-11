# Using `top` Command to Control Running Processes in Linux

---

## ✅ Overview

The `top` command provides a dynamic, real-time view of a running system, including system summary information and a list of processes or threads currently being managed by the Linux kernel.

---

## 📌 1️⃣ Launching `top`
```bash
top
```
- Displays real-time information about CPU, memory usage, and running processes.
- By default, processes are sorted by CPU usage.

---

## 📌 2️⃣ Controlling Processes Within `top`

| **Key** | **Action**                             |
|---------|----------------------------------------|
| **k**   | **Kill** a process                     |
| **r**   | **Renice** (change priority) of a process |
| **P**   | Sort by **CPU usage**                  |
| **M**   | Sort by **Memory usage**               |
| **N**   | Sort by **PID (Process ID)**           |
| **T**   | Sort by running **time**               |
| **h**   | Help (shows all interactive commands)  |
| **q**   | Quit `top`                             |

---

## 📌 3️⃣ Killing a Process via `top`

1️⃣ Press **`k`**  
2️⃣ Enter the **PID** of the process you want to kill.  
3️⃣ Enter the **signal** (default is `15` for graceful termination, use `9` for force kill).  
Example:
```
PID to kill: 1234
Signal to send [15]: 9
```

---

## 📌 4️⃣ Renicing a Process via `top`

1️⃣ Press **`r`**  
2️⃣ Enter the **PID** of the process.  
3️⃣ Enter a new **nice value** (range: `-20` to `19`, lower = higher priority).

---

## 📌 5️⃣ Additional Tips

- Use **`htop`** for a more user-friendly, colorful, interactive interface with mouse support.
- Install `htop` with:
```bash
sudo apt install htop   # Debian/Ubuntu
sudo yum install htop   # RHEL/CentOS
```

---

## ✅ Quick Summary Table

| **Action**      | **Command/Key**  |
|-----------------|------------------|
| Kill process    | `k`              |
| Change priority | `r`              |
| Sort by CPU     | `P`              |
| Sort by Memory  | `M`              |
| Help            | `h`              |
| Quit            | `q`              |

---
