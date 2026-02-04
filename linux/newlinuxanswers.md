# Linux Interview Questions and Answers (DevOps Focus)

This document covers commonly asked Linux interview questions with answers for DevOps and system administration roles.

---

## 1. `uname`

### Question: What is the use of the `uname` command?

**Answer:**
The `uname` command displays system-related information such as kernel name, kernel version, and system architecture.

### Common Options:

```bash
uname -a   # Displays all system information
uname -r   # Kernel release version
uname -m   # Machine hardware name
uname -n   # Network node hostname
```

**Interview One-liner:**
`uname` is used to check kernel and system architecture details.

---

## 2. `lsb_release`

### Question: What does `lsb_release` do?

**Answer:**
`lsb_release` provides Linux distribution-specific information like OS name, version, and codename.

### Example:

```bash
lsb_release -a
```

**Interview One-liner:**
`lsb_release` is used to identify the Linux distribution and version.

---

## 3. `uptime`

### Question: What information does `uptime` show?

**Answer:**
The `uptime` command shows how long the system has been running, the number of logged-in users, and the system load average.

### Example:

```bash
uptime
```

**Interview One-liner:**
`uptime` is used to check system running time and load averages.

---

## 4. `top`

### Question: What is the `top` command used for?

**Answer:**
`top` displays real-time information about system performance, including CPU usage, memory usage, and running processes.

### Useful Shortcuts in `top`:

* `q` → Quit
* `k` → Kill a process
* `M` → Sort by memory usage
* `P` → Sort by CPU usage

**Interview One-liner:**
`top` is used for real-time monitoring of system performance and processes.

---

## 5. `ps`

### Question: What does the `ps` command do?

**Answer:**
The `ps` command displays a snapshot of currently running processes.

### Common Usage:

```bash
ps -ef
ps aux
```

**Interview One-liner:**
`ps` is used to view running processes in the system.

---

## 6. `free`

### Question: What is the use of the `free` command?

**Answer:**
`free` shows memory usage including total, used, free, and available RAM along with swap memory.

### Example:

```bash
free -m
free -h
```

**Interview One-liner:**
`free` is used to check RAM and swap memory usage.

---

## 7. `du`

### Question: What does the `du` command do?

**Answer:**
`du` estimates disk space usage for files and directories.

### Common Usage:

```bash
du -sh /directory
du -h --max-depth=1
```

**Interview One-liner:**
`du` is used to find disk space consumed by directories and files.

---

## 8. `df`

### Question: What is the `df` command?

**Answer:**
`df` displays disk space usage of mounted filesystems.

### Example:

```bash
df -h
```

**Interview One-liner:**
`df` is used to check available and used disk space on filesystems.

---

## Important Differences (Interview Favorites)

### Difference between `du` and `df`

| du                                    | df                              |
| ------------------------------------- | ------------------------------- |
| Shows disk usage of files/directories | Shows disk usage of filesystems |
| File-level usage                      | Filesystem-level usage          |

---

### Difference between `top` and `ps`

| top                  | ps                         |
| -------------------- | -------------------------- |
| Real-time monitoring | Snapshot at execution time |
| Interactive          | Non-interactive            |

---

## Scenario-Based Interview Question

### Question: If a Linux server is slow, which commands will you use?

**Answer:**

```bash
uptime
top
free -h
df -h
ps -ef
```

---

## Final Summary

These Linux commands are essential for system identification, monitoring, memory analysis, disk usage tracking, and troubleshooting in DevOps environments.
