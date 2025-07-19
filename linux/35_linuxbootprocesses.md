# 🐧 Linux Boot Process & 20 Essential Linux Commands

---

## 🚀 Linux Boot Process (Step-by-Step)

1. **BIOS/UEFI**  
   - Initializes hardware and passes control to the bootloader.

2. **MBR/GPT**  
   - Contains partition table and points to the bootloader.

3. **Bootloader (e.g., GRUB)**  
   - Loads the Linux kernel into memory.

4. **Kernel**  
   - Initializes system, loads drivers, mounts root filesystem.

5. **init/systemd**  
   - PID 1: Initializes user space and services.

6. **Target/Runlevel**  
   - Reaches the default runlevel or systemd target (e.g., `multi-user.target`).

7. **Login Prompt**  
   - Terminal or GUI login screen appears.

---

## 🧰 20 Essential Linux Commands with Explanation

| Command                | Description                                                                 |
|------------------------|-----------------------------------------------------------------------------|
| `ls`                   | Lists files and directories in the current path                             |
| `cd /path`             | Changes the current working directory                                       |
| `pwd`                  | Prints the current working directory path                                   |
| `mkdir newfolder`      | Creates a new directory                                                      |
| `rm file.txt`          | Deletes a file                                                               |
| `rm -r folder`         | Deletes a directory and its contents recursively                            |
| `cp file1 file2`       | Copies `file1` to `file2`                                                    |
| `mv old new`           | Moves or renames a file or directory                                        |
| `touch file.txt`       | Creates an empty file                                                        |
| `cat file.txt`         | Displays contents of a file                                                  |
| `less file.txt`        | Views file content page by page                                              |
| `head -n 10 file.txt`  | Shows the first 10 lines of a file                                           |
| `tail -n 10 file.txt`  | Shows the last 10 lines of a file                                            |
| `df -h`                | Shows disk space usage in human-readable format                             |
| `du -sh folder/`       | Shows total size of a folder                                                 |
| `top`                  | Real-time system resource usage monitor                                     |
| `ps aux`               | Shows all running processes                                                  |
| `kill PID`             | Sends signal to kill the process with specified PID                         |
| `chmod +x script.sh`   | Makes a script or file executable                                            |
| `sudo`                 | Runs commands with superuser privileges                                     |

---

## 🧠 Tips

- Use `man <command>` for detailed usage (e.g., `man ls`)
- Combine commands with pipes (`|`) and redirection (`>`, `>>`) for powerful scripting

---

> ✅ Mastering these commands and the boot process is foundational for any Linux user or administrator.

---
