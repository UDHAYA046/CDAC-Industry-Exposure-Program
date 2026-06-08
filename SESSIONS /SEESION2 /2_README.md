# Session 2 – Linux Commands, Users & Permissions

**Date:** 04 June 2026
**Duration:** 2:00 PM – 5:00 PM
**Course:** CDAC Industry Exposure Program

---

# Overview

The second session focused on practical Linux usage through command-line interaction. Topics included Linux users, privilege management, file operations, file viewing utilities, permission management, and virtualization concepts.

---

# Linux User Management

## User Types

### Normal User

* Limited privileges
* Used for everyday tasks
* Cannot modify critical system settings

### Administrator (Root User)

* Full system access
* Responsible for system administration
* Can install software and manage users

---

## sudo Command

Used to execute commands with administrative privileges.

Example:

```bash
sudo apt update
```

sudo stands for:

Super User Do

---

# Basic Linux Commands

## date

Displays current date and time.

```bash
date
```

---

## cal

Displays calendar.

```bash
cal
```

---

## clear

Clears terminal screen.

```bash
clear
```

Shortcut:

```text
Ctrl + L
```

---

## whoami

Displays currently logged-in user.

```bash
whoami
```

---

## ls

Lists files and directories.

```bash
ls
```

---

## pwd

Print Working Directory.

Displays current directory location.

```bash
pwd
```

---

# File Operations

## cat

Displays file contents.

```bash
cat filename
```

---

## Creating Files

```bash
cat > filename
```

Save using:

```text
Ctrl + D
```

---

## Appending Data

```bash
cat >> filename
```

Adds data to existing files.

---

# File Viewing Commands

## less

View large files page-by-page.

```bash
less filename
```

---

## more

Display file content page-by-page.

```bash
more filename
```

---

## head

Display first 10 lines.

```bash
head filename
```

---

## tail

Display last 10 lines.

```bash
tail filename
```

---

## page

Display file page-by-page.

```bash
page filename
```

---

# Linux File Permissions

Linux permissions determine who can:

* Read files
* Modify files
* Execute files

---

## Permission Categories

### User (u)

Owner of the file.

### Group (g)

Users belonging to the file's assigned group.

### Others (o)

Everyone else on the system.

---

## Permission Values

| Permission | Symbol | Value |
| ---------- | ------ | ----- |
| Read       | r      | 4     |
| Write      | w      | 2     |
| Execute    | x      | 1     |
| None       | -      | 0     |

---

# chmod Command

## Syntax

```bash
chmod [who][operator][permission] filename
```

Example:

```bash
chmod u+x script.sh
```

---

## Operators

| Operator | Meaning              |
| -------- | -------------------- |
| +        | Add permission       |
| -        | Remove permission    |
| =        | Set exact permission |

---

# Numeric Permission Model

## chmod 777

```bash
chmod 777 file.txt
```

Owner → rwx

Group → rwx

Others → rwx

Everyone has full access.

---

## chmod 755

```bash
chmod 755 script.sh
```

Owner → rwx

Group → r-x

Others → r-x

Most common permission for executable scripts.

---

## chmod 644

```bash
chmod 644 file.txt
```

Owner → rw-

Group → r--

Others → r--

Common permission for documents and configuration files.

---

## chmod 700

```bash
chmod 700 secret.txt
```

Owner → rwx

Group → ---

Others → ---

Private access for owner only.

---

# Virtualization Concepts

## Hypervisor

Software that manages virtual machines.

---

## Type 1 Hypervisor (Bare Metal)

Architecture:

Hardware
↓
Hypervisor
↓
Virtual Machines

Examples:

* VMware ESXi
* Hyper-V
* Xen
* KVM

---

## Type 2 Hypervisor (Hosted)

Architecture:

Hardware
↓
Host OS
↓
Hypervisor
↓
Virtual Machines

Examples:

* Oracle VirtualBox
* VMware Workstation

---

## Current Lab Setup

Hardware
↓
Windows
↓
Oracle VirtualBox
↓
Kali Linux

This setup uses a Type 2 Hypervisor.

---

# Commands Practiced

```bash
date
cal
clear
whoami
ls
pwd
cat
less
more
head
tail
page
sudo
chmod
```

---

# Key Takeaways

* Linux follows the principle of least privilege.
* sudo allows temporary administrative access.
* Linux provides powerful file viewing utilities.
* File permissions form the foundation of Linux security.
* chmod controls access using symbolic and numeric permission models.
* Understanding permissions is essential for Linux administration, cloud computing, and cybersecurity.
