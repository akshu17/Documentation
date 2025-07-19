# 🐧 Basic Linux Commands Cheat Sheet

This guide covers essential Linux commands useful for beginners and daily usage.

---

## 📁 File & Directory Commands

```bash
ls             # List files and directories
ls -l          # Long listing format
ls -a          # Show hidden files
pwd            # Print current directory
cd /path/to/dir # Change directory
cd ~           # Go to home directory
mkdir newdir   # Create a new directory
rmdir dir      # Remove an empty directory
rm -r dir      # Remove a directory and its contents
```

---

## 📄 File Operations

```bash
touch file.txt       # Create a new empty file
cp file1 file2       # Copy file1 to file2
mv old.txt new.txt   # Rename or move a file
rm file.txt          # Delete a file
cat file.txt         # View file contents
nano file.txt        # Edit file using nano editor
```

---

## 🔍 Viewing & Searching

```bash
less file.txt        # View large files page by page
head file.txt        # Show first 10 lines
tail file.txt        # Show last 10 lines
tail -f file.txt     # Real-time log viewing
grep "text" file.txt # Search for text in a file
find . -name "*.txt" # Find files by name
```

---

## 🧑‍💻 User & Permission

```bash
whoami               # Show current user
id                   # Show user ID and groups
chmod +x file.sh     # Make a script executable
chown user:group file# Change file ownership
```

---

## 📦 Package Management (Debian/Ubuntu)

```bash
sudo apt update             # Refresh package list
sudo apt upgrade            # Upgrade installed packages
sudo apt install packagename# Install a package
sudo apt remove packagename # Remove a package
```

---

## 🖥️ System Info

```bash
uname -a            # System information
top                 # Real-time system processes
htop                # Enhanced version of top (if installed)
df -h               # Disk usage
free -h             # Memory usage
uptime              # System uptime
```

---

## 🔄 Networking

```bash
ip a                # Show IP addresses
ping google.com     # Ping a server
curl ifconfig.me    # Show public IP
```

---

## 📂 File Compression

```bash
tar -czf archive.tar.gz folder/   # Compress folder
tar -xzf archive.tar.gz           # Extract archive
```

---

## 🔚 Exit Commands

```bash
logout      # Log out of terminal session
exit        # Exit shell
reboot      # Restart system
shutdown now# Shut down immediately
```

---

🧠 **Tip**: Use `man <command>` to get help for any command.

```bash
man ls       # Manual for ls command
```

---
