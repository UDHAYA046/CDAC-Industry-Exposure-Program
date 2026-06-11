# Assignment 2 – Linux Commands, Processes, Networking, Shell Scripting, Permissions & ACL

**Course:** CDAC Industry Exposure Program – Cybersecurity  
**Module:** Linux Fundamentals  
**Assignment:** Assignment 2  
**Student:** Udhaya Sankari  
**Date:** June 2026

---

# Objective

The objective of this assignment was to gain hands-on experience with:

- Linux file and directory management
- Process management
- Networking commands
- Shell scripting
- User and group administration
- Linux permissions
- Access Control Lists (ACLs)

The assignment was performed on Kali Linux using terminal commands and shell scripts.

---

# Topics Covered

## File and Directory Management

- Creating directories
- Creating files
- Hidden files
- Copying files
- Moving files
- Searching files
- File content viewing
- File statistics

## Process Management

- Viewing running processes
- Identifying Process IDs (PIDs)
- Running background jobs
- Terminating processes

## System Monitoring

- Memory utilization
- Disk usage monitoring

## Networking

- Viewing IP addresses
- Network configuration inspection

## Shell Scripting

- Variables
- User input
- Arithmetic operations
- Conditional statements
- Loops
- Directory operations

## Linux Security

- User management
- Group management
- File permissions
- ACL (Access Control Lists)
- Default ACL inheritance

---

# Questions Performed

---

# Q1. Create a Directory

Created a directory named:

```bash
mkdir ~/linuxlab
```

Verified using:

```bash
ls ~
```

Purpose:

- Demonstrates directory creation in Linux.
- Forms the workspace for the remaining assignment tasks.

---

# Q2. Create Files

Created three empty files:

```bash
touch file1.txt file2.txt file3.txt
```

Verification:

```bash
ls
```

Files created:

- file1.txt
- file2.txt
- file3.txt

---

# Q3. Display Current Directory and Hidden Files

Commands used:

```bash
pwd
ls -la
```

Purpose:

- `pwd` displays the current working directory.
- `ls -la` displays all files including hidden files.

---

# Q4. Create a Hidden File

Created:

```bash
touch .secret
```

Verification:

```bash
ls -la
```

Purpose:

- Demonstrates hidden files in Linux.
- Files beginning with a dot (`.`) remain hidden during normal listing.

---

# Q5. Copy a File

Copied:

```bash
cp file1.txt backup_file1.txt
```

Verification:

```bash
ls
```

Purpose:

- Demonstrates file duplication using the `cp` command.

---

# Q6. Move a File

Created archive directory:

```bash
mkdir archive
```

Moved file:

```bash
mv file2.txt archive/
```

Verification:

```bash
ls archive
```

Purpose:

- Demonstrates file relocation.

---

# Q7. Find All Text Files

Command:

```bash
find ~ -name "*.txt"
```

Purpose:

- Searches recursively inside the home directory.
- Displays all files ending with `.txt`.

---

# Q8. Display First and Last 5 Lines

Commands:

```bash
head -5 filename.txt
tail -5 filename.txt
```

Purpose:

- `head` displays the beginning of a file.
- `tail` displays the end of a file.

Commonly used for log analysis and troubleshooting.

---

# Q9. Count Lines, Words and Characters

Command:

```bash
wc filename.txt
```

Output includes:

1. Number of lines
2. Number of words
3. Number of characters

Purpose:

- Provides file statistics.
- Frequently used during scripting and reporting.

---

# Q10. Search for a Word

Command:

```bash
grep "Linux" filename.txt
```

Purpose:

- Searches for matching text.
- Displays lines containing the keyword.

---

# Q11. Display Running Processes

Command:

```bash
ps -ef
```

Finding bash process:

```bash
ps -ef | grep bash
```

Purpose:

- Displays all active processes.
- Identifies the Process ID (PID) of the bash shell.

---

# Q12. Start a Background Process

Command:

```bash
sleep 300 &
```

Purpose:

- Starts a process in the background.
- Linux returns a job ID and PID.

Verification:

```bash
jobs
```

---

# Q13. Terminate Background Process

Command:

```bash
kill <PID>
```

Verification:

```bash
jobs
```

Purpose:

- Demonstrates process termination.

---

# Q14. Display Memory and Disk Usage

Memory:

```bash
free -h
```

Disk:

```bash
df -h
```

Purpose:

- Monitors RAM utilization.
- Displays storage utilization.

Important for Linux administration and cloud monitoring.

---

# Q15. Check Network Configuration

Commands:

```bash
ip a
```

or

```bash
ifconfig
```

Purpose:

- Displays IP addresses.
- Displays network interfaces.
- Displays subnet and network configuration information.

---

# Q16. Shell Script – System Information

Script displays:

- Current Date
- Current User
- Hostname

Example:

```bash
#!/bin/bash

echo "Date: $(date)"
echo "User: $(whoami)"
echo "Hostname: $(hostname)"
```

Execution:

```bash
bash q16.sh
```

Purpose:

- Introduces command substitution and shell scripting.

---

# Q17. Shell Script – Add Two Numbers

Script:

```bash
#!/bin/bash

read -p "Enter first number: " a
read -p "Enter second number: " b

sum=$((a+b))

echo "Sum = $sum"
```

Purpose:

- Demonstrates user input.
- Demonstrates arithmetic operations.

---

# Q18. Shell Script – Even or Odd

Script:

```bash
#!/bin/bash

read -p "Enter number: " num

if [ $((num % 2)) -eq 0 ]
then
    echo "Even"
else
    echo "Odd"
fi
```

Purpose:

- Demonstrates conditional statements.

---

# Q19. Shell Script – Numbers 1 to 10

Script:

```bash
#!/bin/bash

for i in {1..10}
do
    echo $i
done
```

Purpose:

- Demonstrates looping constructs.

---

# Q20. Count Files in Directory

Script:

```bash
#!/bin/bash

read -p "Enter directory path: " dir

count=$(find "$dir" -type f | wc -l)

echo "Number of files: $count"
```

Valid Input Example:

```bash
/home/udhaya/linuxlab
```

Purpose:

- Demonstrates directory traversal.
- Demonstrates command substitution.

---

# Q21. Linux Permissions

Created:

```bash
touch project.txt
```

Assigned permissions:

Owner:

- Read
- Write
- Execute

Group:

- Read
- Execute

Others:

- Read

Command:

```bash
chmod 754 project.txt
```

Verification:

```bash
ls -l project.txt
```

Output:

```text
-rwxr-xr--
```

---

# Q22. Modify Permissions

Required:

```text
rw-r-----
```

Numeric Method:

```bash
chmod 640 project.txt
```

Symbolic Method:

```bash
chmod u=rw,g=r,o= project.txt
```

Verification:

```bash
ls -l
```

Output:

```text
-rw-r-----
```

---

# Q23. Create Group and Assign Ownership

Create group:

```bash
sudo groupadd developers
```

Assign ownership:

```bash
sudo chgrp developers project.txt
```

Verification:

```bash
ls -l project.txt
```

Purpose:

- Demonstrates group administration.

---

# Q24. ACL for User student1

Create user:

```bash
sudo useradd -m student1
```

Set password:

```bash
sudo passwd student1
```

Grant ACL:

```bash
sudo setfacl -m u:student1:rw project.txt
```

Verify:

```bash
getfacl project.txt
```

Test:

```bash
su - student1
cat /home/udhaya/linuxlab/project.txt
```

Additional requirement:

Directory traversal permissions were enabled using:

```bash
chmod o+x /home/udhaya
chmod o+x /home/udhaya/linuxlab
```

Result:

- student1 successfully accessed the file.
- ACL functionality verified.

---

# Q25. Default ACL Inheritance

Created directory:

```bash
mkdir shared_data
```

Configured default ACL:

```bash
setfacl -d -m u:student1:rw shared_data
```

Verification:

```bash
getfacl shared_data
```

Created test file:

```bash
touch shared_data/testfile.txt
```

Checked inherited ACL:

```bash
getfacl shared_data/testfile.txt
```

Observed:

```text
user:student1:rw-
```

Testing:

```bash
su - student1
echo "Hello from student1" >> /home/udhaya/linuxlab/shared_data/testfile.txt
```

Verification:

```bash
cat /home/udhaya/linuxlab/shared_data/testfile.txt
```

Output:

```text
Hello from student1
```

Result:

- ACL inheritance verified successfully.
- student1 automatically received read/write permissions.

---

# Key Concepts Learned

## Linux Commands

- mkdir
- touch
- cp
- mv
- ls
- pwd
- find
- head
- tail
- wc
- grep

## Process Management

- ps
- jobs
- kill
- sleep

## System Monitoring

- free
- df

## Networking

- ip
- ifconfig

## Shell Scripting

- Variables
- User Input
- Loops
- Conditions
- Arithmetic Operations

## Security Concepts

- Linux Permissions
- Users and Groups
- ACLs
- Default ACL Inheritance

---

# Conclusion

This assignment provided practical exposure to Linux system administration, process management, networking, shell scripting, permissions, and access control mechanisms. The exercises reinforced essential cybersecurity and Linux administration concepts, particularly ACL-based access management, process monitoring, and automation through shell scripting. These skills form the foundation for advanced topics in cybersecurity, cloud computing, system administration, and DevOps.
