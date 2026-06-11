# Session 3 – Linux Utilities, Networking, Hashing & Introduction to Shell Scripting

**Date:** 09 June 2026
**Duration:** 2:00 PM – 5:00 PM
**Course:** CDAC Industry Exposure Program

---

# Overview

The third session focused on understanding how Linux commands, file systems, process management, networking utilities, password security mechanisms, and shell scripting are used in real-world cloud computing and cybersecurity environments.

The instructor emphasized that modern cloud engineers, DevOps engineers, system administrators, SOC analysts, and penetration testers cannot rely on manual operations for repetitive tasks. Shell scripting enables automation of routine activities, improving efficiency, consistency, and scalability.

The session included practical demonstrations of Linux utilities, process monitoring, networking commands, password hashing concepts, wildcard usage, file archiving, and introductory shell scripting.

---

# Why Shell Scripting?

The primary purpose of shell scripting is automation.

Instead of manually:

* Logging into servers
* Opening terminals
* Entering credentials
* Executing commands repeatedly
* Collecting outputs
* Monitoring processes
* Generating reports

all these tasks can be automated through shell scripts.

---

## Cloud Computing Perspective

In cloud environments such as AWS, Azure, and Google Cloud Platform, administrators frequently perform tasks such as:

* Monitoring server health
* Restarting services
* Collecting logs
* Managing storage
* Verifying connectivity
* Deploying applications

Performing these activities manually across multiple systems becomes inefficient and time-consuming. Shell scripting provides an effective automation mechanism.

---

## Cybersecurity Perspective

Security professionals often perform:

* Vulnerability assessments
* Log analysis
* Network reconnaissance
* Threat hunting
* Process monitoring
* Security auditing

Shell scripts can automate the complete workflow by chaining tools together and processing outputs automatically.

Example:

```text
Scanner Output
      ↓
Log File
      ↓
Parser
      ↓
Security Report
```

---

# Linux Permissions Review

The session revisited Linux file permissions and ownership concepts.

Permission categories:

```text
User
Group
Others
```

Permission values:

| Permission | Value |
| ---------- | ----- |
| Read       | 4     |
| Write      | 2     |
| Execute    | 1     |

Example:

```bash
chmod 700 file.txt
```

Meaning:

```text
User   : rwx
Group  : ---
Others : ---
```

---

## Real-World Example

The instructor used the IRCTC website as an analogy.

Users who visit the website are generally allowed:

```text
Read
Execute
```

permissions.

However:

```text
Write
```

permissions are restricted to authorized users only.

This prevents unauthorized modification of critical resources.

---

# Linux File System Hierarchy

Several important Linux directories were explored.

---

## /bin

Contains executable binary files.

Example:

```bash
cd /bin
ls
```

Common commands stored here:

```text
ls
cat
mv
cp
rm
```

---

## /etc

Stores system-wide configuration files.

Example:

```bash
cd /etc
ls
```

Observed examples:

* Apache configurations
* Java configurations
* Network configurations
* Package manager configurations

---

## /var

Stores variable application data.

Example:

```bash
cd /var
```

Observed directories:

```text
backups
cache
lib
lock
log
mail
www
```

---

## /var/www/html

Default web content directory used by web servers.

Example:

```bash
cd /var/www/html
ls
```

Observed:

```text
index.html
index.nginx-debian.html
```

This directory is commonly used by Apache and Nginx servers.

---

# Password Storage and Hashing

One of the most important cybersecurity topics discussed during the session.

---

## Historical Method

Passwords were previously stored as plain text.

Example:

```text
admin:password123
user:qwerty
```

This approach is insecure because anyone accessing the file can view user credentials.

---

## Hashing

Modern systems store password hashes instead of actual passwords.

Example:

```text
password123
```

can become:

```text
482c811da5d5b4bc6d497ffa98491e38
```

using a hashing algorithm.

---

## Important Property

Hashing is a one-way function.

```text
Password → Hash
```

Easy.

```text
Hash → Password
```

Computationally difficult.

---

## Salting

To improve security, Linux systems add a random value called a salt before hashing.

Example:

```text
Password + Salt
      ↓
Hash
```

Benefits:

* Prevents identical hashes
* Protects against rainbow table attacks
* Increases password security

---

## Relevant Files

### /etc/passwd

Stores:

* User information
* User IDs
* Home directories
* Login shell details

### /etc/shadow

Stores:

* Password hashes
* Password policies
* Authentication-related information

Linux stores password hashes instead of actual passwords.

---

# Linux Utility Commands

---

## history

Displays previously executed commands.

```bash
history
```

Useful for:

* Auditing
* Troubleshooting
* Reusing commands

---

## man

Displays command manuals.

Example:

```bash
man ls
```

Provides:

* Usage
* Syntax
* Options
* Examples

---

## Dangerous Command

The instructor highlighted:

```bash
rm -rf *
```

Meaning:

```text
Remove
Recursively
Forcefully
Everything
```

This command can permanently delete files and directories.

---

# File Viewing Commands

---

## cat

Display file contents.

```bash
cat file.txt
```

---

## head

Display first 10 lines.

```bash
head file.txt
```

---

## tail

Display last 10 lines.

```bash
tail file.txt
```

Commonly used for:

* Log monitoring
* Recent activity inspection

---

## less

View large files page-by-page.

```bash
less file.txt
```

---

## more

Older file viewing utility.

```bash
more file.txt
```

---

# File Comparison Commands

---

## cmp

Compare two files.

```bash
cmp file1 file2
```

Displays the first difference encountered.

---

## diff

Displays all differences between files.

```bash
diff file1 file2
```

Frequently used for:

* Configuration comparisons
* Source code reviews
* Change tracking

---

# Word Count Utility

Command:

```bash
wc file.txt
```

Displays:

```text
Lines
Words
Characters
```

Useful for file statistics and reporting.

---

# Sorting

Sort file contents:

```bash
sort file.txt
```

Store output in another file:

```bash
sort file.txt > sorted.txt
```

---

# Redirection

Output redirection:

```bash
>
```

Example:

```bash
ls > output.txt
```

Input redirection:

```bash
<
```

---

# Piping

Symbol:

```bash
|
```

Purpose:

Output of one command becomes input to another.

Example:

```bash
ls | wc -l
```

Meaning:

```text
List Files
      ↓
Count Lines
```

---

# Process Management

---

## ps

View running processes.

```bash
ps
```

---

## ps -ef

Detailed process information.

```bash
ps -ef
```

---

## top

Real-time process monitor.

```bash
top
```

Displays:

* CPU utilization
* Memory utilization
* Running processes

---

## htop

Enhanced process monitoring utility.

```bash
htop
```

---

## kill

Terminate a process.

```bash
kill PID
```

---

## pkill

Terminate using process name.

```bash
pkill process_name
```

---

# Storage Utilities

---

## du

Disk usage.

```bash
du
```

---

## df -h

Filesystem usage.

```bash
df -h
```

---

## lsblk

Display block devices.

```bash
lsblk
```

Shows:

* Hard drives
* Partitions
* Storage devices

---

# Networking Commands

---

## ifconfig

Display network configuration.

```bash
ifconfig
```

---

## ip a

Modern alternative to ifconfig.

```bash
ip a
```

---

## ping

Test network connectivity.

```bash
ping google.com
```

---

## nslookup

Perform DNS lookup.

```bash
nslookup google.com
```

---

## dig

Detailed DNS information gathering.

```bash
dig google.com
```

---

## netstat

Display network statistics.

```bash
netstat
```

---

## traceroute

Track packet path to destination.

```bash
traceroute google.com
```

---

## curl

Retrieve webpage content.

```bash
curl https://example.com
```

---

# Wildcards

---

## *

Matches any number of characters.

Example:

```bash
ls *
```

---

## ?

Matches exactly one character.

Example:

```bash
ls ???
```

Used extensively for pattern matching.

---

# File Archiving

Create TAR archive:

```bash
tar -cvf sangam.tar *
```

Observed result:

```text
sangam.tar
```

created successfully.

---

# Shell Types

Various shell types were discussed.

| Shell             | Developer          |
| ----------------- | ------------------ |
| Bourne Shell (sh) | Stephen Bourne     |
| Bash              | Bourne Again Shell |
| Korn Shell (ksh)  | David Korn         |
| C Shell (csh)     | Bill Joy           |
| Tcsh              | Enhanced C Shell   |
| Z Shell (zsh)     | Extended Shell     |

---

## Current Shell

View current shell:

```bash
echo $SHELL
```

Observed:

```text
Z Shell (zsh)
```

---

## Available Shells

```bash
cat /etc/shells
```

---

# Introduction to Shell Scripting

---

## First Automation Script

Created:

```bash
automate.sh
```

Contents:

```bash
#!/bin/bash

echo "This is my first automation programme"

ls
date
ls -ll
```

Execution:

```bash
bash automate.sh
```

The script executed multiple commands automatically in sequence.

---

# Variables in Shell Scripts

Example:

```bash
a=10
b=20

course="CSEH9th batch"
Action="Study"
```

Accessing variables:

```bash
$a
$b
$course
$Action
```

---

# Printing Variables

Example:

```bash
echo "Values of a and b are $a and $b"
```

Output:

```text
Values of a and b are 10 and 20
```

---

# User Input in Shell Scripts

---

## Method 1

```bash
read A
```

---

## Method 2 (Preferred)

```bash
read -p "Enter Value: " A
```

Example:

```bash
read -p "Enter the Value of A: " A
read -p "Enter the Value of B: " B
```

Display:

```bash
echo "A value is $A"
echo "B value is $B"
```

---

# Script Execution Methods

Using Bash:

```bash
bash script.sh
```

Using Dash:

```bash
dash script.sh
```

Using Z Shell:

```bash
zsh script.sh
```

Direct execution:

```bash
chmod +x script.sh
./script.sh
```

---

# Key Learning Outcomes

By the end of Session 3, the following concepts were understood:

* Linux file hierarchy
* Password hashing and salting
* Linux permissions and ownership
* File viewing utilities
* Process monitoring and management
* Network information gathering commands
* Wildcards and pattern matching
* File archiving
* Different shell environments
* Introduction to shell scripting
* Variables and user input
* Script execution methods
* Automation fundamentals

The session established the foundation required for advanced shell scripting concepts such as arithmetic operations, conditional statements, loops, functions, and automation workflows that are heavily used in Cloud Computing, DevOps, System Administration, and Cybersecurity.

