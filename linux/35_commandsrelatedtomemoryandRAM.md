# 🧠 Linux Commands Related to Memory and RAM

This guide provides essential commands to check, monitor, and analyze memory (RAM) usage on a Linux system.

---

## 📊 1. `free`

```bash
free -h
```

- Shows used, free, total, and available memory.
- `-h` = human-readable (e.g., MB, GB)

---

## 📈 2. `top`

```bash
top
```

- Real-time display of system processes.
- Memory usage shown under `KiB Mem` and `RES` columns.

> Press `Shift + M` inside `top` to sort by memory usage.

---

## 🔍 3. `htop` (Improved `top`)

```bash
htop
```

- Enhanced, color-coded version of `top`.
- Easier to visualize memory and swap usage.

> ❗ May require installation:
```bash
sudo apt install htop  # Debian/Ubuntu
sudo yum install htop  # RHEL/CentOS
```

---

## 🧾 4. `vmstat`

```bash
vmstat 1 5
```

- Reports virtual memory stats every 1 second for 5 iterations.
- Includes info on memory, processes, CPU, I/O, etc.

---

## 📦 5. `cat /proc/meminfo`

```bash
cat /proc/meminfo
```

- Shows detailed memory stats directly from the kernel.
- Useful for scripting or debugging memory behavior.

---

## 🧮 6. `ps aux --sort=-%mem`

```bash
ps aux --sort=-%mem | head
```

- Lists processes sorted by memory usage.
- Top consumers appear first.

---

## 🔍 7. `smem` (Accurate memory reporting)

```bash
smem -r | head
```

- Reports memory usage per process.
- Includes shared memory more accurately than `ps`.

> ❗ Install if not present:
```bash
sudo apt install smem
```

---

## 📊 8. `sar` (System Activity Report)

```bash
sar -r 1 5
```

- Shows memory usage stats over time.

> ❗ Requires `sysstat` package:
```bash
sudo apt install sysstat
```

---

## 🧪 9. `watch -n 1 free -h`

```bash
watch -n 1 free -h
```

- Continuously monitors memory every second using `free`.

---

## 🧠 Summary Table

| Command                | Purpose                             |
|------------------------|-------------------------------------|
| `free -h`              | View total, used, and free memory   |
| `top` / `htop`         | Real-time system monitoring         |
| `vmstat`               | Virtual memory statistics           |
| `cat /proc/meminfo`    | Low-level memory info               |
| `ps aux --sort=-%mem`  | Show top memory-using processes     |
| `smem`                 | Detailed memory per process         |
| `sar -r`               | Historical memory usage             |

---

> ✅ Use these tools regularly to monitor performance, diagnose memory issues, and optimize your system.
