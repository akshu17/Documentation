# Mounting EBS to EC2 Instance — Persistence After Reboot

## ✅ After Mounting EBS to an EC2 Instance — Will It Still Be Available After Reboot?

### 📌 Short Answer
- **The EBS volume itself remains attached to the EC2 instance** after reboot.
- However, **the filesystem mount may not persist** unless you configure it properly in **`/etc/fstab`** or use cloud-init/systemd scripts.

---

## 📌 Understanding the Behavior

### 1️⃣ **EBS Attachment**
- When you **attach** an EBS volume to an EC2 instance, **it stays attached** *unless* you manually detach it or terminate the instance **without preserving the volume**.
- On reboot (soft/hard), **the attachment persists.**

→ Confirm attached volumes in **AWS Console → EC2 → Volumes → Attached Instances**.

---

### 2️⃣ **Filesystem Mounting**
Even though the device (e.g., `/dev/xvdf`) is **attached**, **it won’t automatically mount** to your desired directory **after reboot** *unless* configured.

---

## ✅ Ensuring EBS Mount Persists After Reboot

### Step 1️⃣ — **Get the UUID of the EBS Volume Partition**
```bash
sudo blkid
```
Example output:
```
/dev/xvdf1: UUID="abcd-1234-5678-efgh" TYPE="ext4"
```

### Step 2️⃣ — **Create a Mount Point**
```bash
sudo mkdir -p /data
```

### Step 3️⃣ — **Add to `/etc/fstab`**
```bash
sudo nano /etc/fstab
```
Example entry:
```
UUID=abcd-1234-5678-efgh /data ext4 defaults,nofail 0 2
```

#### Why `nofail`?
- If the EBS volume is temporarily unavailable or detached, using `nofail` prevents the system from dropping into maintenance mode during boot.

---

### Step 4️⃣ — **Test the Setup**
```bash
sudo mount -a
```
Check:
```bash
df -h | grep /data
```

### Step 5️⃣ — **Reboot and Verify**
```bash
sudo reboot
```
Post reboot:
```bash
df -h | grep /data
```
→ Should show mounted volume.

---

## ⚠️ What Happens on Termination?
- **If “Delete on Termination” is set to `true` for the EBS volume**, it will be **deleted** when the EC2 instance is terminated.
- **If “Delete on Termination” is set to `false` (recommended for persistent storage),** it survives instance termination.

Check and modify this setting via **AWS Console → EC2 → Volumes → Actions → Modify Volume**.

---

## 📌 Summary Table

| **Aspect**                  | **Behavior**                                             |
|-----------------------------|--------------------------------------------------------|
| EBS volume attachment       | ✅ Persists after reboot                               |
| Filesystem mount            | ❗ **Needs `/etc/fstab` configuration to persist**     |
| `nofail` usage              | ✅ Prevents boot failures if volume temporarily absent |
| Volume after termination    | ⚠️ Depends on "Delete on Termination" setting         |

---
