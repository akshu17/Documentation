# 🚨 Linux Server Down — Action Plan

When a Linux server goes down, the goal is to **identify**, **recover**, and **prevent**. Here’s a step-by-step approach:

---

## 1️⃣ Initial Checks

### ✅ Check if the server is really down
- **Ping the server**:
  ```bash
  ping <server_ip>
  ```
- **Try SSH**:
  ```bash
  ssh user@<server_ip>
  ```

---

## 2️⃣ Remote Access Fails?

### 🔁 Try Console or IPMI (Out-of-Band Management)
If SSH/ping fails:
- Use a **cloud provider's console access** (AWS, GCP, Azure)
- Use **iDRAC**, **ILO**, or **IPMI** for physical servers

---

## 3️⃣ Server is Down — Restart

### 🔧 Reboot via:
- Cloud console (e.g., AWS EC2 -> Actions -> Reboot)
- Remote BMC tools (iDRAC/iLO)
- Power cycle if on-premise

---

## 4️⃣ After Reboot — Check System Logs

```bash
sudo journalctl -xe         # System logs
dmesg                       # Kernel ring buffer
sudo tail -n 100 /var/log/syslog   # Debian-based
sudo tail -n 100 /var/log/messages # RHEL-based
```

Look for:
- Kernel panics
- Disk errors
- Memory issues
- OOM (Out of Memory) kills

---

## 5️⃣ Check Resource Usage

```bash
top
htop
df -h        # Disk usage
free -h      # Memory
uptime       # Load average
```

---

## 6️⃣ Check Services

```bash
systemctl status
systemctl --failed
```

Restart critical services if needed:

```bash
sudo systemctl restart nginx
sudo systemctl restart mysql
```

---

## 7️⃣ Network Check

```bash
ip a
ip route
ping 8.8.8.8
curl http://localhost
```

Check firewall rules:

```bash
sudo iptables -L
sudo ufw status
```

---

## 8️⃣ Disk and File System Check

Check disk health:

```bash
sudo smartctl -a /dev/sda
```

Check and repair file systems (if necessary):

```bash
sudo fsck /dev/sdX
```

---

## 9️⃣ Security/Compromise Checks (if suspicious)

```bash
last
who
w
cat /etc/passwd
sudo netstat -tulnp
```

Look for:
- Unknown users or processes
- Unusual open ports

---

## 🔟 Document & Prevent

- Create an **incident report**
- Set up monitoring/alerting (e.g., Nagios, Zabbix, Prometheus, CloudWatch)
- Implement redundancy (e.g., load balancers, failover)

---

> 🧠 **Tip**: Always have regular backups and test restore procedures!

---
