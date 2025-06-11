# Runlevel Commands in Linux

---

## ✅ What is a Runlevel?

A **runlevel** defines the **state of a Linux system** after boot. It specifies **what services or processes should be running**.

Each runlevel represents a different mode of operation for the system, such as **single-user mode**, **multi-user mode**, or **graphical mode**.

---

## 📌 Common Runlevels (SysV Init)

| **Runlevel** | **Description**                    |
|--------------|------------------------------------|
| `0`          | **Halt** (Shutdown the system)     |
| `1`          | **Single-user mode** (Recovery)    |
| `2`          | Multi-user (no networking)         |
| `3`          | **Multi-user with networking**     |
| `4`          | Unused (customizable)              |
| `5`          | **Multi-user with GUI (graphical)**|
| `6`          | **Reboot**                         |

---

## 📌 Commands to Work with Runlevels

### 🔸 1️⃣ **Check Current Runlevel**
```bash
runlevel
```
Example output:
```
N 3
```
- `N` → No previous runlevel
- `3` → Current runlevel is 3

---

### 🔸 2️⃣ **Change Runlevel Temporarily**
```bash
init <runlevel>
```
Example:
```bash
init 5
```
→ Switches to **graphical mode** (if configured)

---

### 🔸 3️⃣ **Change Runlevel Permanently (SysV Init Systems)**
Edit the **`/etc/inittab`** file:
```
id:3:initdefault:
```
→ Sets default runlevel to 3

---

## 📌 Modern Systems (Systemd)
Most modern Linux distributions **use `systemd` instead of SysV**.

| **Traditional Runlevel** | **systemd Target Equivalent**         |
|--------------------------|---------------------------------------|
| `0`                      | `poweroff.target`                   |
| `1`                      | `rescue.target`                     |
| `3`                      | `multi-user.target`                 |
| `5`                      | `graphical.target`                  |
| `6`                      | `reboot.target`                     |

### **View Default Target:**
```bash
systemctl get-default
```

### **Change Default Target:**
```bash
sudo systemctl set-default graphical.target
```

---

## ✅ Summary Table

| **Runlevel** | **Meaning (SysV)**      | **systemd Equivalent**  |
|--------------|-------------------------|-------------------------|
| `0`          | Halt                    | `poweroff.target`      |
| `1`          | Single-user mode        | `rescue.target`        |
| `3`          | Multi-user w/ networking| `multi-user.target`    |
| `5`          | Multi-user with GUI     | `graphical.target`     |
| `6`          | Reboot                  | `reboot.target`        |

---
