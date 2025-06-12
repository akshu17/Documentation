# 🖥️ Listing Running Processes in Linux/Unix

## ✅ Using `ps` Command

The `ps` (process status) command displays information about **active processes**.

### 🔹 Basic Usage:

```bash
ps
```

This shows processes running **under the current terminal**.

### 🔹 Show All Processes:

```bash
ps -e
```

or

```bash
ps -A
```

### 🔹 Detailed Information:

```bash
ps -ef
```

or

```bash
ps aux
```

| Option       | Meaning                            |
| ------------ | ---------------------------------- |
| `-e` or `-A` | Show all processes                 |
| `-f`         | Full-format listing                |
| `a`          | Show processes of all users        |
| `u`          | Show user/owner of the process     |
| `x`          | Include processes without terminal |

---

## ✅ Using `top` Command (Real-Time View)

```bash
top
```

* Displays a **real-time** view of processes.
* Press **`q`** to quit.

---

## ✅ Using `htop` (Interactive, User-Friendly)

```bash
htop
```

* Advanced version of `top` (requires installation)
* Allows easy navigation and sorting
* Install with:

```bash
sudo apt install htop      # Debian/Ubuntu
sudo yum install htop      # RHEL/CentOS
brew install htop          # macOS
```

---

## ✅ Using `pgrep` (Find by Name)

```bash
pgrep nginx
```

* Lists **process IDs (PIDs)** of processes matching the name.

---

## ✅ Using `pidof` (Get PID of a Program)

```bash
pidof sshd
```

* Returns the **process ID** of the given program name.

---

## 📋 Example Output of `ps -ef`:

```plaintext
UID        PID  PPID  C STIME TTY          TIME CMD
root         1     0  0 10:00 ?        00:00:05 /sbin/init
user      1234  1001  0 10:01 pts/0    00:00:00 bash
user      5678  1234  2 10:02 pts/0    00:00:05 python script.py
```

---

## ✅ Conclusion

| Command  | Purpose                                |
| -------- | -------------------------------------- |
| `ps -ef` | List all processes with details        |
| `top`    | Real-time resource usage               |
| `htop`   | User-friendly interactive process view |
| `pgrep`  | Find processes by name (PID only)      |
| `pidof`  | Find PID of a specific command         |

---

> ⚙️ **Pro Tip**: Combine with `grep` to search for specific processes:
>
> ```bash
> ps -ef | grep java
> ```

---
