---

# Checking Number of CPU Cores in Linux

## ✅ Commands to Check How Many CPU Cores Are There in the System

---

## 📌 1️⃣ `lscpu`
Displays detailed CPU architecture information, including number of cores.
```bash
lscpu
```
Look for:
```
CPU(s):              8
Core(s) per socket:  4
Socket(s):           2
```
- **CPU(s)** → Number of processing units (logical cores)
- **Core(s) per socket** → Number of cores per physical processor
- **Socket(s)** → Number of physical processors

---

## 📌 2️⃣ `nproc`
Simpler command that displays the **number of processing units** available:
```bash
nproc
```
Example output:
```
8
```

---

## 📌 3️⃣ `cat /proc/cpuinfo`
Shows detailed CPU info. To count the number of cores:
```bash
grep -c ^processor /proc/cpuinfo
```
→ Gives the **number of logical cores**.

---

## ✅ Quick Summary Table

| **Command**                     | **Purpose**                              |
|---------------------------------|------------------------------------------|
| `lscpu`                         | Detailed CPU architecture & core info   |
| `nproc`                         | Number of available cores (processing units) |
| `grep -c ^processor /proc/cpuinfo` | Number of cores from detailed CPU info |

---
