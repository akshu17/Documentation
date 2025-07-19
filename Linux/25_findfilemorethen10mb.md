# How to Find Files Larger Than 10GB

To identify files larger than **10GB**, you can use command-line tools depending on your operating system. Below are methods for **Linux/macOS** and **Windows**.

---

## 🐧 Linux / macOS

Use the `find` command:

```bash
find /path/to/search -type f -size +10G
```

- `/path/to/search`: Directory to start searching (e.g., `/`, `/home`, etc.)
- `-type f`: Finds only files (not directories)
- `-size +10G`: Finds files larger than 10 Gigabytes

### Example:
```bash
find / -type f -size +10G 2>/dev/null
```

> **Note:** `2>/dev/null` suppresses permission denied errors.

---

## 🪟 Windows (Using PowerShell)

Use the `Get-ChildItem` command:

```powershell
Get-ChildItem -Path "C:\path\to\search" -Recurse -File | Where-Object { $_.Length -gt 10GB }
```

- `-Recurse`: Search all subdirectories  
- `-File`: Include only files  
- `$_ .Length -gt 10GB`: Filter files larger than 10GB

### Example:
```powershell
Get-ChildItem -Path "C:\" -Recurse -File | Where-Object { $_.Length -gt 10GB }
```

> **Note:** Running this as Administrator may give better access across folders.

---

## 🔍 Tips

- Always replace `/path/to/search` or `C:\path\to\search` with your actual directory.
- Use output redirection or logging if the result is too large:
  - Linux: `... > large_files.txt`
  - Windows: `... | Out-File large_files.txt`

---
