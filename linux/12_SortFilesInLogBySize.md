# Shell Script to Sort Files in `logs/` by Size and Save to Another File

---

## ✅ Script

```bash
#!/bin/bash

# Directory containing log files
LOG_DIR="logs"
OUTPUT_FILE="sorted_logs_by_size.txt"

# Check if directory exists
if [ ! -d "$LOG_DIR" ]; then
    echo "Directory $LOG_DIR does not exist!"
    exit 1
fi

# List files with sizes, sort by size (largest first), save to OUTPUT_FILE
du -ah "$LOG_DIR" | sort -rh > "$OUTPUT_FILE"

echo "Sorted list of files by size saved to $OUTPUT_FILE"
```

---

## 📌 Explanation
- `du -ah logs/` → Displays size of each file with human-readable format
- `sort -rh` → Sorts by **human-readable numbers** in **reverse order** (largest first)
- `> sorted_logs_by_size.txt` → Writes output to the file

Example output in `sorted_logs_by_size.txt`:
```
120M logs/application.log
32M logs/error.log
4.0K logs/debug.log
```

---

## ✅ Example Usage

```bash
chmod +x sort_logs_by_size.sh
./sort_logs_by_size.sh
```

---
