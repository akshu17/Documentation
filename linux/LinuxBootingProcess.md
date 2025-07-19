# 🚀 Linux Booting Process

The Linux boot process is the sequence of steps that occur from powering on a machine to reaching a fully functional Linux environment (CLI or GUI).

---

## 🔢 Step-by-Step Boot Process

### 1️⃣ **BIOS / UEFI Initialization**
- BIOS (Basic Input/Output System) or UEFI initializes hardware components.
- Performs POST (Power-On Self-Test).
- Locates the boot device (HDD, SSD, USB, etc.).

---

### 2️⃣ **MBR / GPT (Bootloader Stage 1)**
- MBR (Master Boot Record) or GPT (GUID Partition Table) is located on the bootable disk.
- Points to the bootloader program (like GRUB, LILO, or systemd-boot).

---

### 3️⃣ **Bootloader (GRUB / LILO)**
- GRUB (GRand Unified Bootloader) is commonly used.
- Displays a boot menu (if configured).
- Loads and passes control to the Linux **kernel**.
- Can boot multiple operating systems.

---

### 4️⃣ **Kernel Initialization**
- The Linux kernel is loaded into memory.
- Initializes CPU, memory management, and device drivers.
- Mounts the **root filesystem**.
- Starts **initrd/initramfs** (temporary root filesystem for loading modules).

---

### 5️⃣ **Init System (systemd / init / Upstart)**
- The kernel executes PID 1: usually `systemd`, `SysVinit`, or `Upstart`.
- This is the **user-space initialization**.
- Starts essential services like networking, logging, etc.

---

### 6️⃣ **System Targets / Runlevels**
- `systemd` reaches a target like:
  - `multi-user.target` (non-GUI)
  - `graphical.target` (GUI)
- Older systems use runlevels (0–6).

---

### 7️⃣ **Login Prompt**
- User is presented with:
  - A **login shell** (tty) for CLI systems
  - A **Display Manager** (like GDM, LightDM) for GUI

---

## 🧠 Boot Summary Flow

```text
BIOS/UEFI → MBR/GPT → Bootloader → Kernel → initramfs → systemd/init → Targets/Runlevels → Login
```

---

## 🧪 Commands for Boot Troubleshooting

| Command                  | Purpose                                |
|--------------------------|----------------------------------------|
| `dmesg`                  | View kernel ring buffer logs           |
| `journalctl -b`          | View boot logs                         |
| `lsblk` / `blkid`        | View block devices & partitions        |
| `systemctl list-units`  | View active services                   |
| `grub-mkconfig`          | Regenerate GRUB config (advanced)      |

---

> ✅ Understanding the boot process is essential for Linux admins, troubleshooting, and system recovery.

---
