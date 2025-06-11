# Init Levels (Runlevels) in Linux

## ✅ What Init Levels Are Implemented in Linux?

**Init levels**, or **runlevels**, represent different states of a Linux system that define what services or processes should be running.

Traditionally, **System V (SysV) init** used **runlevels**. More modern Linux distributions now use **systemd**, but **runlevel targets** are still available for compatibility.

---

## 📌 Runlevels in SysV Init

| **Runlevel** | **Description**                                 |
|-------------|-------------------------------------------------|
| 0           | Halt the system (Shutdown)                     |
| 1           | Single-user mode (Maintenance/Recovery)       |
| 2           | Multi-user mode without networking (varies)   |
| 3           | Multi-user mode with networking (Text UI)     |
| 4           | Undefined / User-defined (Customizable)       |
| 5           | Multi-user mode with GUI (Graphical Login)    |
| 6           | Reboot the system                             |

---

## 📌 Common Runlevels Explained

### 🔸 **Runlevel 0** — *Shutdown/Halt*
- Used when the system is shutting down.

### 🔸 **Runlevel 1** — *Single-User Mode*
- For maintenance tasks.
- Networking, graphical interface are usually *disabled*.
- Only `root` is logged in.

### 🔸 **Runlevel 3** — *Multi-User Mode (Text Mode)*
- Network services active.
- No graphical interface.
- Used for servers.

### 🔸 **Runlevel 5** — *Multi-User Mode (Graphical)*
- Same as Runlevel 3, **plus** GUI login screen.
- Used for desktops.

### 🔸 **Runlevel 6** — *Reboot*
- Initiates a system reboot.

---

## 📌 How to Check Current Runlevel (SysV Systems)
```bash
runlevel
```
Example output:
```
N 5
```
→ Meaning system is in **runlevel 5**.

---

## 📌 Init Levels with **systemd** (Modern Linux)

Most modern Linux distributions (e.g., Ubuntu, CentOS 7+, RHEL 7+, Debian 8+) use **`systemd`**, replacing traditional runlevels with **targets**.

| **Runlevel** | **Equivalent `systemd` Target**  |
|-------------|----------------------------------|
| 0           | `poweroff.target`                |
| 1           | `rescue.target`                  |
| 2, 3, 4     | `multi-user.target`              |
| 5           | `graphical.target`               |
| 6           | `reboot.target`                  |

---

## 📌 How to Check Current Target (`systemd` systems)
```bash
systemctl get-default
```

---

## 📌 Changing Default Target (`systemd`)
```bash
sudo systemctl set-default graphical.target
```
**or**
```bash
sudo systemctl set-default multi-user.target
```

---

## ✅ Summary Table

| **Runlevel** | **Purpose**                       | **Systemd Equivalent**  |
|-------------|------------------------------------|-------------------------|
| 0           | Halt/Shutdown                     | poweroff.target         |
| 1           | Single-user mode                  | rescue.target           |
| 2           | Multi-user (non-network, varies)  | multi-user.target       |
| 3           | Multi-user (network, no GUI)      | multi
