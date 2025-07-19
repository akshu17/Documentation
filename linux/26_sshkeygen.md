# 🔐 SSH and SSH-Keygen Guide

## 📌 What is SSH?

SSH (Secure Shell) is a protocol used to securely connect to remote systems over a network.

---

## 🧰 Generate SSH Key Pair

To generate a new SSH key pair:

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

### Explanation:
- `-t rsa`: Type of key (RSA)
- `-b 4096`: Key length (4096 bits)
- `-C`: Comment, typically your email

### Steps:
1. Run the command.
2. Press `Enter` to accept the default file location (`~/.ssh/id_rsa`).
3. Set a passphrase (optional but recommended).

---

## 📂 Public and Private Keys

- **Private key**: `~/.ssh/id_rsa` → **Keep this secret!**
- **Public key**: `~/.ssh/id_rsa.pub` → Can be shared and added to remote servers

---

## 📥 Add SSH Key to Remote Server

To copy your public key to a remote server:

```bash
ssh-copy-id username@remote_host
```

Or manually:

1. Open the public key:

   ```bash
   cat ~/.ssh/id_rsa.pub
   ```

2. Copy the output and paste it into the remote server's:

   ```
   ~/.ssh/authorized_keys
   ```

---

## 🔐 Connect Using SSH

```bash
ssh username@remote_host
```

---

## 🛠️ Troubleshooting

- Ensure `~/.ssh` and `authorized_keys` have the correct permissions:
  ```bash
  chmod 700 ~/.ssh
  chmod 600 ~/.ssh/authorized_keys
  ```

- Use verbose mode for debugging:
  ```bash
  ssh -v username@remote_host
  ```

---

## 🧠 Tip: Use `ssh-agent` to Cache Your Passphrase

Start the agent and add your key:

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
```

---
