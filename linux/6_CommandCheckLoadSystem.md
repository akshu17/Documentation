# Checking System Load in Linux

## ✅ Command to Check the Load of the System in Linux

---

## 📌 1️⃣ `uptime`
Displays the system uptime **and** the **load averages**.
```bash
uptime
```
Example output:
```
 19:04:58 up 10 days,  3:52,  2 users,  load average: 0.45, 0.56, 0.60
```
→ **Load Averages**:
- **1 min**, **5 min**, **15 min** averages.
- Example above → 0.45 (1 min), 0.56 (5 min), 0.60 (15 min)

---

## 📌 2️⃣ `top`
Dynamic, real-time display of processes and system load:
```bash
top
```
→ **Look at the line starting with `load average:`** at the top.

---

## 📌 3️⃣ `w`
Also shows system load along with who is logged in:
```bash
w
```

---

## 📌 4️⃣ `cat /proc/loadavg`
Displays the raw **load average** numbers:
```bash
cat /proc/loadavg
```

---

## 📌 Example Interpretation of Load Average
- **Load average** represents **the number of processes waiting for CPU or I/O**.
- Example output: `0.45 0.56 0.60`
- **If you have 4 cores**, a load of **4.00** = full utilization.
- General rule:
  - **Less than number of cores** → Healthy.
  - **Equal to number of cores** → Fully utilized.
  - **Greater than number of cores** → Overloaded.

---

## ✅ Quick Summary Table

| **Command**            | **Purpose**                                |
|-----------------------|--------------------------------------------|
| `uptime`              | Shows system uptime & load averages       |
| `top`                 | Real-time view of processes & load       |
| `w`                   | Who is logged in & system load averages |
| `cat /proc/loadavg`   | Raw load average numbers                 |

---
