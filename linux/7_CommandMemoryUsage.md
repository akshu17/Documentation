# Checking Memory (RAM) Usage in Linux

## ✅ Commands to Check Memory (RAM) Usage in Linux

---

## 📌 1️⃣ `free`
Displays total, used, and available memory.
```bash
free -h
```
- `-h` → human-readable format (e.g., MB, GB)
Example output:
```
              total        used        free      shared  buff/cache   available
Mem:           16Gi       5.2Gi       4.0Gi       1.1Gi       6.0Gi       9.7Gi
Swap:          2.0Gi       0.0Gi       2.0Gi
```
**Fields:**
- **total**: Total installed memory
- **used**: Memory in use
- **free**: Completely unused memory
- **available**: Memory available for new processes

---

## 📌 2️⃣ `top` or `htop`
### `top`
```bash
top
```
- Shows real-time memory usage along with processes.
- Look at the `KiB Mem` or `MiB Mem` line at the top.

### `htop` *(if installed)*
```bash
htop
```
- Interactive, colorful, easier to read.

Install with:
```bash
sudo apt install htop   # Debian/Ubuntu
sudo yum install htop   # RHEL/CentOS
```

---

## 📌 3️⃣ `vmstat`
Displays memory usage along with other system stats.
```bash
vmstat -s -SM
```
→ `-s`: display in summary form  
→ `-SM`: display in megabytes

---

## 📌 4️⃣ `/proc/meminfo`
View detailed memory info:
```bash
cat /proc/meminfo
```
- Provides **fine-grained** details, such as cached memory, swap usage, buffers, etc.

---

## ✅ Quick Summary Table

| **Command**         | **Purpose**                             |
|--------------------|-----------------------------------------|
| `free -h`          | Quick summary of memory usage          |
| `top` / `htop`     | Real-time, detailed memory + processes |
| `vmstat -s -SM`    | Summary of memory stats                |
| `cat /proc/meminfo`| Detailed raw memory information        |

---
