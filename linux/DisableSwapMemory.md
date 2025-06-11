# Disabling Swap Memory in Linux

## 1️⃣ What is Swap Memory?

**Swap memory (or swap space)** is a portion of storage (usually a file or dedicated partition on disk) that your operating system uses as "virtual memory" when **RAM** is full. It *swaps* inactive pages from RAM to swap to free up memory for active processes.

### ✅ Why use Swap?
- Prevents apps from crashing when RAM is full.
- Allows you to run more processes than available RAM.
- *BUT*: Swap is **much slower** than RAM (because it’s on disk).

### ⚠️ Problems with Swap:
- **Performance drops** when system heavily uses swap (disk I/O is slower than RAM).
- On SSDs: too much swap usage can **reduce lifespan** of SSD.
- Modern systems with large RAM (>8GB) often **don’t need much swap**.

---

## 2️⃣ How to Disable Swap in Linux

### Temporary Disable (until next reboot)
```bash
sudo swapoff -a
```
- `-a` means *disable all swap* (file or partition).
- Useful for **testing**.

---

### Permanently Disable Swap

#### 1️⃣ Turn off current swap
```bash
sudo swapoff -a
```

#### 2️⃣ Edit `/etc/fstab`
```bash
sudo nano /etc/fstab
```
- Look for any lines referring to **swap**. Example:
```
UUID=xxxxxxxx none swap sw 0 0
```
- **Comment it out** by adding `#` at the beginning:
```
#UUID=xxxxxxxx none swap sw 0 0
```
- Or **remove** the line entirely.

#### 3️⃣ Save the file and exit.

#### 4️⃣ Verify
```bash
cat /proc/swaps
```
- Should be **empty** if everything is correct.

#### 5️⃣ Optional: Remove swap file if you used a file for swap
```bash
sudo rm /swapfile
```
*(Do this only if you know you don’t need it anymore.)*

---

### Check Current Swap Usage
```bash
free -h
```
or
```bash
swapon --show
```

---

## 3️⃣ Advanced (sysctl tuning)

If you don’t want to disable but want to minimize usage:
```bash
sudo sysctl vm.swappiness=10
```
- **0** = avoid using swap unless absolutely necessary
- **60** = default
- **10** = prefer RAM, use swap only when needed

To make it **permanent**:
```bash
echo "vm.swappiness=10" | sudo tee -a /etc/sysctl.conf
```

---

## ✅ Summary Table

| **Action**           | **Command**                    |
|----------------------|--------------------------------|
| Disable temporarily  | `sudo swapoff -a`              |
| Disable permanently  | Edit `/etc/fstab`, remove swap |
| Check swap usage     | `free -h` or `swapon --show`   |
| Adjust swappiness    | `sudo sysctl vm.swappiness=10` |

---

## ❗ When Should You Disable Swap?
- **Development/Testing machines** with **ample RAM**.
- If using SSD and want to **prolong its life**.
- For performance-critical workloads (e.g., databases).

If unsure → **don’t fully disable**, just reduce `swappiness`.

---
