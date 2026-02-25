1️⃣ What is Bash?
Bash (Bourne Again Shell) is a Unix shell and command-line interpreter.
Default shell in most Linux systems
Used for automation and scripting
Executes commands
2️⃣ What is a Shell Script?
A file containing shell commands executed sequentially.
#!/bin/bash
echo "Hello World"
3️⃣ Shebang (#!)
Defines interpreter for the script.
#!/bin/bash
4️⃣ Variables in Bash
Declare variable
name="John"
⚠ No spaces around =
Access variable
echo $name
5️⃣ Special Variables
Variable	Meaning
$0	Script name
$1-$9	Arguments
$#	Number of arguments
$@	All arguments
$$	Process ID
$?	Exit status
Example:
echo "Script: $0"
echo "Arguments: $@"
6️⃣ Exit Status
0 → Success
Non-zero → Failure
Check exit status:
echo $?
7️⃣ If Condition
if [ condition ]
then
    commands
fi
Example:
num=10

if [ $num -gt 5 ]
then
    echo "Greater than 5"
fi
8️⃣ Numeric Operators
Operator	Meaning
-eq	Equal
-ne	Not equal
-gt	Greater
-lt	Less
-ge	Greater or equal
-le	Less or equal
9️⃣ String Comparison
if [ "$a" = "$b" ]
then
    echo "Equal"
fi
🔟 File Checks
Option	Meaning
-f	Regular file
-d	Directory
-e	Exists
-r	Readable
-w	Writable
-x	Executable
Example:
if [ -f file.txt ]
then
    echo "File exists"
fi
1️⃣1️⃣ Loops
For Loop
for i in 1 2 3
do
    echo $i
done
While Loop
while [ condition ]
do
    commands
done
1️⃣2️⃣ Case Statement
case $var in
    1) echo "One" ;;
    2) echo "Two" ;;
    *) echo "Other" ;;
esac
1️⃣3️⃣ Functions
myfunc() {
    echo "Hello"
}

myfunc
1️⃣4️⃣ Command Substitution
today=$(date)
Old style:
today=`date`
1️⃣5️⃣ Redirection
Operator	Meaning
>	Overwrite
>>	Append
2>	Error
&>	All output
Example:
echo "Hello" > file.txt
1️⃣6️⃣ Pipe
ls -l | grep ".txt"
1️⃣7️⃣ Permissions
chmod 755 file.sh
755 means:
User → rwx
Group → r-x
Others → r-x
1️⃣8️⃣ Run Script in Background
./script.sh &
1️⃣9️⃣ Debug Script
bash -x script.sh
Or inside script:
set -x
2️⃣0️⃣ Practical Example – Even or Odd
read num

if [ $((num % 2)) -eq 0 ]
then
    echo "Even"
else
    echo "Odd"
fi
📝 Quick Revision Summary
Bash is a shell and scripting language
Exit status drives logic
Use if, loops, functions
Know redirection and pipes
Understand permissions
Practice scripting
