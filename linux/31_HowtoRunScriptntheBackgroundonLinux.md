# 🧠 How to Run a Script in the Background on Linux

Running a script in the background allows the terminal to remain free while the script continues to execute.

---

## 1️⃣ Using `&` (Ampersand)

```bash
./yourscript.sh &
```

- Runs the script in the background.
- Output still goes to the terminal.

> ❗ If the terminal closes, the script will stop unless protected by `nohup` or `screen`.

---

## 2️⃣ Using `nohup` (No Hangup)

```bash
nohup ./yourscript.sh &
```

- Prevents the script from terminating when the terminal closes.
- Output is saved to `nohup.out` by default.

### Example:

```bash
nohup ./backup.sh > backup.log 2>&1 &
```

> ✅ Recommended for long-running scripts.

---

## 3️⃣ Using `disown` (After Running)

```bash
./yourscript.sh &
disown
```

- Removes the script from the shell's job table.
- Prevents the shell from sending SIGHUP (hangup) when you log out.

---

## 4️⃣ Using `screen` (Virtual Terminal Session)

Install screen (if not already):

```bash
sudo apt install screen    # Debian/Ubuntu
sudo yum install screen    # RHEL/CentOS
```

### Start a session:
```bash
screen -S myscript
```

Then run your script:

```bash
./yourscript.sh
```

Detach with:
```
Ctrl + A then D
```

Reattach anytime:

```bash
screen -r myscript
```

---

## 5️⃣ Using `tmux` (Terminal Multiplexer)

```bash
tmux new -s mysession
./yourscript.sh
```

Detach with:
```
Ctrl + B then D
```

Reattach:

```bash
tmux attach -t mysession
```

---

## 🧹 Optional: Kill a Background Script

Find its PID:

```bash
ps aux | grep yourscript.sh
```

Kill it:

```bash
kill <PID>
```

---

## 📝 Summary

| Method      | Survives Logout | Easy to Reconnect | Logs Output |
|-------------|------------------|-------------------|--------------|
| `&`         | ❌               | ❌
