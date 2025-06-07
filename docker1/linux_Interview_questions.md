# Linux Administration Interview Questions and Answers

### 1. How do you disable swap memory through command line and ensure it is not added to the system?

**Answer:**
Swap memory can be disabled temporarily using the command:

```bash
swapoff -a
```

This turns off all swap partitions immediately. To ensure swap does not get enabled again on reboot, you need to remove or comment out any swap entries in the `/etc/fstab` file. This file contains information about disk partitions and mount points that are mounted at boot time.

### 2. How to make sure that file system doesn’t get mounted upon the reboot?

**Answer:**
To prevent a file system from being mounted on reboot, you should remove or comment out its entry in `/etc/fstab`. This file tells the OS what to mount during the boot process. If a file system is listed here, it will automatically be mounted.

### 3. Have you created a file system and how do you ensure those file systems are available after reboot?

**Answer:**
Yes. After creating a file system using commands like `mkfs.ext4 /dev/xvdf`, it should be mounted using `mount`. To ensure it persists across reboots, add an entry to `/etc/fstab` using either the device path or the UUID obtained using `blkid`.

### 4. After mounting EBS to instance, will it still be available after reboot?

**Answer:**
By default, mounting is not persistent. To make EBS volumes available after reboot, they should be added to `/etc/fstab` with the correct mount point, file system type, and options. Make sure to use UUID for reliability.

### 5. What init levels are implemented in Linux?

**Answer:**
Runlevels determine the state of the machine after boot. Common runlevels include:

* 0: Halt
* 1: Single-user mode (maintenance)
* 2: Multi-user without networking
* 3: Multi-user with networking (default for servers)
* 4: Undefined (custom)
* 5: GUI mode (default for desktops)
* 6: Reboot
  Modern systems use systemd instead of traditional SysV init.

### 6. Command to check the load of the system?

**Answer:**

```bash
uptime
```

This shows the system uptime, number of users, and system load averages over the last 1, 5, and 15 minutes. Load average indicates how many processes are waiting to be executed.

### 7. Command to check usage of memory/RAM of the system?

**Answer:**

```bash
free -h
```

Displays the total, used, and free memory in a human-readable format. Also shows buffer and cache usage.

### 8. Command to check how many CPU cores are there in the system?

**Answer:**

```bash
grep -c ^processor /proc/cpuinfo
```

This command counts the number of logical CPU cores listed in `/proc/cpuinfo`.

### 9. Suppose I have 100 servers, each with username and password. How can I install packages in all those servers remotely without logging in, using a shell script?

**Answer:**
Use a loop with `sshpass` or public key authentication. Here's an example using a list of IPs:

```bash
for server in $(cat servers.txt); do
  sshpass -p 'password' ssh user@$server "sudo apt install -y packagename"
done
```

For a more secure setup, use SSH key-based authentication.

### 10. Using top command, how will you control all running processes?

**Answer:**
When inside `top`, you can:

* Press `k` to kill a process by PID.
* Use `r` to renice a process (change priority).
* Press `Shift + P` to sort by CPU usage.

### 11. Write a shell script to print all alternate lines

**Answer:**

```bash
#!/bin/bash
awk 'NR % 2 == 1' filename
```

This script uses `awk` to print every odd-numbered line (i.e., alternate lines).

### 12. Script to sort all files in logs and sort them according to top memory consumption and copy it to another file

**Answer:**

```bash
ps aux --sort=-%mem > sorted_logs.txt
```

This command lists all running processes sorted by memory usage and saves them to a file.

### 13. Explain runlevel commands

**Answer:**

* `runlevel`: Shows the previous and current runlevel.
* `who -r`: Displays the current runlevel.
  Note: With systemd, runlevels are replaced by targets (e.g., `multi-user.target`).

### 14. How do you find complete details of the Linux version you are using?

**Answer:**

```bash
uname -a
cat /etc/os-release
```

These commands show the kernel version, distribution name, version number, and more.

### 15. What does `ps -ef` do?

**Answer:**
Lists all running processes in full-format, showing PID, PPID, user, and command.

### 16. What does `kill -9 processname` do?

**Answer:**
Kills the process forcefully. You generally need the PID:

```bash
kill -9 <PID>
```

### 17. What are `$?`, `$*`, and `$0`?

**Answer:**

* `$?`: Exit code of the last executed command.
* `$*`: All script arguments as a single word.
* `$0`: Name of the script.

### 18. What is SSH?

**Answer:**
SSH (Secure Shell) is a protocol for secure remote login and command execution.

```bash
ssh user@host
```

### 19. What are the port numbers for SSH, HTTP, and HTTPS?

**Answer:**

* SSH: 22
* HTTP: 80
* HTTPS: 443

### 20. How to list the processes running?

**Answer:**

```bash
ps aux
```

Lists all running processes with details.

### 21. How to login to EC2 if PEM key is lost?

**Answer:**

* Stop the instance
* Detach root volume
* Attach to another instance
* Mount and modify `.ssh/authorized_keys`
* Reattach volume to original instance and start

### 22. How to check memory in Linux server?

**Answer:**

```bash
free -h
vmstat
```

Shows RAM usage, swap, and memory buffers.

### 23. How to get the IP address of server?

**Answer:**

```bash
ip a
hostname -I
```

### 24. How do I find available storage on the server using Linux commands?

**Answer:**

```bash
df -h
```

Displays file system disk usage in human-readable form.

### 25. How to identify/find files which are more than 10GB in size?

**Answer:**

```bash
find / -type f -size +10G
```

### 26. What is the difference between Git merge and rebase?

**Answer:**

* `merge`: Combines two branches preserving history.
* `rebase`: Rewrites commit history for a linear history.

### 27. What is `ssh-keygen`?

**Answer:**
Used to generate SSH key pairs for passwordless login.

```bash
ssh-keygen
```

### 28. Difference between CMD, ENTRYPOINT, and RUN in Docker?

**Answer:**

* CMD: Sets default command.
* ENTRYPOINT: Sets fixed command, allows arguments.
* RUN: Executes at build time to modify the image.

### 29. Basic Linux Commands

**Answer:**
Examples:

```bash
ls, cd, cp, mv, rm, mkdir, chmod, chown, ps, top, df, du, tar
```

### 30. What action do you take if the Linux server goes down?

**Answer:**

* Check uptime/logs: `journalctl -xe`, `dmesg`
* Verify services: `systemctl status`
* Check disk/memory usage: `df -h`, `free -h`
* Reboot if safe

### 31. How to start a script at boot level?

**Answer:**

* Add to `/etc/rc.local`
* Or create a systemd service and enable it

### 32. How to start a service at boot level?

**Answer:**

```bash
systemctl enable servicename
```

### 33. What is the way to run script in background?

**Answer:**

```bash
./script.sh &
```

This allows the script to run in background.

### 34. How do you check open ports?

**Answer:**

```bash
ss -tuln
netstat -tuln
```

### 35. How do you see the number of arguments in a script?

**Answer:**

```bash
echo $#
```

Displays the number of positional parameters.

### 36. What is the `k` statement in shell script?

**Answer:**
No standard `k` in bash. May refer to `kill` in `top`.

### 37. How to establish password-less SSH connection?

**Answer:**

```bash
ssh-keygen
ssh-copy-id user@remote
```

This copies your public key to the remote machine.

### 38. Shell script for prime numbers in a given range

**Answer:**
Prints all prime numbers between 2 and 50.

```bash
#!/bin/bash
for ((num=2; num<=50; num++))
do
  prime=1
  for ((i=2; i<num; i++))
  do
    if (( num%i == 0 )); then
      prime=0
      break
    fi
  done
  if (( prime == 1 )); then
    echo $num
  fi
done
```

### 39. Explain Linux boot process

**Answer:**

1. BIOS: Initializes hardware
2. MBR: Loads bootloader (GRUB)
3. GRUB: Loads Linux kernel
4. Kernel: Initializes devices and mounts root
5. init/systemd: Starts user-space processes
6. Services/Targets: Reaches desired state

### 40. Linux commands related to memory and system RAM

**Answer:**

```bash
free -h
vmstat
top
htop
cat /proc/meminfo
```

### 41. Which scripting language are you comfortable with?

**Answer:**
This is a personal choice. Example: Bash and Python.

### 42. Script to find the port number of a service

**Answer:**

```bash
ss -tulnp | grep <service_name>
```

### 43. What are namespaces in Linux?

**Answer:**
Namespaces isolate system resources (PID, mount, network, etc.) and are used in containers like Docker.

### 44. Explain the Linux booting process

**Answer:**
(Refer to question 39)

### 45. Types of Linux OS used and package manager for Ubuntu

**Answer:**
Examples of OS: Ubuntu, CentOS, RHEL, Debian
Package manager for Ubuntu: `apt`

### 46. What are `$?` and `$!`?

**Answer:**

* `$?`: Exit status of last command (0 = success)
* `$!`: PID of the last background command
