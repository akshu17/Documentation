# Creating Filesystems and Ensuring Availability After Reboot

## ✅ Have You Created a Filesystem and Ensured It’s Available After Reboot?

Yes — **creating a filesystem** and **making sure it’s available after reboot** is a very common task when working with Linux systems, especially when setting up additional disks, partitions, or new servers.

---

## 📌 1️⃣ How to Create a Filesystem

### Step 1: Partition the Disk (if needed)
Use `lsblk` to view available disks:
```bash
lsblk
```

Partition the disk (example for `/dev/sdb`):
```bash
sudo fdisk /dev/sdb
```
→ Create a new partition, write changes.

### Step 2: Format the Partition
```bash
sudo mkfs.ext4 /dev/sdb1
```
*(Or use `mkfs.xfs`, `mkfs.vfat`, etc., depending on your needs)*

---

## 📌 2️⃣ Create a Mount Point
```bash
sudo mkdir -p /mnt/mydata
```

---

## 📌 3️⃣ Mount the Filesystem
```bash
sudo mount /dev/sdb1 /mnt/mydata
```

---

## ⚠️ Temporary Mount
By default, this mount will **NOT** persist after reboot.

---

## 📌 4️⃣ Ensuring Filesystem is Available After Reboot

To **persist** the mount across reboots, you need to add an entry in **`/etc/fstab`**.

### Step 1: Get the UUID of the Partition
```bash
blkid /dev/sdb1
```
Example output:
```
/dev/sdb1: UUID="abcd-1234-5678-efgh" TYPE="ext4"
```

### Step 2: Add Entry to `/etc/fstab`
```bash
sudo nano /etc/fstab
```
Add this line:
```
UUID=abcd-1234-5678-efgh /mnt/mydata ext4 defaults 0 2
```

### Step 3: Test Before Rebooting
```bash
sudo mount -a
```
→ If no error → configured correctly.

### Step 4: Verify Mount
```bash
df -h | grep /mnt/mydata
```

---

## 📌 5️⃣ Example `/etc/fstab` Entry
```
UUID=abcd-1234-5678-efgh /mnt/mydata ext4 defaults 0 2
```

---

## ✅ Conclusion

| **Action**                | **Command**                                 |
|---------------------------|---------------------------------------------|
| Format partition          | `sudo mkfs.ext4 /dev/sdX1`                  |
| Create mount point        | `sudo mkdir -p /mnt/mydata`                |
| Mount (temporary)         | `sudo mount /dev/sdX1 /mnt/mydata`         |
| Find UUID                 | `blkid /dev/sdX1`                          |
| Configure in `/etc/fstab` | `UUID=xxxx /mnt/mydata ext4 defaults 0 2`  |
| Test                      | `sudo mount -a`                            |
| Verify                    | `df -h` or `mount | grep mydata`           |

→ **After reboot**, filesystem will be automatically mounted.

---
