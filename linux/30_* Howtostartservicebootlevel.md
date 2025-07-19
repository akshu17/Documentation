# 🛠️ How to Start a Service at Boot Level on Linux

To ensure a service starts automatically at boot, use `systemd`. Below are the steps for enabling, disabling, checking, and managing services at boot.

---

## ✅ Enable a Service at Boot

```bash
sudo systemctl enable <service-name>
```

### Example:
```bash
sudo systemctl enable nginx
```

This creates a symbolic link in the appropriate systemd directory to start the service at boot.

---

## ▶️ Start the Service Immediately (Optional)

```bash
sudo systemctl start <service-name>
```

### Example:
```bash
sudo systemctl start nginx
```

---

## 🔍 Check If a Service is Enabled at Boot

```bash
systemctl is-enabled <service-name>
```

### Example:
```bash
systemctl is-enabled nginx
```

> Output will be `enabled`, `disabled`, `static`, or `masked`.

---

## 🚫 Disable a Service from Starting at Boot

```bash
sudo systemctl disable <service-name>
```

### Example:
```bash
sudo systemctl disable nginx
```

---

## 📋 View All Enabled Services at Boot

```bash
systemctl list-unit-files --type=service --state=enabled
```

---

## 🧠 Notes

- **systemd** services typically have unit files in `/etc/systemd/system/` or `/lib/systemd/system/`.
- Services are usually named with `.service` at the end (e.g., `nginx.service`), but you can omit the suffix when using `systemctl`.

---

## 🧪 Example: Creating Your Own Boot-Level Service

1. Create a service file:

```bash
sudo nano /etc/systemd/system/myscript.service
```

2. Example content:

```ini
[Unit]
Description=Run My Script at Boot
After=network.target

[Service]
ExecStart=/usr/local/bin/myscript.sh
Restart=always
User=root

[Install]
WantedBy=multi-user.target
```

3. Enable it:

```bash
sudo chmod +x /usr/local/bin/myscript.sh
sudo systemctl daemon-reload
sudo systemctl enable myscript.service
sudo systemctl start myscript.service
```

---

> ✅ Recommended method: Always prefer `systemd` over legacy methods like `rc.local` or `init.d`.

---
