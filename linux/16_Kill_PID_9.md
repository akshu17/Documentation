# What Does `kill -9 <process>` Do?

---

## 📌 What is `kill`?

The `kill` command **sends signals to processes** to control their behavior (usually to terminate them).

---

## 📌 Meaning of `kill -9`

- `-9` refers to **SIGKILL**, a powerful signal that **forcibly stops a process**.
- Syntax:
```bash
kill -9 <PID>
```
→ **Forcefully terminates** the process with **Process ID (PID)** `<PID>`.

⚠️ **Important**: `kill -9` *does not allow the process to clean up*. It is immediate and forceful.

---

## 📌 Why `-9` / SIGKILL?

| **Signal**   | **Number** | **Meaning**                               |
|--------------|------------|-------------------------------------------|
| `SIGTERM`    | 15         | Gracefully ask the process to terminate   |
| `SIGKILL`    | 9          | Forcefully kill; *cannot be ignored*      |

- **`kill <PID>`** (default sends `SIGTERM`) → Graceful stop.
- **`kill -9 <PID>`** → Immediate, forceful stop.

---

## 📌 How to Use It

### 🔸 1️⃣ Find Process ID (PID):
```bash
ps -ef | grep <processname>
```

### 🔸 2️⃣ Kill Process by PID:
```bash
kill -9 <PID>
```
Example:
```bash
kill -9 1234
```

### 🔸 3️⃣ Kill by Name (with `pkill`):
```bash
pkill -9 <processname>
```

---

## ⚠️ When to Use `kill -9`

✅ Use **only when**:
- Normal termination (`kill <PID>`) doesn’t work.
- The process is *frozen* or *misbehaving*.

❌ **Avoid overuse** of `-9` because:
- Files may remain locked.
- Resources may not release properly.
- Services might restart improperly.

---

## ✅ Summary Table

| **Command**        | **Action**                                 |
|--------------------|--------------------------------------------|
| `kill <PID>`       | Graceful stop (default `SIGTERM`)          |
| `kill -9 <PID>`    | Forceful, immediate termination (`SIGKILL`)|
| `pkill -9 <name>`  | Kill by process name using `SIGKILL`       |

---
