# 🔎 How to Check Open Ports on Linux

Open ports are network ports that are listening for incoming connections. Here are multiple ways to check them:

---

## 1️⃣ Using `ss` (Modern replacement for `netstat`)

```bash
sudo ss -tuln
```

### Explanation:
- `-t`: TCP
- `-u`: UDP
- `-l`: Listening ports
- `-n`: Show numeric addresses (no DNS lookup)

---

## 2️⃣ Using `netstat` (Older, may need to install)

```bash
sudo netstat -tuln
```

Or to show processes using ports:

```bash
sudo netstat -tulnp
```

> ❗ Install with:
```bash
sudo apt install net-tools       # Debian/Ubuntu
sudo yum install net-tools       # RHEL/CentOS
```

---

## 3️⃣ Using `lsof` (List open files including ports)

```bash
sudo lsof -i -P -n | grep LISTEN
```

### Explanation:
- `-i`: Show network files
- `-P`: Don't resolve port numbers to names
- `-n`: Don't resolve hostnames

---

## 4️⃣ Using `nmap` (Network scanner)

```bash
sudo nmap -sT -O localhost
```

Or for remote host:

```bash
nmap <ip-address>
```

> ❗ Install with:
```bash
sudo apt install nmap
```

---

## 5️⃣ Using `firewalld` or `ufw` (Check firewall allowed ports)

### For `firewalld`:
```bash
sudo firewall-cmd --list-all
```

### For `ufw`:
```bash
sudo ufw status
```

---

## 🧠 Tip: What is Listening?

A port is **open** if:
- A process is actively **listening** on it.
- It's **not blocked by a firewall**.

---

## 📋 Summary of Tools

| Tool     | Command                            | Notes                  |
|----------|-------------------------------------|-------------------------|
| `ss`     | `ss -tuln`                          | Fast & modern          |
| `netstat`| `netstat -tuln`                     | Legacy, widely known   |
| `lsof`   | `lsof -i -P -n | grep LISTEN`       | Shows process info     |
| `nmap`   | `nmap localhost`                    | Scan from outside      |
| `ufw`    | `ufw status`                        | Shows allowed ports    |
| `firewalld`| `firewall-cmd --list-all`         | Shows open firewall ports |

---

> ✅ Recommended: Use `ss` or `lsof` for local port info, `nmap` for remote scans.

---
