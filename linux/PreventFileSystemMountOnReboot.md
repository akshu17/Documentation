# Preventing a Filesystem from Mounting on Reboot (Linux)

## ✅ Why Would You Disable Auto-Mount?

Sometimes you don’t want certain partitions, drives, or network filesystems to **auto-mount** at boot. This could be because:

- It’s a temporary drive or USB.
- You’re troubleshooting boot issues.
- You don’t want that filesystem used anymore.

By default, **mount points** are controlled by entries in **`/etc/fstab`**, or dynamically by systemd and automounters.

---

## 📌 Steps to Prevent Filesystem from Mounting on Boot

### 1️⃣ Identify the Filesystem
Run:
```bash
lsblk -f
```
Or:
```bash
blkid
```
→ Lists block devices and their UUIDs, mount points, etc.

Example output:
```
/dev/sdb1: UUID="1234-ABCD" TYPE="ext4" PARTUUID="abcd-01"
```

---

### 2️⃣ Modify `/etc/fstab`
`/etc/fstab` tells Linux what filesystems to mount at boot.

#### Example entry in `/etc/fstab`:
```
UUID=1234-ABCD /mnt/data ext4 defaults 0 2
```

#### 🚫 Prevent from mounting:
- **Option 1: Comment out the entry**
```bash
#UUID=1234-ABCD /mnt/data ext4 defaults 0 2
```
- **Option 2: Remove the entry entirely.**
```bash
sudo nano /etc/fstab
```
Delete or comment → **Save and Exit**.

---

### 3️⃣ Testing Without Rebooting (Recommended)
If you want to **test** before rebooting:
```bash
sudo mount -a
```
- If there’s no error → OK.
- Check if the filesystem is mounted:
```bash
mount | grep /mnt/data
```
→ It should **not** appear if removed or commented properly.

---

### 4️⃣ Advanced: Using the `noauto` Option
Sometimes you may want to *keep* the entry but **prevent auto-mount at boot**, allowing **manual mounting** later.

**Example:**
```
UUID=1234-ABCD /mnt/data ext4 noauto,defaults 0 2
```
→ It **won’t** mount automatically on boot, but you can mount it manually:
```bash
sudo mount /mnt/data
```

---

### 5️⃣ Using Systemd (if applicable)
If the mount is managed via systemd (`.mount` units):

List current mounts:
```bash
systemctl list-units --type=mount
```

Disable a mount unit permanently:
```bash
sudo systemctl disable <mount-name>.mount
```

---

## ✅ Verify on Next Boot
After reboot:
```bash
mount | grep <mount-point>
```
→ If **no result**, filesystem is not mounted.

---

## 📌 Summary Table

| **Action**                     | **Method**                              |
|---------------------------------|-----------------------------------------|
| Comment/remove from `/etc/fstab`| `#UUID=xxxx-xxxx /mount/point ...`     |
| Disable systemd mount unit      | `sudo systemctl disable name.mount`    |
| Use `noauto` to disable auto-mount | `UUID=xxxx /mount/point ext4 noauto ...` |
| Verify                         | `mount | grep /mount-point`            |

---

## ⚠️ Important Notes

- **Critical Filesystems**: Do NOT disable mounts for **`/`**, **`/boot`**, or other **essential system partitions** unless you know exactly what you’re doing.
- For **removable drives/USBs**: They don’t need `/etc/fstab` entries unless you’ve added them manually.

---
