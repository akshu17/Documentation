# 🌐 How to Get the IP Address of a Linux Server

Knowing the IP address of your server is essential for networking and remote access. Below are various ways to check it.

---

## ✅ Using `ip addr` Command (Recommended)

```bash
ip addr show
```

Or, for a specific interface (like eth0):

```bash
ip addr show eth0
```

**Example Output:**

```plaintext
inet 192.168.1.100/24 brd 192.168.1.255 scope global eth0
```

* **inet**: IPv4 address
* **inet6**: IPv6 address

---

## ✅ Using `hostname -I`

```bash
hostname -I
```

* Displays all assigned **IP addresses** (IPv4 and IPv6).

---

## ✅ Using `ifconfig` (Older Systems)

```bash
ifconfig
```

> ⚠️ **Note**: `ifconfig` is deprecated on newer Linux distros. Use `ip addr` instead.

Install on Debian/Ubuntu if needed:

```bash
sudo apt install net-tools
```

---

## ✅ Get Public IP Address (External IP)

### 1️⃣ Using `curl` with Public Services:

```bash
curl ifconfig.me
```

or

```bash
curl icanhazip.com
```

### 2️⃣ Using Dig (If Available):

```bash
dig +short myip.opendns.com @resolver1.opendns.com
```

---

## ✅ Example Summary of Commands

| Command            | Purpose           |
| ------------------ | ----------------- |
| `ip addr show`     | Show all IPs      |
| `hostname -I`      | Quick list of IPs |
| `curl ifconfig.me` | Get **public** IP |
| `ifconfig`         | Legacy command    |

---

## 🗨️ Quote

> **"Your IP is your identity on the network — know it, guard it."**

---

## ✅ Conclusion

For **internal/private IP**:

```bash
ip addr show
```

For **public/external IP**:

```bash
curl ifconfig.me
```

Use the method that best suits your environment.

---
