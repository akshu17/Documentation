# 🐚 Bash Interview Notes (Complete)

---

# 1. What is Bash?

Bash (Bourne Again Shell) is a Unix shell and command-line interpreter.

- Default shell in most Linux systems
- Used for automation and scripting
- Executes system commands

---

# 2. What is a Shell Script?

A shell script is a file containing commands executed by the shell.

Example:

```bash
#!/bin/bash
echo "Hello World"
```

---

# 3. Shebang (#!)

Defines which interpreter should execute the script.

```bash
#!/bin/bash
```

---

# 4. Variables in Bash

## Declare Variable

```bash
name="John"
```

⚠ No spaces around `=`

## Access Variable

```bash
echo $name
```

---

# 5. Special Variables

| Variable | Meaning |
|-----------|----------|
| $0 | Script name |
| $1-$9 | Positional arguments |
| $# | Number of arguments |
| $@ | All arguments |
| $$ | Process ID |
| $? | Exit status of last command |

Example:

```bash
echo "Script name: $0"
echo "Arguments: $@"
```

---

# 6. Exit Status

- 0 → Success
- Non-zero → Failure

Check exit status:

```bash
echo $?
```

---

# 7. If Condition

Basic syntax:

```bash
if [ condition ]
then
    commands
fi
```

Example:

```bash
num=10

if [ $num -gt 5 ]
then
    echo "Greater than 5"
fi
```

---

# 8. Numeric Comparison Operators

| Operator | Meaning |
|------------|----------|
| -eq | Equal |
| -ne | Not equal |
| -gt | Greater than |
| -lt | Less than |
| -ge | Greater or equal |
| -le | Less or equal |

---

# 9. String Comparison

```bash
if [ "$a" = "$b" ]
then
    echo "Equal"
fi
```

---

# 10. File Test Operators

| Option | Meaning |
|---------|----------|
| -f | Regular file |
| -d | Directory |
| -e | Exists |
| -r | Readable |
| -w | Writable |
| -x | Executable |

Example:

```bash
if [ -f file.txt ]
then
    echo "File exists"
fi
```

---

# 11. Loops

## For Loop

```bash
for i in 1 2 3
do
    echo $i
done
```

## While Loop

```bash
while [ condition ]
do
    commands
done
```

---

# 12. Case Statement

```bash
case $var in
    1) echo "One" ;;
    2) echo "Two" ;;
    *) echo "Other" ;;
esac
```

---

# 13. Functions

```bash
myfunc() {
    echo "Hello"
}

myfunc
```

---

# 14. Command Substitution

```bash
today=$(date)
```

Old style:

```bash
today=`date`
```

---

# 15. Redirection

| Operator | Meaning |
|------------|----------|
| > | Overwrite |
| >> | Append |
| < | Input |
| 2> | Error output |
| &> | Redirect all output |

Example:

```bash
echo "Hello" > file.txt
```

---

# 16. Pipe

```bash
ls -l | grep ".txt"
```

---

# 17. File Permissions

```bash
chmod 755 file.sh
```

755 means:
- User → rwx
- Group → r-x
- Others → r-x

---

# 18. Run Script in Background

```bash
./script.sh &
```

---

# 19. Debug Script

```bash
bash -x script.sh
```

Or inside script:

```bash
set -x
```

---

# 20. Practical Example – Even or Odd

```bash
read num

if [ $((num % 2)) -eq 0 ]
then
    echo "Even"
else
    echo "Odd"
fi
```

---

# Quick Revision Summary

- Bash is a shell and scripting language
- Exit status controls conditions
- Use if, loops, functions
- Understand pipes and redirection
- Know file permissions
- Practice scripting problems
