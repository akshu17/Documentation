# 🔐 How to Establish a Password-less SSH Connection in Linux

Password-less SSH allows you to log in to a remote server **without entering a password**, using **SSH key-based authentication**.

---

## ✅ Step-by-Step Guide

### 1️⃣ Generate SSH Key Pair (On Local Machine)

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

- Press `Enter` to accept the default path (`~/.ssh/id_rsa`)
- Optionally enter a **passphrase** (or press Enter for no passphrase)

### Output:
- **Private key**: `~/.ssh/id_rsa`
- **Public key**: `~/.ssh/id_rsa.pub`

> 🧠 Never share your private key!

---

### 2️⃣ Copy the Public Key to the Remote Server

```bash
ssh-copy-id user@remote_host
```

Or manually:

```bash
cat ~/.ssh/id_rsa.pub | ssh user@remote_host 'mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys'
```

> 🔐 Make sure `.ssh` directory and `authorized_keys` file have correct permissions on the remote host:

```bash
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

---

### 3️⃣ Test the Connection

```bash
ssh user@remote_host
```

You should be logged in **without being prompted for a password**.

---

## 🧪 Example

```bas
