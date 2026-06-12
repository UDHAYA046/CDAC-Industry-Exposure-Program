# Session 4 – Shell Scripting Fundamentals

**Date:** 12 June 2026
**Duration:** 9:30 AM – 11:45 AM
**Course:** CDAC Industry Exposure Program – Cybersecurity

---

# Overview

The third session focused on Linux Shell Scripting using Bash. The session introduced operators, variables, user input handling, conditional statements, loops, command substitution, pipes, and basic automation concepts.

Shell scripting enables users to automate repetitive tasks, execute multiple commands sequentially, perform decision-making operations, and create simple administrative or cybersecurity tools.

---

# Introduction to Shell Scripting

A shell script is a text file containing Linux commands that are executed sequentially by the shell interpreter.

Example:

```bash
#!/bin/bash

echo "Hello World"
```

The first line:

```bash
#!/bin/bash
```

is called the **Shebang** and specifies that the script should be executed using the Bash shell.

---

# Variables in Shell Scripting

Variables are used to store data.

Example:

```bash
name="CDAC"
echo $name
```

Output:

```text
CDAC
```

---

# Taking User Input

The `read` command is used to accept input from the user.

Example:

```bash
read -p "Enter your name: " name
echo "Hello $name"
```

---

# Operators in Shell Scripting

Operators are symbols used to perform operations on variables and values.

---

## Arithmetic Operators

Used for mathematical calculations.

| Operator | Description    |
| -------- | -------------- |
| +        | Addition       |
| -        | Subtraction    |
| *        | Multiplication |
| /        | Division       |
| %        | Modulus        |

Example:

```bash
sum=$((a+b))
```

---

## Relational Operators

Used for comparison operations.

| Operator | Description              |
| -------- | ------------------------ |
| -gt      | Greater Than             |
| -lt      | Less Than                |
| -ge      | Greater Than or Equal To |
| -le      | Less Than or Equal To    |
| -eq      | Equal To                 |
| -ne      | Not Equal To             |

Example:

```bash
if [ $a -gt $b ]
```

---

## Logical Operators

Used to combine multiple conditions.

| Operator | Description |
| -------- | ----------- |
| -a       | Logical AND |
| -o       | Logical OR  |
| !        | Logical NOT |

Example:

```bash
if [ $a -gt $b -a $a -gt $c ]
```

---

# Arithmetic Operations

Arithmetic calculations can be performed using:

```bash
$(( ))
```

Example:

```bash
sum=$((a+b))
```

Alternative method:

```bash
let sum=a+b
```

---

# Conditional Statements

Conditional statements allow decision-making within scripts.

---

## if Statement

Syntax:

```bash
if [ condition ]
then
    statements
fi
```

Example:

```bash
if [ $a -gt $b ]
then
    echo "$a is greater"
fi
```

---

## if-else Statement

Syntax:

```bash
if [ condition ]
then
    statements
else
    statements
fi
```

---

## if-elif-else Statement

Syntax:

```bash
if [ condition1 ]
then
    statements
elif [ condition2 ]
then
    statements
else
    statements
fi
```

---

# Program: Addition of Two Numbers

```bash
#!/bin/bash

read -p "Enter first number: " a
read -p "Enter second number: " b

sum=$((a+b))

echo "The sum of $a and $b is $sum"
```

Sample Output:

```text
Enter first number: 34
Enter second number: 43

The sum of 34 and 43 is 77
```

---

# Program: Sum of Digits of a Four-Digit Number

Input:

```text
1234
```

Logic:

```text
1 + 2 + 3 + 4 = 10
```

Script:

```bash
read -p "Enter any 4 digit Integer Number: " n

a=$(echo $n | cut -c 1)
b=$(echo $n | cut -c 2)
c=$(echo $n | cut -c 3)
d=$(echo $n | cut -c 4)

echo "The sum of all positional digits are : $((a+b+c+d))"
```

---

# Pipe Operator

The pipe operator transfers the output of one command as input to another command.

Syntax:

```bash
command1 | command2
```

Example:

```bash
echo $n | cut -c 1
```

Here:

* `echo` produces output
* `cut` receives the output as input

---

# cut Command

Used to extract specific characters from text.

Examples:

```bash
cut -c 1
cut -c 2
cut -c 3
cut -c 4
```

Used in the four-digit number program to extract individual digits.

---

# Program: Greatest of Three Numbers

```bash
#!/bin/bash

read -p "Enter 3 Numbers: " a b c

if [ $a -gt $b -a $a -gt $c ]
then
    echo "The Greatest Number is : $a"

elif [ $b -gt $c ]
then
    echo "The Greatest Number is : $b"

else
    echo "The Greatest Number is : $c"
fi
```

---

# Loops in Shell Scripting

Loops are used to execute a block of code repeatedly.

---

# While Loop

Executes repeatedly while the condition remains true.

Syntax:

```bash
while [ condition ]
do
    statements
done
```

Example:

```bash
i=1

while [ $i -le 10 ]
do
    echo $i
    let i++
done
```

Output:

```text
1
2
3
4
5
6
7
8
9
10
```

---

# Program: Sum of First N Numbers

```bash
read -p "Enter the value: " n

i=1
sum=0

while [ $i -le $n ]
do
    let sum=sum+i
    let i++
done

echo "The sum of first $n numbers is : $sum"
```

---

# Until Loop

Executes until a condition becomes true.

Syntax:

```bash
until [ condition ]
do
    statements
done
```

Difference:

* While Loop → Runs while condition is true.
* Until Loop → Runs until condition becomes true.

---

# For Loop

Used when the number of iterations is known.

Syntax:

```bash
for ((initialization; condition; increment))
do
    statements
done
```

---

## Example: Print 1 to N

```bash
for ((i=1;i<=10;i++))
do
    echo $i
done
```

---

## Example: Reverse Counting

```bash
for ((i=n;i>=1;i--))
do
    echo $i
done
```

---

# Program: Multiplication Table

```bash
#!/bin/bash

read -p "Enter the Nth Table: " n

for ((i=1;i<=10;i++))
do
    echo "$n * $i = $((n*i))"
done
```

Sample Output:

```text
2 * 1 = 2
2 * 2 = 4
2 * 3 = 6
...
2 * 10 = 20
```

---

# File Handling with For Loop

The script iterates through all items in the current directory.

```bash
for fname in *
do
    if [ -f $fname ]
    then
        echo "The file name is $fname"
    fi
done
```

---

## File Test Operator

```bash
-f
```

Checks whether the given object is a regular file.

Example:

```bash
if [ -f filename ]
```

---

# Automation Concepts Introduced

The instructor briefly discussed creating automation tools using shell scripts.

Shell scripts can be used for:

* File management
* Backup automation
* Log monitoring
* System administration
* Security auditing
* Network scanning
* Cybersecurity automation tasks

---

# Key Learning Outcomes

By the end of this session, participants were able to:

* Create and execute Bash shell scripts
* Use variables and user input
* Perform arithmetic operations
* Apply relational and logical operators
* Implement conditional statements
* Develop programs using if, elif, and nested if
* Use pipe operations and command substitution
* Extract data using the cut command
* Implement while, until, and for loops
* Create multiplication table and number-processing scripts
* Iterate through files in a directory
* Understand the foundations of shell-based automation

---

# Conclusion

Session 3 completed the core Shell Scripting fundamentals required for Linux administration and cybersecurity automation. Participants gained hands-on experience with Bash scripting, control structures, loops, file handling, and simple automation techniques, forming the foundation for future Python programming and cybersecurity tool development.
