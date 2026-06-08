# Session 1 – Linux Fundamentals & UNIX Architecture

**Date:** 02 June 2026
**Duration:** 2:00 PM – 5:00 PM
**Course:** CDAC Industry Exposure Program

---

# Overview

The first session introduced the fundamentals of Linux, UNIX architecture, open-source software concepts, operating system responsibilities, virtualization, and Kali Linux installation.

The instructor emphasized understanding the internal working of the operating system rather than merely memorizing commands. Special focus was placed on understanding the interaction between users, the shell, the kernel, and hardware.

---

# Topics Covered

## Operating System Fundamentals

An Operating System (OS) acts as an interface between the user and computer hardware.

### Responsibilities of an Operating System

* Process Management
* Memory Management
* File Management
* Device Management
* CPU Scheduling
* Security Management

---

## UNIX Introduction

UNIX is:

* Portable
* Multi-user
* Multi-tasking
* Multi-processing
* Written in C language

### UNIX Components

#### Kernel

The core of the operating system responsible for:

* Process Management
* Memory Management
* Device Management
* File Systems
* Security

#### Shell

Acts as an interface between the user and the kernel.

Responsibilities:

* Accept commands
* Interpret commands
* Communicate with the kernel

#### Applications

Examples:

* Browsers
* Editors
* Utility Programs

---

## UNIX Architecture

Applications
↑
Shell
↑
Kernel
↑
Hardware

The kernel serves as the bridge between software and hardware.

---

## Linux Fundamentals

Linux is a UNIX-like operating system that provides:

* Multi-user support
* Multi-tasking
* Multi-processing
* Open-source development
* Networking support
* Complete development environment

---

## Open Source Software

### Characteristics

* Freedom to use
* Freedom to modify
* Freedom to distribute
* Access to source code

### License Types

#### GPL (GNU General Public License)

* Source code must remain available.
* Modifications must be distributed under the same license.

#### BSD License

* Modifications can remain private.
* No obligation to share source code changes.

---

## Linux History

| Year | Event            |
| ---- | ---------------- |
| 1969 | UNIX             |
| 1985 | MINIX            |
| 1991 | Linux            |
| 1993 | Debian, Red Hat  |
| 1994 | Linux Kernel 1.0 |
| 2001 | Ubuntu           |
| 2007 | Android          |

---

## Linux Distributions

Covered distributions:

* Ubuntu
* Debian
* Fedora
* Red Hat
* OpenSUSE
* Kali Linux
* Linux Mint
* Android
* Chromium OS

---

## Linux vs UNIX

| Linux                         | UNIX                 |
| ----------------------------- | -------------------- |
| Open Source                   | Mostly Commercial    |
| Community Driven              | Vendor Controlled    |
| Supports Broad Hardware Range | Specialized Hardware |
| Freely Distributed            | Commercial Licensing |

---

# Cybersecurity Concepts Introduced

## Vulnerability Assessment (VA)

Process of identifying vulnerabilities and prioritizing remediation.

## Penetration Testing (PT)

Process of simulating attacks to evaluate security.

## CERT-In

Indian Computer Emergency Response Team responsible for cyber incident response and security advisories.

---

# Virtualization

## Oracle VirtualBox Installation

Installed Oracle VirtualBox to create isolated Linux environments.

### Virtualization Stack

Windows
↓
Oracle VirtualBox
↓
Kali Linux

---

# Kali Linux Installation

## Virtual Machine Configuration

| Parameter       | Value           |
| --------------- | --------------- |
| VM Name         | Kali Linux      |
| RAM             | 4096 MB         |
| CPU             | 2               |
| Disk Size       | 30 GB           |
| Hypervisor Type | Type 2 (Hosted) |

### Installation Steps

* Downloaded Kali Linux ISO
* Created Virtual Machine
* Configured storage
* Configured users
* Configured partitions
* Installed software packages
* Installed GRUB bootloader

---

# Practical Challenge

## Error Encountered

Error:

DrvVD_DISKFULL

Cause:

Host machine storage became full during installation.

Resolution:

Freed storage space and resumed installation.

---

# Quiz Performance

🏆 Rank: 1st Place

Nickname: GreenPanda

Score: 7934

---

# Key Takeaways

* Understanding Linux requires understanding kernel-level concepts.
* Linux is dominant in cloud, cybersecurity, DevOps, and server environments.
* Open-source licensing influences software distribution.
* Virtualization enables safe experimentation without modifying the host OS.
* Kali Linux serves as a primary platform for cybersecurity learning.
