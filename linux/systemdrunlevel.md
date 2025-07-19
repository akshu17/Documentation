# 🔄 systemd Runlevels (Targets)

In traditional Linux systems using **SysVinit**, the system booted into **runlevels** (0–6). With **systemd**, these are replaced by **targets**, which offer more flexibility and clarity.

---

## 🔁 Traditional Runlevels vs systemd Targets

| Runlevel | systemd Target         | Description                              |
|----------|------------------------|------------------------------------------|
| 0        | `poweroff.target`      | Halt the system                          |
| 1        | `rescue.target`        | Single-user mode (maintenance)           |
| 2        | `multi-user.target`    | Multi-user mode (no networking in some distros) |
| 3        | `multi-user.target`    | Full multi-user mode with networking     |
| 4        | `multi-user.target`    | (Unused / customizable)                  |
| 5        | `graphical.target`     | Multi-user mode with GUI                 |
| 6        | `reboot.target`        | Reboot the system                        |

---

## 🛠 How to Check Current Target

```bash
systemctl get-default
```

---

## 🛠 How to Set Default Target (Runlevel)

```bash
# Set to GUI (graphical target)
sudo systemctl set-default graphical.target

# Set to CLI only (no GUI)
sudo systemctl set-default multi-user.target
```

---

## 🔁 Switching Target Temporarily

```bash
# Switch to text mode (no GUI)
sudo systemctl isolate multi-user.target

# Switch to GUI
sudo systemctl isolate graphical.target
```

---

## 📍 Common Targets Explained

| Target              | Purpose                                 |
|---------------------|------------------------------------------|
| `rescue.target`     | Single-user mode, minimal services       |
| `multi-user.target` | CLI-based multi-user mode                |
| `graphical.target`  | GUI with multi-user mode                 |
| `emergency.target`  | Minimal system, no services; for recovery |
| `reboot.target`     | Reboots the system                       |
| `poweroff.target`   | Shuts down the system                    |

---

> ✅ In `systemd`, **targets** are more flexible than runlevels and can include dependencies, making them more modular and powerful.
