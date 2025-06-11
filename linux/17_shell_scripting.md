# Understanding `$?`, `$*`, and `$0` in Shell Scripting

---

## 📌 1️⃣ `$?` — Exit Status of Last Command

- Stores the **exit status** of the **last executed command**.
- `0` → **Success**
- Non-zero → **Failure** (error codes)

**Example:**
```bash
ls /tmp
echo $?   # 0 if successful

ls /nonexistent
echo $?   # Non-zero (e.g., 2) if failed
```

---

## 📌 2️⃣ `$*` — All Script Arguments

- Represents **all the positional parameters** (*arguments*) **as a single word (string)**.

**Example usage:**
```bash
#!/bin/bash
echo "Arguments: $*"
```
```bash
./script.sh one two three
```
**Output:**
```
Arguments: one two three
```

**Note:** If enclosed in double quotes (`""`), it treats **all arguments as one string**.
```bash
echo "$*"
```
Output: `"one two three"`

---

## 📌 3️⃣ `$0` — Script Name

- Holds the **name of the script** or the **shell command used to invoke the script**.

**Example:**
```bash
#!/bin/bash
echo "Script name: $0"
```
```bash
./script.sh
```
Output:
```
Script name: ./script.sh
```

---

## ✅ Summary Table

| **Variable** | **Meaning**                           |
|--------------|---------------------------------------|
| `$?`         | Exit status of the last command       |
| `$*`         | All script arguments (single string)  |
| `$0`         | Name of the script                    |

---
