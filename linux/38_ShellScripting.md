# 💡 `$?` and `$!` in Shell Scripting

In Linux shell (bash), `$?` and `$!` are **special variables** used frequently in scripting and debugging.

---

## ✅ `$?` — Exit Status of Last Command

- Returns the **exit code** of the **most recently executed command**.
- `0` = Success  
- Non-zero = Error

### 📌 Example:

```bash
ls /tmp
echo $?    # Will print 0 (success)

ls /nonexistent
echo $?    # Will print non-zero (e.g., 2 - No such file)
```

### ✅ Use Case:
Check if a command ran successfully.

```bash
if [ $? -eq 0 ]; then
  echo "Command succeeded"
else
  echo "Command failed"
fi
```

---

## ✅ `$!` — PID of Last Background Process

- Returns the **process ID (PID)** of the most recent command run **in the background**.

### 📌 Example:

```bash
sleep 30 &
echo $!     # Prints PID of the 'sleep' process
```

### ✅ Use Case:
Track or monitor background jobs.

```bash
sleep 60 &
pid=$!
echo "Waiting on process $pid..."
wait $pid
echo "Background task done"
```

---

## 🔁 Summary Table

| Variable | Meaning                          | Example Use                  |
|----------|----------------------------------|------------------------------|
| `$?`     | Exit status of last command      | `if [ $? -eq 0 ]; then ...` |
| `$!`     | PID of last background process   | `kill $!`                    |

---

> 🧠 These variables are **essential** in automation, process control, and error handling in bash scripts.
