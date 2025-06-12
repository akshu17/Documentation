# 🔐 How to Access an EC2 Instance if PEM Key is Lost

Losing the PEM key to your EC2 instance **does not mean the instance is lost**, but it requires a workaround to regain access. Below are **methods** you can use:

---

## ✅ Method 1: Using EC2 Instance Connect (For Amazon Linux/Ubuntu)

If **EC2 Instance Connect** is enabled and supported for your instance type and AMI:

1. Go to **AWS Console → EC2 → Instances**.
2. Select the instance.
3. Click **Connect** → **EC2 Instance Connect (browser-based SSH)**.
4. Login without a PEM file directly from the browser.

> ⚠️ **Note**: This works if:
>
> * Instance Connect is enabled in the **instance settings**.
> * **Inbound rules** allow SSH (port 22).

---

## ✅ Method 2: Create a New Key Pair and Attach to the Instance

If EC2 Instance Connect is **not available**, follow these steps:

### 1️⃣ Create a New PEM Key

1. Go to **EC2 → Key Pairs → Create key pair**.
2. Save the new `.pem` file securely.

### 2️⃣ Stop the Instance

* **Go to EC2 → Instances → Select Instance → Stop**

### 3️⃣ Detach Root Volume

* **Go to EC2 → Elastic Block Store → Volumes**
* Find the **root volume** attached to your instance.
* **Detach** it.

### 4️⃣ Attach Root Volume to Another EC2 Instance

* Launch a **temporary EC2 instance** (same Availability Zone).
* Attach the **detached volume** to this new instance.

### 5️⃣ Mount and Modify SSH Config

* SSH into the temporary EC2 using its key.
* Mount the attached volume:

```bash
sudo mkdir /mnt/temp
sudo mount /dev/xvdf1 /mnt/temp    # Adjust device name if necessary
```

* Navigate to the `.ssh/authorized_keys`:

```bash
cd /mnt/temp/home/ec2-user/.ssh/
```

* Add **new public key** (from the new PEM file):

```bash
echo 'ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQE...' >> authorized_keys
```

* Unmount and detach the volume:

```bash
sudo umount /mnt/temp
```

### 6️⃣ Attach Volume Back and Start the Instance

* Attach the volume back to the original EC2 **as root (/dev/xvda or /dev/sda1)**.
* Start your instance.
* SSH using your **new PEM file**:

```bash
ssh -i "new-key.pem" ec2-user@<public-ip>
```

---

## ✅ Method 3: Backup Data & Recreate

If you don’t want to go through attaching/detaching:

1. Create an **AMI** of the instance.
2. Launch a **new instance** from that AMI with a **new PEM key**.
3. Data and configuration remain as in the original.

---

## ✅ Prevention Tips for the Future

* Store PEM keys **securely** in a password manager or secure vault.
* **Add multiple SSH public keys** in advance to your EC2 instances.
* Enable **EC2 Instance Connect** if possible.
* Create **AMI backups regularly** for critical instances.

---

## 🗨️ Quote

> **"Losing the key is a mistake, but recovering access is just a process."**

---

## ✅ Conclusion

| Situation             | Solution                         |
| --------------------- | -------------------------------- |
| EC2 Instance Connect  | Connect from AWS Console         |
| Lost PEM, need access | New key → Attach volume → Edit   |
| Want simpler recovery | Create AMI → Launch new instance |

---
