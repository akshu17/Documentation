# 💾 How to Find Available Storage on a Linux Server

Monitoring disk usage is crucial to avoid running out of storage on your Linux server. Below are essential commands to check available storage.

---

## ✅ Using `df` Command (Disk Free)

```bash
df -h
```

| Option | Description                   |
| ------ | ----------------------------- |
| `-h`   | Human-readable format (MB/GB) |

**Example Output:**

```plaintext
Filesystem      Size  Used Avail Use% Mounted on
/dev/xvda1       50G   15G   33G  31% /
tmpfs           7.8G     0  7.8G   0% /dev/shm
```

* **Size**: Total size of the filesystem
* **Used**: Used space
* **Avail**: Available free space
* **Mounted on**: Where the filesystem is attached

---

## ✅ Using `du` Command (Disk Usage)

### To check size of a directory:

```bash
du -sh /path/to/directory
```

| Option | Description                   |
| ------ | ----------------------------- |
| `-s`   | Summarize total               |
| `-h`   | Human-readable format (MB/GB) |

Example:

```bash
du -sh /var/log
```

---

## ✅ Using `ls` Command for File Sizes

```bash
ls -lh /path/to/directory
```

* Lists files along with their sizes in a human-readable format.

---

## ✅ Using `ncdu` for Interactive Directory Usage (Recommended for Cleanup)

Install `ncdu`:

```bash
sudo apt install ncdu      # Debian/Ubuntu
sudo yum install ncdu      # RHEL/CentOS
```

Run:

```bash
ncdu /
```

* Interactive, visual disk usage explorer.

---

## ✅ Example Summary of Commands

| Command       | Purpose                             |
| ------------- | ----------------------------------- |
| `df -h`       | Disk space usage of all filesystems |
| `du -sh /dir` | Size of specific directory          |
| `ls -lh /dir` | File sizes in directory             |
| `ncdu /`      | Interactive, visual usage explorer  |

---

## 🗨️ Quote

> **"Storage is like time — you only miss it when it’s gone."**

---

## ✅ Conclusion

For overall storage:

```bash
df -h
```

For specific folder analysis:

```bash
du -sh /path/to/folder
```

For interactive cleanup (recommended):

```bash
ncdu /
```

---
