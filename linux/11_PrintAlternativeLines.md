# Shell Script to Print Alternate Lines from a File

---

## ✅ Script

```bash
#!/bin/bash

# Usage: ./alternate_lines.sh <filename>

if [ $# -eq 0 ]; then
    echo "Usage: $0 <filename>"
    exit 1
fi

FILE="$1"

# Print alternate lines: odd-numbered lines (1,3,5,...)
awk 'NR % 2 == 1' "$FILE"
```

---

## 📌 Explanation
- `NR` → Current line number in `awk`
- `NR % 2 == 1` → Selects **odd-numbered lines** (1st, 3rd, 5th, etc.)
- To print **even-numbered lines** instead:
```bash
awk 'NR % 2 == 0' "$FILE"
```

---

## ✅ Example Usage
```bash
chmod +x alternate_lines.sh
./alternate_lines.sh myfile.txt
```

---
