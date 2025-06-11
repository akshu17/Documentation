# Understanding `ps -ef` Command in Linux

---

## 📌 What is `ps`?

The `ps` command (**process status**) displays **information about active processes** on a Linux system.

---

## 📌 Meaning of `ps -ef`

| **Option** | **Meaning**                                         |
|------------|------------------------------------------------------|
| `-e`       | Show **all** processes (same as `-A`)                |
| `-f`       | Show **full-format** listing (extra details shown)   |

So:
```bash
ps -ef
```
→ **Displays all running processes** in a **detailed format**.

---

## 📌 Example Output
```
UID        PID  PPID  C STIME TTY          TIME CMD
root         1     0  0 10:30 ?        00:00:02 /sbin/init
user      2045     1  0 10:32 ?        00:00:00 /lib/systemd/systemd --user
user      2060  2045  0 10:32 ?        00:00:00 (sd-pam)
```

---

## 📌 Column Descriptions:

| **Column** | **Description**                                        |
|------------|--------------------------------------------------------|
| `UID`      | User ID of the process owner                           |
| `PID`      | Process ID                                              |
| `PPID`     | Parent Process ID (which process started this process)  |
| `C`        | CPU usage percentage                                   |
| `STIME`    | Start time of the process                              |
| `TTY`      | Terminal associated with the process                   |
| `TIME`     | Cumulative CPU time                                    |
| `CMD`      | Command that started the process                       |

---

## 📌 Common Usage with `ps -ef`

### 🔸 1️⃣ Find processes by name:
```bash
ps -ef | grep nginx
```
→ Lists all processes related to `nginx`.

### 🔸 2️⃣ Find process by PID:
```bash
ps -ef | grep 1234
```

---

## ✅ Summary Table

| **Command**           | **Purpose**                                  |
|-----------------------|----------------------------------------------|
| `ps -ef`              | Lists all running processes (full format)   |
| `ps -ef | grep <proc>`| Search for specific process by name or PID  |

---
