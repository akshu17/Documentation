# 🔢 How to See the Number of Arguments in a Bash Script

In a Bash script, the number of arguments passed is stored in the special variable: `$#`

---

## 🧪 Example Script

```bash
#!/bin/bash

echo "Number of arguments passed: $#"
```

### Save as:

```bash
count_args.sh
```

### Make it executable:

```bash
chmod +x count_args.sh
```

### Run it with some arguments:

```bash
./count_args.sh one two three
```

### Output:

```
Number of arguments passed: 3
```

---

## 🧠 Related Special Variables

| Variable | Description                      |
|----------|----------------------------------|
| `$#`     | Number of arguments              |
| `$0`     | Script name                      |
| `$1`, `$2`, ... | First, second argument, etc. |
| `$@`     | All arguments (individually quoted) |
| `$*`     | All arguments (as single string) |

---

## ✅ Tip

You can use this in scripts to validate arguments:

```bash
if [ $# -lt 2 ]; then
  echo "Usage: $0 arg1 arg2"
  exit 1
fi
```

---

> 💡 `$#` is a simple and powerful way to ensure correct input to your Bash scripts.
