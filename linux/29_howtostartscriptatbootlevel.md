# 🚀 How to Start a Script at Boot on Linux

There are several ways to automatically run a script when the system boots. Below are the most common methods.

---

## 1️⃣ Using `crontab` with `@reboot`

### Steps:

1. Open crontab:
   ```bash
   crontab -e
   ```

2. Add this line at the bottom:
   ```bash
   @reboot /path/to/your/script.sh
   ```

3. Make sure the script is executable:
   ```bash
   chmod +x /path/to/your/script.sh
   ```

> ✅ Works for per-user tasks. The script will run as that user.

---

## 2️⃣ Using `systemd` Service

### Step 1: Create a systemd unit file

```bash
sudo nano /etc/systemd/system/myscript.service
```

### Example Content:

```ini
[Unit]
Description=My Startup Script
After=network.target

[Service]
ExecStart=/path/to/your/script.sh
Restart=on-failure
User=your-username

[Install]
WantedBy=multi-user.target
```

### Step 2: Enable and start the service

```bash
sudo chmod +x /path/to/your/script.sh
sudo systemctl daemon-reexec
sudo systemctl daemon-reload
sudo systemctl enable myscript.service
sudo systemctl start myscript.service
```

> ✅ Most reliable and modern way. Preferred for production systems.

---

## 3️⃣ Add to `/etc/rc.local` (Legacy Method)

1. Edit file:
   ```bash
   sudo nano /etc/rc.local
   ```

2. Add your script above the `exit 0` line:
   ```bash
   /path/to/your/script.sh &
   ```

3. Make it executable:
   ```bash
   sudo chmod +x /etc/rc.local
   ```

> ⚠️ May not be available on all distros (e.g., Ubuntu 18.04+ by default doesn't use it).

---

## 4️⃣ Add to User's `~/.bashrc` or `~/.profile`

Add the script command at the end of:

```bash
nano ~/.bashrc
```

Or:

```bash
nano ~/.profile
```

> ✅ Will run only when the user logs in (not truly boot level).

---

## 🧠 Tips

- Use absolute paths in scripts.
- Redirect logs to file for troubleshooting:
  ```bash
  /path/to/script.sh >> /var/log/myscript.log 2>&1
  ```
- Test the script manually before adding to boot.

---
