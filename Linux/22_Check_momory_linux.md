# 🖥️ How to Check Memory in Linux Server

Monitoring memory usage on a Linux server is essential for system administration. Below are the most common commands to check memory usage.

---

## ✅ Using `free` Command

```bash
free -h
```

| Option | Description            |
| ------ | ---------------------- |
| `-h`   | Human-readable (MB/GB) |

**Example Output:**

```plaintext
              total        used        free      shared  buff/cache   available
Mem:            15G         3.1G         7.0G         180M         5.0G         11G
Swap:          2.0G         0B          2.0G
```

* **total**: Total installed RAM
* **used**: RAM in use
* **free**: Completely free RAM
* **buff/cache**: Memory used by cache/buffers
* **available**: Approx. available memory for new applications

---

## ✅ Using `top` Command (Real-Time View)

```bash
top
```

* Memory usage is shown at the top of the screen.
* Press `q` to quit.

---

## ✅ Using `htop` (Interactive, User-Friendly)

```bash
htop
```

* Displays CPU, memory, and process usage graphically.
* Install with:

```bash
sudo apt install htop      # Debian/Ubuntu
sudo yum install htop      # RHEL/CentOS
brew install htop          # macOS
```

---

## ✅ Using `/proc/meminfo`

```bash
cat /proc/meminfo
```

* Detailed memory statistics.

---

## ✅ Using `vmstat` Command

```bash
vmstat -s
```

* Displays memory, swap, IO, and CPU statistics.

---

## ✅ Summary of Commands

| Command             | Purpose                        |
| ------------------- | ------------------------------ |
| `free -h`           | Overall memory usage           |
| `top`               | Real-time usage                |
| `htop`              | User-friendly interactive view |
| `cat /proc/meminfo` | Detailed stats from proc       |
| `vmstat -s`         | System performance summary     |

---

## 🗨️ Quote

> **"Monitor your memory before your memory monitors you."**

---

## ✅ Conclusion

For regular memory checks, use:

```bash
free -h
```

For real-time monitoring:

```bash
top
```

or

```bash
htop
```

For detailed analysis:

```bash
cat /proc/meminfo
```

---
