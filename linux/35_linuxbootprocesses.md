# Linux Booting Process (Interview Explanation)

This document explains the **Linux booting process step by step**, written in an interview-friendly and easy-to-understand format.

---

## 1. BIOS / UEFI

### What happens:

* When the system is powered on, **BIOS** or **UEFI** is the first program that runs.
* It performs **POST (Power-On Self Test)** to check hardware components.
* It locates the **bootable device** (HDD, SSD, USB, etc.).

### Interview Answer:

BIOS/UEFI initializes hardware and transfers control to the bootloader.

---

## 2. Bootloader (GRUB)

### What happens:

* The bootloader is loaded into memory by BIOS/UEFI.
* The most common Linux bootloader is **GRUB2**.
* GRUB allows users to:

  * Select an operating system
  * Choose a kernel version
  * Pass kernel parameters

### Interview Answer:

GRUB loads the Linux kernel and initramfs into memory.

---

## 3. Kernel Initialization

### What happens:

* The Linux kernel is decompressed into memory.
* It initializes:

  * CPU
  * Memory
  * Device drivers
* The kernel mounts the root filesystem temporarily in read-only mode.

### Interview Answer:

The kernel initializes hardware and prepares the system environment.

---

## 4. Initramfs / Initrd

### What happens:

* **Initramfs** is a temporary root filesystem loaded into RAM.
* It contains essential drivers needed to access the actual root filesystem.
* After locating the real root filesystem, control is handed over to it.

### Interview Answer:

Initramfs helps the kernel mount the real root filesystem.

---

## 5. Init Process (PID 1)

### What happens:

* The kernel starts the first user-space process called **init**.
* This process always has **PID 1**.
* Modern Linux systems use **systemd** as the init system.

### Interview Answer:

`systemd` is the first process started by the kernel and has PID 1.

---

## 6. systemd Targets / Runlevels

### What happens:

* systemd starts system services such as:

  * Network
  * SSH
  * Docker
  * Cron
* The system is brought to a specific **target** (similar to runlevels).

### Common Targets:

* `multi-user.target` – Command-line mode
* `graphical.target` – GUI mode

### Interview Answer:

Systemd starts services and brings the system to the desired target.

---

## 7. Login Prompt

### What happens:

* The system displays a **login prompt** or **graphical login screen**.
* The Linux booting process is now complete.

---

## Linux Booting Process Flow

```
Power ON
   ↓
BIOS / UEFI
   ↓
Bootloader (GRUB)
   ↓
Kernel
   ↓
Initramfs
   ↓
systemd (PID 1)
   ↓
Services / Targets
   ↓
Login Prompt
```

---

## Important Interview Questions

### What is PID 1?

The first process started by the Linux kernel, usually `systemd`.

---

### What is GRUB?

GRUB is a bootloader responsible for loading the Linux kernel and initramfs.

---

### Difference between BIOS and UEFI?

| BIOS              | UEFI                 |
| ----------------- | -------------------- |
| Legacy firmware   | Modern firmware      |
| Uses MBR          | Uses GPT             |
| Slower            | Faster               |
| Limited disk size | Supports large disks |

---

### Command to check default target

```
systemctl get-default
```

---

### Command to change default target

```
systemctl set-default multi-user.target
```

---

## One-Line Interview Summary

Linux booting starts from BIOS/UEFI, loads GRUB, then the kernel initializes hardware, mounts the root filesystem using initramfs, starts systemd (PID 1), and finally brings up services and the login prompt.

---
