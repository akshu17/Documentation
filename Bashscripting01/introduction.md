# BASH Scripting Introduction — Interview Questions & Answers

## 1. What is Bash?

Bash (Bourne Again Shell) is a command-line interpreter used in Linux and Unix systems.
It allows users to execute commands, automate tasks, and run shell scripts.

---

## 2. What is a Bash Script?

A Bash script is a file containing a sequence of shell commands that are executed automatically.

Example:

```bash
#!/bin/bash
echo "Hello World"
```

---

## 3. What is a Shebang (`#!/bin/bash`)?

It specifies which interpreter should execute the script.
`#!/bin/bash` tells the system to run the script using Bash.

---

## 4. How do you make a script executable?

```bash
chmod +x script.sh
```

---

## 5. How do you run a Bash script?

```bash
./script.sh
```

or

```bash
bash script.sh
```

---

## 6. How do you declare variables in Bash?

```bash
name="John"
echo $name
```

Note: No spaces around `=`.

---

## 7. How do you take user input?

```bash
read name
echo "Hello $name"
```

---

## 8. What are positional parameters?

They store command-line arguments passed to a script.

```bash
echo $1
echo $2
```

---

## 9. How do you write an if statement?

```bash
if [ $a -gt $b ]
then
  echo "A is greater"
fi
```

---

## 10. What are loops in Bash?

Loops repeat commands multiple times.

### For Loop

```bash
for i in 1 2 3
do
  echo $i
done
```

### While Loop

```bash
while [ $count -lt 5 ]
do
  echo $count
  ((count++))
done
```

---

## 11. What is `$?` in Bash?

It stores the exit status of the last executed command.

* `0` → success
* Non-zero → failure

---

## 12. What is `$0` in Bash?

It represents the script name.

---

## 13. How do you write comments in Bash?

```bash
# This is a comment
```

---

## 14. What are functions in Bash?

Functions group reusable commands.

```bash
myfunc() {
  echo "Hello"
}
myfunc
```

---

## 15. What is piping in Bash?

It sends output of one command as input to another.

```bash
ls | grep file
```

---

## 16. Difference between `>` and `>>`

| Symbol | Meaning         |
| ------ | --------------- |
| `>`    | Overwrites file |
| `>>`   | Appends to file |

---

## 17. What is an environment variable?

A system-wide variable available to all processes.

Example:

```bash
echo $HOME
```

---

## 18. How do you debug a Bash script?

```bash
bash -x script.sh
```

---

## 19. Common uses of Bash scripting

* Task automation
* System monitoring
* Backups
* Deployment scripts
* Log processing

---

## 20. One-Line Interview Summary

Bash scripting is used to automate command-line tasks in Linux by writing executable scripts that run sequences of commands.
