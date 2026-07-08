
# Session 10 – Password Cracking, Exploitation, Privilege Escalation and Post-Exploitation
## Part 1 – Overview, Authentication, Password Cracking and Password Storage

---

# Overview

This session focuses on the stages of a cyber attack that occur after reconnaissance and vulnerability identification. Once an attacker discovers a vulnerable target, the next objectives are to gain access, increase privileges, execute malicious code, maintain persistence, and hide evidence of compromise.

Unlike previous sessions, which concentrated on reconnaissance, scanning, enumeration, and vulnerability identification, this session shifts focus toward exploitation and post-exploitation techniques.

The major topics covered include:

- Microsoft authentication mechanisms
- Password storage
- Password cracking
- Password attack techniques
- Password recovery tools
- Password cracking tools
- Password salting
- Exploitation fundamentals
- Privilege escalation
- Post exploitation
- Remote code execution
- Practical demonstrations using Kali Linux and Metasploitable

The instructor emphasized that all demonstrations should only be performed in authorized laboratory environments such as Kali Linux, Metasploitable, DVWA, or systems where explicit permission has been granted.

---

# Ethical Boundary

Every technique discussed during this session is intended for:

- Authorized penetration testing
- Personal laboratory environments
- Vulnerable virtual machines
- Educational purposes

These techniques must **never** be used against systems that you do not own or do not have written authorization to test.

A simple rule followed by every ethical hacker is:

```text
No Permission
        =
No Testing
```

Ethics separates a penetration tester from an attacker.

---

# Attack Lifecycle

This session covers the middle portion of a penetration testing engagement.

Complete attack lifecycle:

```text
Reconnaissance
        ↓
Scanning
        ↓
Enumeration
        ↓
Vulnerability Assessment
        ↓
Exploitation
        ↓
Privilege Escalation
        ↓
Persistence
        ↓
Post Exploitation
        ↓
Covering Tracks
        ↓
Reporting
```

The primary focus of this session is:

```text
Exploitation

↓

Privilege Escalation

↓

Post Exploitation
```

---

# Authentication

## What is Authentication?

Authentication is the process of verifying the identity of a user, device, or application before granting access to resources.

Authentication answers the question:

```text
Who are you?
```

Examples include:

- Username and password
- Fingerprint
- Face recognition
- OTP
- Smart cards
- Security keys

Only after successful authentication does the system determine what actions the user is allowed to perform.

---

# Authentication vs Authorization

Students often confuse these two concepts.

## Authentication

Authentication verifies identity.

Example:

```text
Username

+

Password

↓

Identity Verified
```

---

## Authorization

Authorization determines what the authenticated user is allowed to access.

Example:

```text
Authenticated User

↓

Can View Dashboard

↓

Cannot Delete Users
```

Authentication comes first.

Authorization comes second.

---

# Microsoft Authentication

Modern Windows systems use multiple authentication mechanisms.

The session introduces two important authentication protocols:

- NTLM
- Kerberos

Before understanding these protocols, it is important to understand how Windows stores user credentials.

---

# Security Accounts Manager (SAM)

## What is SAM?

SAM stands for:

```text
Security Accounts Manager
```

It is a Windows database that stores information about local user accounts.

SAM contains:

- Usernames
- Password hashes
- Account identifiers
- Security information

One of the most important security concepts is:

Windows does **not** store user passwords directly.

Instead, Windows stores password hashes.

---

# Password vs Password Hash

## Password

The password is the secret chosen by the user.

Example:

```text
Password123
```

---

## Hash

A hash is the output of a mathematical function applied to the password.

Example:

```text
Password123

↓

Hash Function

↓

482c811da5d5b4bc6d497ffa98491e38
```

The original password cannot easily be recovered from the hash.

Authentication works by hashing the entered password and comparing it with the stored hash.

---

# Why Hash Passwords?

Suppose passwords were stored directly.

Example:

```text
admin : password123

john : hello123
```

If an attacker steals the database, every password becomes immediately available.

Instead, systems store:

```text
admin : 482c811da5d5...

john : 94b5f87...
```

Although hashes can sometimes be cracked, they provide significantly better protection than plaintext passwords.

---

# NTLM Authentication

## What is NTLM?

NTLM stands for:

```text
NT LAN Manager
```

It is a Microsoft authentication protocol used by Windows systems.

Although Kerberos is now preferred in Active Directory environments, NTLM remains important because many legacy systems still support it.

---

# Why NTLM is Targeted

Attackers frequently target NTLM because:

- NTLM hashes can sometimes be captured.
- Weak passwords can be cracked offline.
- Legacy environments still depend on NTLM.
- Misconfigured systems may allow relay attacks.

---

# LM Hashes vs NTLM Hashes

Earlier Windows systems used LM hashes.

LM hashing had several weaknesses:

- Passwords converted to uppercase.
- Password divided into smaller blocks.
- Weak cryptographic design.
- Easier brute-force attacks.

NTLM improved upon LM but still has limitations.

Modern enterprise environments generally prefer Kerberos.

---

# Kerberos Authentication

## What is Kerberos?

Kerberos is a ticket-based authentication protocol designed to provide stronger security than NTLM.

Instead of repeatedly sending authentication information, Kerberos issues encrypted tickets.

Authentication flow:

```text
User Logs In

↓

Domain Controller Verifies Identity

↓

Ticket Granted

↓

Ticket Used to Access Services
```

---

# Advantages of Kerberos

Kerberos provides:

- Mutual authentication
- Ticket-based authentication
- Strong encryption
- Better protection against replay attacks
- Efficient authentication within Active Directory

However, Kerberos can still be attacked if administrators use weak passwords or poor configurations.

Examples include:

- Kerberoasting
- AS-REP Roasting
- Weak Service Account Passwords

---

# Password Cracking

## Definition

Password cracking is the process of recovering passwords by testing guesses against:

- Login systems
- Password hashes
- Encrypted password databases
- Protected files

Password cracking is commonly performed during:

- Password auditing
- Security assessments
- Penetration testing
- Digital forensics

---

# Why Password Cracking Works

Most successful password attacks occur because users choose predictable passwords.

Examples include:

```text
password123

admin123

welcome

company@123

john1998

india123
```

Attackers take advantage of predictable human behavior rather than attempting completely random guesses.

---

# Types of Password Attacks

The instructor introduced three primary password attack techniques:

1. Dictionary Attack
2. Brute Force Attack
3. Rule-Based Attack

---

# Dictionary Attack

## Definition

A dictionary attack uses a predefined list of likely passwords.

Instead of trying every possible combination, the attacker tests passwords commonly chosen by users.

Example wordlist:

```text
password

password123

admin

welcome

root

qwerty

india123
```

---

## Dictionary Attack Workflow

```text
Password List

↓

Cracking Tool

↓

Target Login / Password Hash

↓

Try Every Password

↓

Match Found
```

---

## Advantages

- Fast
- Efficient
- Works well against weak passwords
- Requires fewer attempts than brute force

---

## Limitations

Fails if:

- Password is long
- Password is random
- Password is not present in the wordlist

---

# Brute Force Attack

## Definition

A brute force attack systematically tries every possible password combination.

Example:

```text
a

b

c

...

aa

ab

ac

...

aaa

aab
```

Eventually every possible password is attempted.

---

## Brute Force Workflow

```text
Generate Password

↓

Attempt Login

↓

Incorrect?

↓

Generate Next Password

↓

Repeat
```

---

## Advantages

Guaranteed to succeed eventually if enough time is available.

---

## Limitations

Very slow for long passwords.

Example:

A four-digit PIN has:

```text
10,000 possibilities
```

An eight-character password containing uppercase letters, lowercase letters, numbers, and symbols has billions of possible combinations.

---

# Dictionary Attack vs Brute Force

| Dictionary Attack | Brute Force |
|-------------------|------------|
| Uses prepared password list | Generates every possible password |
| Fast | Slow |
| Depends on common passwords | Does not require assumptions |
| Efficient against human passwords | Efficient only for short passwords |

---

# Rule-Based Attack

## Definition

A rule-based attack modifies known words using common password creation habits.

Suppose the attacker starts with:

```text
john
```

The attack tool automatically generates:

```text
John123

john@123

John2025

J0hn123

john#123
```

People often create passwords by adding:

- Numbers
- Years
- Symbols
- Capital letters

Rule-based attacks exploit these predictable habits.

---

# Wordlists

## What is a Wordlist?

A wordlist is simply a text file containing thousands or millions of possible passwords.

Example:

```text
admin

password

root

guest

welcome

password123
```

Wordlists are commonly used by:

- Hydra
- Medusa
- John the Ripper
- Hashcat

---

# How Wordlists Are Built

Attackers may create wordlists using:

- Public password leaks
- Employee names
- Company names
- Birthdays
- Social media
- Phone numbers
- Vehicle numbers
- Common passwords
- Dictionary words

This demonstrates why personal information should never be used in passwords.

---

# RockYou Wordlist

One of the most famous password lists is:

```text
rockyou.txt
```

It contains millions of real passwords leaked during a historical data breach.

It is widely used in security training laboratories to demonstrate password cracking.

It should only be used in authorized environments.

---

# Default Passwords

Manufacturers often ship devices using default credentials.

Examples:

```text
admin/admin

admin/password

root/root

root/toor
```

Default passwords are common in:

- Routers
- Firewalls
- Switches
- CCTV Cameras
- DVRs
- IoT Devices
- Web Administration Panels

If administrators fail to change them, attackers may gain access without exploiting any technical vulnerability.

---

# Password Recovery Tools

Password recovery tools are generally intended for legitimate recovery of forgotten passwords.

Examples discussed include:

- Elcomsoft Distributed Password Recovery
- Passware Kit
- Password Recovery Toolkit
- PCUnlocker
- Windows Password Recovery Tool

These tools are commonly used by:

- Digital forensic investigators
- Incident response teams
- System administrators

---

# Password Cracking Tools

The session introduced several password auditing tools.

Examples include:

- John the Ripper
- Hashcat
- THC Hydra
- Medusa
- Ophcrack
- RainbowCrack
- L0phtCrack

Each tool has different strengths depending on whether the attack is online or offline.

---

# John the Ripper

John the Ripper is primarily used for offline password cracking.

It works against password hashes rather than active login services.

Typical workflow:

```text
Password Hash

↓

John the Ripper

↓

Wordlist / Rules

↓

Recovered Password
```

---

# Hashcat

Hashcat is a high-performance password recovery tool.

Unlike many traditional tools, Hashcat can utilize GPU acceleration, allowing billions of password guesses per second depending on the hardware and hash type.

Hashcat supports:

- Dictionary attacks
- Rule-based attacks
- Mask attacks
- Hybrid attacks

---

# Online vs Offline Password Cracking

## Online Cracking

Targets a live authentication service.

Examples:

- SSH
- FTP
- HTTP Login
- RDP

Requires repeated login attempts.

Usually slower due to:

- Account lockout
- Rate limiting
- Network latency

---

## Offline Cracking

Targets exported password hashes.

No communication with the victim is required.

Advantages:

- Much faster
- No account lockouts
- Can utilize GPUs

---

# Hydra

Hydra is an online password guessing tool.

It supports numerous protocols including:

- SSH
- FTP
- HTTP
- HTTPS
- SMB
- RDP
- Telnet

Hydra attempts different username-password combinations against a live service.

---

# Medusa

Medusa is another online password auditing tool.

Like Hydra, it supports multiple network protocols and parallel authentication attempts.

---

# Rainbow Tables

## Definition

A rainbow table is a precomputed database of password hashes.

Instead of computing hashes every time, the attacker simply searches the table.

Workflow:

```text
Hash

↓

Rainbow Table Lookup

↓

Possible Password
```

Rainbow tables become significantly less effective when passwords are salted.

---

# Password Salting

## Definition

Salting means adding a unique random value to every password before hashing.

Example:

```text
Password

↓

Random Salt

↓

Hash
```

Suppose two users choose:

```text
password123
```

Without salting:

```text
Same Password

↓

Same Hash
```

With salting:

```text
password123 + Salt A

↓

Hash A

password123 + Salt B

↓

Hash B
```

Even though the passwords are identical, the hashes become completely different.

---

# Why Salting Matters

Salting protects against:

- Rainbow tables
- Hash comparison attacks
- Large-scale password database attacks

Modern password storage should always include:

- Unique salt
- Slow password hashing algorithm
- Secure password policy

---

# Recommended Password Hashing Algorithms

Suitable algorithms include:

- bcrypt
- scrypt
- Argon2
- PBKDF2

Algorithms such as MD5 and SHA1 should not be used for password storage because they are too fast and no longer considered secure for this purpose.

---

# Strong Password Policy

A secure organization should enforce:

- Long passwords
- Passphrases
- Multi-factor authentication
- Password reuse prevention
- Account lockout
- Login rate limiting
- Continuous monitoring

---

# Key Takeaways

- Authentication verifies identity, while authorization determines permissions.
- Windows stores password hashes rather than plaintext passwords.
- NTLM and Kerberos are important Microsoft authentication protocols.
- Dictionary attacks exploit common passwords.
- Brute force attacks try every possible combination.
- Rule-based attacks exploit predictable password creation habits.
- RockYou is a widely used password wordlist for security training.
- Default passwords remain a common real-world security weakness.
- John the Ripper and Hashcat are primarily used for offline password recovery.
- Hydra and Medusa perform online password attacks against live services.
- Salting protects password hashes against precomputed attacks.
- Secure password storage requires strong hashing algorithms and unique salts.

# Session 10 – Password Cracking, Exploitation, Privilege Escalation and Post-Exploitation
## Part 1 – Overview, Authentication, Password Cracking and Password Storage

---

# Overview

This session focuses on the stages of a cyber attack that occur after reconnaissance and vulnerability identification. Once an attacker discovers a vulnerable target, the next objectives are to gain access, increase privileges, execute malicious code, maintain persistence, and hide evidence of compromise.

Unlike previous sessions, which concentrated on reconnaissance, scanning, enumeration, and vulnerability identification, this session shifts focus toward exploitation and post-exploitation techniques.

The major topics covered include:

- Microsoft authentication mechanisms
- Password storage
- Password cracking
- Password attack techniques
- Password recovery tools
- Password cracking tools
- Password salting
- Exploitation fundamentals
- Privilege escalation
- Post exploitation
- Remote code execution
- Practical demonstrations using Kali Linux and Metasploitable

The instructor emphasized that all demonstrations should only be performed in authorized laboratory environments such as Kali Linux, Metasploitable, DVWA, or systems where explicit permission has been granted.

---

# Ethical Boundary

Every technique discussed during this session is intended for:

- Authorized penetration testing
- Personal laboratory environments
- Vulnerable virtual machines
- Educational purposes

These techniques must **never** be used against systems that you do not own or do not have written authorization to test.

A simple rule followed by every ethical hacker is:

```text
No Permission
        =
No Testing
```

Ethics separates a penetration tester from an attacker.

---

# Attack Lifecycle

This session covers the middle portion of a penetration testing engagement.

Complete attack lifecycle:

```text
Reconnaissance
        ↓
Scanning
        ↓
Enumeration
        ↓
Vulnerability Assessment
        ↓
Exploitation
        ↓
Privilege Escalation
        ↓
Persistence
        ↓
Post Exploitation
        ↓
Covering Tracks
        ↓
Reporting
```

The primary focus of this session is:

```text
Exploitation

↓

Privilege Escalation

↓

Post Exploitation
```

---

# Authentication

## What is Authentication?

Authentication is the process of verifying the identity of a user, device, or application before granting access to resources.

Authentication answers the question:

```text
Who are you?
```

Examples include:

- Username and password
- Fingerprint
- Face recognition
- OTP
- Smart cards
- Security keys

Only after successful authentication does the system determine what actions the user is allowed to perform.

---

# Authentication vs Authorization

Students often confuse these two concepts.

## Authentication

Authentication verifies identity.

Example:

```text
Username

+

Password

↓

Identity Verified
```

---

## Authorization

Authorization determines what the authenticated user is allowed to access.

Example:

```text
Authenticated User

↓

Can View Dashboard

↓

Cannot Delete Users
```

Authentication comes first.

Authorization comes second.

---

# Microsoft Authentication

Modern Windows systems use multiple authentication mechanisms.

The session introduces two important authentication protocols:

- NTLM
- Kerberos

Before understanding these protocols, it is important to understand how Windows stores user credentials.

---

# Security Accounts Manager (SAM)

## What is SAM?

SAM stands for:

```text
Security Accounts Manager
```

It is a Windows database that stores information about local user accounts.

SAM contains:

- Usernames
- Password hashes
- Account identifiers
- Security information

One of the most important security concepts is:

Windows does **not** store user passwords directly.

Instead, Windows stores password hashes.

---

# Password vs Password Hash

## Password

The password is the secret chosen by the user.

Example:

```text
Password123
```

---

## Hash

A hash is the output of a mathematical function applied to the password.

Example:

```text
Password123

↓

Hash Function

↓

482c811da5d5b4bc6d497ffa98491e38
```

The original password cannot easily be recovered from the hash.

Authentication works by hashing the entered password and comparing it with the stored hash.

---

# Why Hash Passwords?

Suppose passwords were stored directly.

Example:

```text
admin : password123

john : hello123
```

If an attacker steals the database, every password becomes immediately available.

Instead, systems store:

```text
admin : 482c811da5d5...

john : 94b5f87...
```

Although hashes can sometimes be cracked, they provide significantly better protection than plaintext passwords.

---

# NTLM Authentication

## What is NTLM?

NTLM stands for:

```text
NT LAN Manager
```

It is a Microsoft authentication protocol used by Windows systems.

Although Kerberos is now preferred in Active Directory environments, NTLM remains important because many legacy systems still support it.

---

# Why NTLM is Targeted

Attackers frequently target NTLM because:

- NTLM hashes can sometimes be captured.
- Weak passwords can be cracked offline.
- Legacy environments still depend on NTLM.
- Misconfigured systems may allow relay attacks.

---

# LM Hashes vs NTLM Hashes

Earlier Windows systems used LM hashes.

LM hashing had several weaknesses:

- Passwords converted to uppercase.
- Password divided into smaller blocks.
- Weak cryptographic design.
- Easier brute-force attacks.

NTLM improved upon LM but still has limitations.

Modern enterprise environments generally prefer Kerberos.

---

# Kerberos Authentication

## What is Kerberos?

Kerberos is a ticket-based authentication protocol designed to provide stronger security than NTLM.

Instead of repeatedly sending authentication information, Kerberos issues encrypted tickets.

Authentication flow:

```text
User Logs In

↓

Domain Controller Verifies Identity

↓

Ticket Granted

↓

Ticket Used to Access Services
```

---

# Advantages of Kerberos

Kerberos provides:

- Mutual authentication
- Ticket-based authentication
- Strong encryption
- Better protection against replay attacks
- Efficient authentication within Active Directory

However, Kerberos can still be attacked if administrators use weak passwords or poor configurations.

Examples include:

- Kerberoasting
- AS-REP Roasting
- Weak Service Account Passwords

---

# Password Cracking

## Definition

Password cracking is the process of recovering passwords by testing guesses against:

- Login systems
- Password hashes
- Encrypted password databases
- Protected files

Password cracking is commonly performed during:

- Password auditing
- Security assessments
- Penetration testing
- Digital forensics

---

# Why Password Cracking Works

Most successful password attacks occur because users choose predictable passwords.

Examples include:

```text
password123

admin123

welcome

company@123

john1998

india123
```

Attackers take advantage of predictable human behavior rather than attempting completely random guesses.

---

# Types of Password Attacks

The instructor introduced three primary password attack techniques:

1. Dictionary Attack
2. Brute Force Attack
3. Rule-Based Attack

---

# Dictionary Attack

## Definition

A dictionary attack uses a predefined list of likely passwords.

Instead of trying every possible combination, the attacker tests passwords commonly chosen by users.

Example wordlist:

```text
password

password123

admin

welcome

root

qwerty

india123
```

---

## Dictionary Attack Workflow

```text
Password List

↓

Cracking Tool

↓

Target Login / Password Hash

↓

Try Every Password

↓

Match Found
```

---

## Advantages

- Fast
- Efficient
- Works well against weak passwords
- Requires fewer attempts than brute force

---

## Limitations

Fails if:

- Password is long
- Password is random
- Password is not present in the wordlist

---

# Brute Force Attack

## Definition

A brute force attack systematically tries every possible password combination.

Example:

```text
a

b

c

...

aa

ab

ac

...

aaa

aab
```

Eventually every possible password is attempted.

---

## Brute Force Workflow

```text
Generate Password

↓

Attempt Login

↓

Incorrect?

↓

Generate Next Password

↓

Repeat
```

---

## Advantages

Guaranteed to succeed eventually if enough time is available.

---

## Limitations

Very slow for long passwords.

Example:

A four-digit PIN has:

```text
10,000 possibilities
```

An eight-character password containing uppercase letters, lowercase letters, numbers, and symbols has billions of possible combinations.

---

# Dictionary Attack vs Brute Force

| Dictionary Attack | Brute Force |
|-------------------|------------|
| Uses prepared password list | Generates every possible password |
| Fast | Slow |
| Depends on common passwords | Does not require assumptions |
| Efficient against human passwords | Efficient only for short passwords |

---

# Rule-Based Attack

## Definition

A rule-based attack modifies known words using common password creation habits.

Suppose the attacker starts with:

```text
john
```

The attack tool automatically generates:

```text
John123

john@123

John2025

J0hn123

john#123
```

People often create passwords by adding:

- Numbers
- Years
- Symbols
- Capital letters

Rule-based attacks exploit these predictable habits.

---

# Wordlists

## What is a Wordlist?

A wordlist is simply a text file containing thousands or millions of possible passwords.

Example:

```text
admin

password

root

guest

welcome

password123
```

Wordlists are commonly used by:

- Hydra
- Medusa
- John the Ripper
- Hashcat

---

# How Wordlists Are Built

Attackers may create wordlists using:

- Public password leaks
- Employee names
- Company names
- Birthdays
- Social media
- Phone numbers
- Vehicle numbers
- Common passwords
- Dictionary words

This demonstrates why personal information should never be used in passwords.

---

# RockYou Wordlist

One of the most famous password lists is:

```text
rockyou.txt
```

It contains millions of real passwords leaked during a historical data breach.

It is widely used in security training laboratories to demonstrate password cracking.

It should only be used in authorized environments.

---

# Default Passwords

Manufacturers often ship devices using default credentials.

Examples:

```text
admin/admin

admin/password

root/root

root/toor
```

Default passwords are common in:

- Routers
- Firewalls
- Switches
- CCTV Cameras
- DVRs
- IoT Devices
- Web Administration Panels

If administrators fail to change them, attackers may gain access without exploiting any technical vulnerability.

---

# Password Recovery Tools

Password recovery tools are generally intended for legitimate recovery of forgotten passwords.

Examples discussed include:

- Elcomsoft Distributed Password Recovery
- Passware Kit
- Password Recovery Toolkit
- PCUnlocker
- Windows Password Recovery Tool

These tools are commonly used by:

- Digital forensic investigators
- Incident response teams
- System administrators

---

# Password Cracking Tools

The session introduced several password auditing tools.

Examples include:

- John the Ripper
- Hashcat
- THC Hydra
- Medusa
- Ophcrack
- RainbowCrack
- L0phtCrack

Each tool has different strengths depending on whether the attack is online or offline.

---

# John the Ripper

John the Ripper is primarily used for offline password cracking.

It works against password hashes rather than active login services.

Typical workflow:

```text
Password Hash

↓

John the Ripper

↓

Wordlist / Rules

↓

Recovered Password
```

---

# Hashcat

Hashcat is a high-performance password recovery tool.

Unlike many traditional tools, Hashcat can utilize GPU acceleration, allowing billions of password guesses per second depending on the hardware and hash type.

Hashcat supports:

- Dictionary attacks
- Rule-based attacks
- Mask attacks
- Hybrid attacks

---

# Online vs Offline Password Cracking

## Online Cracking

Targets a live authentication service.

Examples:

- SSH
- FTP
- HTTP Login
- RDP

Requires repeated login attempts.

Usually slower due to:

- Account lockout
- Rate limiting
- Network latency

---

## Offline Cracking

Targets exported password hashes.

No communication with the victim is required.

Advantages:

- Much faster
- No account lockouts
- Can utilize GPUs

---

# Hydra

Hydra is an online password guessing tool.

It supports numerous protocols including:

- SSH
- FTP
- HTTP
- HTTPS
- SMB
- RDP
- Telnet

Hydra attempts different username-password combinations against a live service.

---

# Medusa

Medusa is another online password auditing tool.

Like Hydra, it supports multiple network protocols and parallel authentication attempts.

---

# Rainbow Tables

## Definition

A rainbow table is a precomputed database of password hashes.

Instead of computing hashes every time, the attacker simply searches the table.

Workflow:

```text
Hash

↓

Rainbow Table Lookup

↓

Possible Password
```

Rainbow tables become significantly less effective when passwords are salted.

---

# Password Salting

## Definition

Salting means adding a unique random value to every password before hashing.

Example:

```text
Password

↓

Random Salt

↓

Hash
```

Suppose two users choose:

```text
password123
```

Without salting:

```text
Same Password

↓

Same Hash
```

With salting:

```text
password123 + Salt A

↓

Hash A

password123 + Salt B

↓

Hash B
```

Even though the passwords are identical, the hashes become completely different.

---

# Why Salting Matters

Salting protects against:

- Rainbow tables
- Hash comparison attacks
- Large-scale password database attacks

Modern password storage should always include:

- Unique salt
- Slow password hashing algorithm
- Secure password policy

---

# Recommended Password Hashing Algorithms

Suitable algorithms include:

- bcrypt
- scrypt
- Argon2
- PBKDF2

Algorithms such as MD5 and SHA1 should not be used for password storage because they are too fast and no longer considered secure for this purpose.

---

# Strong Password Policy

A secure organization should enforce:

- Long passwords
- Passphrases
- Multi-factor authentication
- Password reuse prevention
- Account lockout
- Login rate limiting
- Continuous monitoring

---

# Key Takeaways

- Authentication verifies identity, while authorization determines permissions.
- Windows stores password hashes rather than plaintext passwords.
- NTLM and Kerberos are important Microsoft authentication protocols.
- Dictionary attacks exploit common passwords.
- Brute force attacks try every possible combination.
- Rule-based attacks exploit predictable password creation habits.
- RockYou is a widely used password wordlist for security training.
- Default passwords remain a common real-world security weakness.
- John the Ripper and Hashcat are primarily used for offline password recovery.
- Hydra and Medusa perform online password attacks against live services.
- Salting protects password hashes against precomputed attacks.
- Secure password storage requires strong hashing algorithms and unique salts.

# Session 10 – Password Cracking, Exploitation, Privilege Escalation and Post-Exploitation
## Part 2 – Vulnerability Exploitation, CVE, Exploit Databases and Privilege Escalation

---

# Introduction

After an attacker gains initial access to a system—whether through password cracking, phishing, social engineering, or exploiting a vulnerability—the next objective is rarely to remain a normal user.

In most real-world attacks, the attacker's goal is to obtain **higher privileges**, eventually reaching **Administrator**, **SYSTEM**, or **root** access.

This section explains:

- Vulnerabilities
- Exploitation
- Public vulnerability databases
- CVEs
- Exploit Database
- Privilege escalation
- UAC
- Common privilege escalation methods
- Defensive measures

---

# From Initial Access to Complete System Control

A successful cyber attack usually follows this progression:

```text
Reconnaissance
        ↓
Scanning
        ↓
Enumeration
        ↓
Find Vulnerability
        ↓
Exploit Vulnerability
        ↓
Gain Initial Access
        ↓
Privilege Escalation
        ↓
Administrator / SYSTEM
        ↓
Post Exploitation
```

Getting access as a normal user is only the beginning.

The attacker now searches for ways to obtain complete control of the machine.

---

# What is a Vulnerability?

A vulnerability is a weakness in hardware, software, configuration, or system design that can be exploited to violate the confidentiality, integrity, or availability of a system.

A vulnerability may exist because of:

- Programming mistakes
- Weak authentication
- Incorrect permissions
- Missing security checks
- Outdated software
- Poor configuration
- Design flaws
- Unpatched operating systems

---

# Examples of Vulnerabilities

Examples include:

- Buffer Overflow
- SQL Injection
- Cross Site Scripting
- Weak Password Policy
- Misconfigured Windows Services
- Default Credentials
- Unpatched Apache Server
- Outdated FTP Server
- Writable Service Executables
- Insecure File Permissions

Every vulnerability represents an opportunity for an attacker.

---

# Vulnerability vs Threat vs Exploit

Students often confuse these three terms.

## Vulnerability

A weakness.

Example:

```text
Outdated Apache Server
```

---

## Threat

Something capable of exploiting the weakness.

Example:

```text
Cyber Criminal
```

---

## Exploit

The actual code or technique used to abuse the weakness.

Example:

```text
Python Exploit Script
```

Relationship:

```text
Vulnerability

↓

Threat

↓

Exploit

↓

Compromise
```

---

# What is Exploitation?

Exploitation is the process of taking advantage of a vulnerability to perform actions that were never intended by the system designer.

Examples:

- Execute malicious code
- Read confidential files
- Bypass authentication
- Escalate privileges
- Install malware
- Obtain a shell
- Execute remote commands

---

# Exploitation Workflow

A penetration tester typically performs the following steps:

```text
Identify Vulnerability

↓

Research Exploit

↓

Verify Applicability

↓

Configure Exploit

↓

Execute

↓

Gain Access

↓

Validate Results
```

Notice that exploitation always comes **after** reconnaissance, scanning, and enumeration.

---

# Public Vulnerability Databases

Cybersecurity professionals rarely discover every vulnerability themselves.

Instead, they rely on publicly available vulnerability databases.

The most important ones include:

- CVE
- Exploit Database
- VulDB
- NVD (National Vulnerability Database)

These databases provide standardized information about known security issues.

---

# Common Vulnerabilities and Exposures (CVE)

## What is CVE?

CVE stands for:

```text
Common Vulnerabilities and Exposures
```

It is a globally recognized naming system for publicly disclosed security vulnerabilities.

Each vulnerability receives a unique identifier.

Example:

```text
CVE-2021-44228
```

(Log4Shell)

---

# CVE Naming Format

A CVE follows the format:

```text
CVE-Year-Identifier
```

Example:

```text
CVE-2024-12345
```

Where:

- CVE = Common Vulnerabilities and Exposures
- 2024 = Year assigned
- 12345 = Unique identifier

---

# Why CVEs Are Important

Suppose Microsoft, Cisco, and Rapid7 all discover the same vulnerability.

Without a common naming convention:

Each vendor might use different names.

With CVE:

Everyone refers to the same vulnerability.

Example:

```text
Microsoft

↓

Cisco

↓

ExploitDB

↓

Rapid7

↓

All Reference

CVE-2024-12345
```

This standardization improves communication across the cybersecurity industry.

---

# CVSS Score

Most CVEs are accompanied by a CVSS score.

CVSS stands for:

```text
Common Vulnerability Scoring System
```

It measures the severity of a vulnerability.

Typical ranges:

| Score | Severity |
|-------|----------|
| 0.0 | None |
| 0.1 – 3.9 | Low |
| 4.0 – 6.9 | Medium |
| 7.0 – 8.9 | High |
| 9.0 – 10.0 | Critical |

Higher scores indicate vulnerabilities that should be prioritized.

---

# National Vulnerability Database (NVD)

The National Vulnerability Database expands upon CVE entries by providing:

- Detailed descriptions
- CVSS scores
- References
- Affected software
- Mitigation guidance

Many vulnerability scanners use NVD as one of their information sources.

---

# Exploit Database (Exploit-DB)

Exploit Database is a public repository containing proof-of-concept exploits.

Unlike CVE, which only identifies vulnerabilities,

Exploit Database provides actual exploit code for educational and research purposes.

Typical workflow:

```text
Identify Software Version

↓

Search ExploitDB

↓

Locate Matching Exploit

↓

Study Exploit

↓

Test in Authorized Lab
```

---

# Why Version Detection Matters

Imagine the following scenario:

Apache Version:

```text
2.4.18
```

Known vulnerability:

```text
Remote Code Execution
```

However,

Apache:

```text
2.4.62
```

may already contain the patch.

Therefore,

Version Detection is always performed before exploit selection.

---

# VulDB

VulDB is another vulnerability database.

It focuses more on:

- Vulnerability intelligence
- Vendor advisories
- References
- Severity
- Risk assessment

Unlike ExploitDB,

VulDB is not primarily an exploit repository.

---

# Searching for Exploits

Security professionals generally search using:

```text
Software Name

+

Software Version

+

Operating System
```

Example:

```text
vsftpd 2.3.4 exploit

Apache 2.4 exploit

Windows privilege escalation
```

Searching only by software name is usually insufficient because vulnerabilities are often version-specific.

---

# Privilege Escalation

## Definition

Privilege escalation is the process of obtaining permissions higher than those originally assigned.

Example:

```text
Guest

↓

User

↓

Administrator

↓

SYSTEM
```

---

# Why Privilege Escalation Matters

Suppose an attacker compromises a normal employee account.

Initially, they may only be able to:

- Read personal files
- Execute user programs
- Browse accessible folders

After privilege escalation,

they may:

- Dump password hashes
- Disable antivirus
- Create administrator accounts
- Access every user's files
- Install persistence mechanisms
- Modify system settings

---

# Types of Privilege Escalation

There are two major categories.

---

# Vertical Privilege Escalation

Vertical privilege escalation means moving upward in privilege level.

Example:

```text
Standard User

↓

Administrator
```

or

```text
Administrator

↓

SYSTEM
```

This is the most common type discussed during penetration testing.

---

# Horizontal Privilege Escalation

Horizontal privilege escalation occurs when an attacker moves sideways.

Example:

```text
User A

↓

User B
```

Both accounts have similar privilege levels.

However,

the attacker gains access to another user's information.

Example:

Changing:

```text
userID=101
```

to

```text
userID=102
```

without proper authorization.

---

# Causes of Privilege Escalation

Privilege escalation vulnerabilities commonly arise because of:

- Programming errors
- Design flaws
- Weak file permissions
- Writable service executables
- Misconfigured registry entries
- Unpatched operating systems
- Vulnerable drivers
- Weak access control

---

# Privilege Escalation Through Vulnerabilities

Suppose a local service contains a programming bug.

Workflow:

```text
Normal User

↓

Find Local Vulnerability

↓

Execute Exploit

↓

Administrator

↓

SYSTEM
```

The attacker abuses the vulnerability to execute code with elevated privileges.

---

# Why Kernel Vulnerabilities Are Dangerous

The operating system kernel executes with the highest possible privilege.

If the kernel is compromised,

the attacker gains complete control over the operating system.

Capabilities include:

- Read any memory
- Modify kernel structures
- Disable security software
- Install rootkits
- Hide malicious processes

Kernel vulnerabilities therefore receive very high severity ratings.

---

# Privilege Escalation Through Misconfigured Services

Windows services often run with SYSTEM privileges.

Suppose:

```text
Service.exe
```

runs as SYSTEM.

If ordinary users can replace:

```text
Service.exe
```

with a malicious executable,

then restarting the service causes the malicious program to execute as SYSTEM.

This is a common real-world privilege escalation scenario.

---

# Unattended Installation Files

Windows supports automated operating system installation using unattended configuration files.

Examples include:

```text
Unattend.xml
```

These files sometimes contain:

- Administrator passwords
- Domain credentials
- Service account credentials

If administrators forget to remove or protect these files,

attackers may recover sensitive credentials.

---

# Common Locations

Examples include:

```text
C:\Windows\Panther\

C:\Windows\Panther\UnattendGC\

C:\Windows\System32\Sysprep\
```

These locations are commonly examined during authorized penetration tests.

---

# User Account Control (UAC)

## What is UAC?

User Account Control is a Windows security feature designed to reduce accidental administrative actions.

Whenever software requests elevated privileges,

Windows displays a confirmation dialog.

Example:

```text
Allow this application

Yes

No
```

This prevents silent privilege escalation by ordinary applications.

---

# Purpose of UAC

Without UAC,

any application could silently perform administrative actions.

With UAC,

the user is informed whenever privileged operations are requested.

This creates an additional security barrier.

---

# UAC Bypass

The PPT discusses UAC bypass techniques.

A UAC bypass does **not** bypass Windows login.

Instead,

it attempts to execute code with elevated privileges **without displaying the normal UAC prompt**.

Successful UAC bypasses usually depend upon:

- Specific Windows versions
- Misconfigurations
- Trusted auto-elevated components
- Known vulnerabilities

---

# Defense Against Privilege Escalation

The instructor highlighted several defensive strategies.

---

## Principle of Least Privilege

Users should receive only the permissions necessary for their jobs.

Never grant administrator rights unless absolutely required.

---

## Multi-Factor Authentication

Administrative accounts should require multiple authentication factors.

Examples include:

- Password
- OTP
- Authenticator App
- Hardware Security Key

---

## Service Hardening

Services should:

- Run using dedicated accounts
- Avoid SYSTEM unless necessary
- Use strong permissions
- Restrict writable directories

---

## Patch Management

Many privilege escalation vulnerabilities already have security updates.

Regular patching significantly reduces the attack surface.

---

## Secure Coding

Developers should:

- Validate input
- Handle permissions correctly
- Avoid unsafe APIs
- Perform code reviews
- Conduct security testing

---

## Code Auditing

Security reviews help identify:

- Buffer overflows
- Race conditions
- Privilege escalation bugs
- Improper permission handling

before software reaches production.

---

# Interview Questions

## What is privilege escalation?

Privilege escalation is the process of obtaining permissions higher than those originally assigned to a user or process.

---

## Difference between vertical and horizontal privilege escalation?

Vertical privilege escalation increases privilege level.

Horizontal privilege escalation gains access to another account with the same privilege level.

---

## What is UAC?

User Account Control is a Windows security mechanism that prompts users before privileged operations are performed.

---

## What is CVE?

CVE (Common Vulnerabilities and Exposures) is a standardized identifier assigned to publicly disclosed security vulnerabilities.

---

## Difference between CVE and Exploit?

A CVE identifies a vulnerability.

An exploit is code or a technique that abuses the vulnerability.

---

## Why is least privilege important?

Least privilege limits the damage that attackers can cause after compromising an account by ensuring users and services have only the permissions necessary to perform their tasks.

---

# Key Takeaways

- Exploitation uses known vulnerabilities to gain unauthorized capabilities.
- CVEs provide standardized identifiers for publicly disclosed vulnerabilities.
- Exploit Database contains proof-of-concept exploit code for research and education.
- Version detection is essential because exploits are often version-specific.
- Privilege escalation is a common objective after initial system access.
- Vertical privilege escalation increases privilege level, while horizontal privilege escalation targets accounts at the same level.
- Misconfigured services, weak permissions, vulnerable drivers, and unattended installation files are common privilege escalation vectors.
- UAC provides an additional security barrier but is not a substitute for proper system hardening.
- Defenses include least privilege, service hardening, secure coding, regular patching, and strong authentication.

# Session 10 – Password Cracking, Exploitation, Privilege Escalation and Post-Exploitation
## Part 3B – Windows Services, Service Control Manager (SCM), WMI and WinRM

---

# Windows Services

## Introduction

One of the most important concepts introduced during this session is the Windows Service architecture.

Many beginners think that every program starts only when a user opens it.

This is not true.

Windows contains many background programs that start automatically when the operating system boots.

These programs are called **Windows Services**.

A service is a long-running executable that performs specific functions without requiring direct user interaction.

Examples include:

- Windows Update
- Print Spooler
- Windows Defender
- DHCP Client
- DNS Client
- Remote Registry
- SQL Server
- Apache
- MySQL

Services are responsible for keeping the operating system functional.

---

# Characteristics of Windows Services

A Windows Service:

- Runs in the background.
- Does not require a logged-in user.
- Starts automatically or manually.
- Can run continuously for months.
- Can communicate with hardware.
- Can communicate with the network.
- Can execute programs.

---

# Why Services are Important for Attackers

Many services execute with elevated privileges.

Examples:

```text
SYSTEM

Administrator

Network Service

Local Service
```

If an attacker can manipulate one of these services,

the malicious program may inherit the same privileges.

This makes Windows Services one of the most common privilege escalation vectors.

---

# Windows Service Lifecycle

```text
System Boots

↓

Service Control Manager Starts

↓

Required Services Loaded

↓

Service Executes

↓

Waits for Requests

↓

Stops When Requested
```

---

# Service Startup Types

Windows supports several startup modes.

## Automatic

Starts every time Windows boots.

Example:

```text
Windows Defender
```

---

## Automatic (Delayed Start)

Starts shortly after boot to reduce startup load.

---

## Manual

Starts only when requested.

Example:

```text
Database Service
```

---

## Disabled

Cannot start until enabled.

---

# Service Accounts

Every service runs under a security account.

Common service accounts include:

## Local System

Highest privilege.

Almost unrestricted access.

---

## Local Service

Limited local permissions.

Minimal network privileges.

---

## Network Service

Limited local permissions.

Can authenticate on the network.

---

## Custom Service Accounts

Organizations often create dedicated service accounts for applications.

Example:

```text
SQLService

BackupService

WebService
```

This follows the Principle of Least Privilege.

---

# Why SYSTEM is Dangerous

SYSTEM is more powerful than Administrator.

Capabilities include:

- Access any file
- Modify registry
- Load drivers
- Create users
- Disable security software
- Read memory

If malware executes as SYSTEM,

the entire operating system is effectively compromised.

---

# Service Misconfiguration

One of the most common privilege escalation techniques involves weak service configuration.

Suppose:

```text
BackupService.exe
```

runs as SYSTEM.

However,

all users have permission to modify the executable.

Workflow:

```text
Attacker

↓

Replace Service Binary

↓

Restart Service

↓

SYSTEM Executes Malicious Program
```

This is why file permissions are critical.

---

# Common Service Misconfigurations

Examples include:

- Writable executable
- Writable service directory
- Weak registry permissions
- Weak service permissions
- Unquoted service paths
- Incorrect file ownership

Each of these can become a privilege escalation opportunity.

---

# Service Enumeration

During penetration testing,

enumerating Windows Services is an important activity.

Objectives include identifying:

- Service name
- Executable path
- Startup type
- Running account
- File permissions
- Service permissions

The goal is to determine whether a service can be abused for privilege escalation.

---

# Service Control Manager (SCM)

## What is SCM?

SCM stands for:

```text
Service Control Manager
```

It is a core Windows component responsible for managing services.

SCM performs tasks such as:

- Starting services
- Stopping services
- Restarting services
- Monitoring service state
- Managing dependencies

Without SCM,

Windows Services cannot operate correctly.

---

# SCM Workflow

```text
Windows Boots

↓

SCM Starts

↓

Reads Service Configuration

↓

Launches Services

↓

Monitors Services

↓

Restarts if Necessary
```

---

# Why Attackers Target SCM

If attackers gain permission to modify service configuration,

they may:

- Change executable path
- Replace service binary
- Change startup type
- Execute malicious code

Therefore,

service permissions should always be carefully controlled.

---

# Windows Management Instrumentation (WMI)

## Introduction

The PPT introduces Windows Management Instrumentation (WMI) as a Windows management framework.

WMI provides administrators with a standardized interface for querying and managing Windows systems.

Examples include:

- Hardware information
- Software inventory
- Running processes
- Services
- Users
- Operating system information

WMI is widely used by:

- Administrators
- Monitoring software
- Asset management systems
- Enterprise automation tools

---

# WMI Architecture

```text
Administrator

↓

WMI Query

↓

Windows Management Service

↓

Operating System

↓

Results Returned
```

---

# Information Available Through WMI

Examples include:

- CPU details
- Memory
- Disk drives
- Installed software
- Running processes
- Network adapters
- Logged-in users
- BIOS information
- Operating system version

This makes WMI extremely powerful.

---

# Why Attackers Use WMI

Attackers abuse WMI because:

- It already exists on Windows.
- It is trusted.
- Many organizations rely on it.
- It can execute commands remotely.

Examples:

- Execute PowerShell
- Launch programs
- Collect system information
- Move laterally
- Schedule persistence

Using WMI often avoids dropping obvious malware onto disk.

---

# Living Off the Land

The instructor indirectly introduced an important concept.

Rather than installing custom malware,

professional attackers frequently abuse built-in administrative tools.

This technique is known as:

```text
Living Off the Land
```

Examples include:

- WMI
- PowerShell
- cmd.exe
- WinRM
- schtasks
- reg.exe

These tools already exist on Windows,

making them more difficult to detect.

---

# Windows Remote Management (WinRM)

## What is WinRM?

WinRM stands for:

```text
Windows Remote Management
```

It is Microsoft's implementation of the WS-Management protocol.

Its purpose is to allow administrators to manage remote Windows systems.

Examples include:

- Execute commands
- Configure systems
- Install software
- Collect logs
- Run PowerShell remotely

---

# WinRM Workflow

```text
Administrator

↓

WinRM

↓

Remote Windows Computer

↓

Execute Command

↓

Return Output
```

---

# Why Organizations Use WinRM

Large organizations may manage:

- Hundreds
- Thousands
- Tens of thousands

of Windows computers.

Physically visiting every computer is impossible.

WinRM enables centralized administration.

---

# Why Attackers Target WinRM

If attackers obtain valid administrator credentials,

WinRM may allow:

- Remote command execution
- Lateral movement
- Remote PowerShell
- Remote service management

Therefore,

WinRM is frequently encountered during penetration testing.

---

# PowerShell Remoting

PowerShell Remoting is built on WinRM.

Instead of logging into every computer individually,

administrators execute PowerShell commands remotely.

Example workflow:

```text
Administrator

↓

PowerShell

↓

WinRM

↓

Remote Machine

↓

Execute Script

↓

Return Results
```

This greatly simplifies enterprise administration.

---

# WMI vs WinRM

Students often confuse these technologies.

| WMI | WinRM |
|------|--------|
| Management framework | Remote management protocol |
| Queries system information | Executes remote management tasks |
| Used for inventory and monitoring | Used for remote administration |
| Can execute commands | Supports PowerShell Remoting |
| Older management technology | Modern remote administration technology |

---

# Administrative Tools Can Be Abused

Many legitimate administration technologies become dangerous when attackers obtain administrative credentials.

Examples include:

- WMI
- WinRM
- PowerShell
- PsExec
- Scheduled Tasks
- Group Policy

The technology itself is not malicious.

Unauthorized use makes it dangerous.

---

# Defensive Measures

Organizations should protect Windows management technologies by:

- Following Least Privilege.
- Restricting administrator accounts.
- Monitoring remote administration.
- Enabling PowerShell logging.
- Monitoring WMI activity.
- Restricting WinRM access.
- Using Multi-Factor Authentication.
- Applying regular security updates.
- Monitoring service configuration changes.

---

# Interview Questions

## What is a Windows Service?

A Windows Service is a background process that performs system or application tasks without requiring direct user interaction.

---

## What is the Service Control Manager?

SCM is the Windows component responsible for starting, stopping, monitoring, and managing Windows Services.

---

## Why are Windows Services targeted during privilege escalation?

Because many services execute with elevated privileges such as SYSTEM, and misconfigured services may allow attackers to execute code with those privileges.

---

## What is WMI?

Windows Management Instrumentation is a Windows management framework used to retrieve system information and perform administrative tasks.

---

## What is WinRM?

Windows Remote Management is Microsoft's implementation of the WS-Management protocol used for remote administration of Windows systems.

---

## Difference between WMI and WinRM?

WMI provides system management functionality, while WinRM provides the communication mechanism used for remote management and PowerShell remoting.

---

# Key Takeaways

- Windows Services are long-running background processes managed by the Service Control Manager.
- Services often execute with elevated privileges, making them attractive privilege escalation targets when misconfigured.
- The Service Control Manager starts, stops, and monitors Windows Services.
- Windows Management Instrumentation (WMI) provides powerful system management and inventory capabilities.
- Windows Remote Management (WinRM) enables remote administration using the WS-Management protocol.
- PowerShell Remoting is built on WinRM and allows administrators to execute commands remotely.
- Legitimate administrative technologies such as WMI, WinRM, and PowerShell can be abused if attackers obtain administrative credentials.
- Proper permission management, logging, monitoring, and least privilege significantly reduce the risk of abuse.

# Session 10 – Password Cracking, Exploitation, Privilege Escalation and Post-Exploitation
## Part 3C – Remote Administration Tools, Persistence, File Hiding and Rootkits

---

# Remote Administration Tools

## Introduction

Every large organization manages hundreds or even thousands of computers.

It is impractical for an administrator to physically visit every machine whenever software must be installed, updates are required, or troubleshooting is needed.

To solve this problem, organizations use **Remote Administration Tools (RATs)**.

These tools allow administrators to:

- Access remote systems
- Install software
- Collect logs
- Troubleshoot problems
- Execute commands
- Deploy updates
- Monitor system health

The important concept introduced during the session is that **these tools are legitimate administrative utilities**. However, if attackers obtain administrative credentials, the same tools can be abused to move laterally within a network.

---

# Why Remote Administration Tools Exist

Imagine a company with:

```text
5,000 Computers
```

Without remote administration:

```text
Administrator

↓

Walk to Computer 1

↓

Install Software

↓

Walk to Computer 2

↓

Repeat 5,000 Times
```

Clearly impossible.

Instead:

```text
Administrator

↓

Remote Administration Tool

↓

All Systems Managed Centrally
```

---

# Common Features

Most enterprise remote administration tools provide:

- Remote Desktop
- Remote Command Execution
- Software Deployment
- Inventory Collection
- Patch Management
- Remote File Transfer
- PowerShell Execution
- Event Log Collection
- Remote Registry Access

---

# PsExec

## What is PsExec?

PsExec is part of Microsoft's Sysinternals Suite.

It allows administrators to execute commands on remote Windows systems.

Instead of opening Remote Desktop,

administrators can directly execute commands remotely.

General workflow:

```text
Administrator

↓

PsExec

↓

Remote Computer

↓

Execute Command

↓

Return Output
```

---

# Why Administrators Use PsExec

Common uses include:

- Restarting services
- Installing software
- Running scripts
- Troubleshooting
- Collecting logs

It is lightweight and widely used in Windows administration.

---

# Why Attackers Like PsExec

If attackers obtain valid administrator credentials,

PsExec allows:

- Remote command execution
- Lateral movement
- Malware deployment
- Remote process execution

The tool itself is legitimate.

Unauthorized use makes it dangerous.

---

# PDQ Deploy

## Purpose

PDQ Deploy is an enterprise software deployment solution.

Administrators use it to install software on multiple computers simultaneously.

Example:

```text
Administrator

↓

PDQ Deploy

↓

500 Computers

↓

Install Chrome
```

Instead of manually installing software,

deployment becomes automated.

---

# Security Perspective

If attackers gain access to PDQ Deploy,

they may distribute:

- Malware
- Backdoors
- Persistence tools

across many systems simultaneously.

Therefore,

access to deployment servers should be carefully protected.

---

# DameWare

DameWare is another enterprise remote administration platform.

Capabilities include:

- Remote Desktop
- Remote Command Execution
- Service Management
- Event Viewer
- Registry Editing
- User Management

It is commonly used by IT support teams.

---

# Ninja

Ninja (often called NinjaOne) is a Remote Monitoring and Management (RMM) platform.

Capabilities include:

- Endpoint monitoring
- Patch management
- Remote access
- Software deployment
- Asset inventory
- Performance monitoring

Modern Managed Service Providers (MSPs) frequently use RMM platforms such as Ninja.

---

# ManageEngine Desktop Central

Desktop Central (Endpoint Central) is an enterprise endpoint management solution.

It provides:

- Patch management
- Software deployment
- Configuration management
- Asset inventory
- Remote troubleshooting

Large organizations use such platforms to centrally manage thousands of devices.

---

# Why Attackers Target RMM Tools

Remote Management software already possesses:

- Administrative privileges
- Remote connectivity
- Access to many systems

If compromised,

one management server may provide access to an entire enterprise.

This is why attackers increasingly target RMM infrastructure.

---

# Living Off the Land

Rather than installing suspicious malware,

professional attackers frequently abuse existing administration software.

Examples include:

- PsExec
- PowerShell
- WMI
- WinRM
- Remote Desktop
- Scheduled Tasks

This approach reduces the likelihood of detection.

---

# Persistence

## Definition

Persistence refers to techniques that allow attackers to regain access after the initial compromise.

Without persistence,

the attacker loses access when:

- The computer restarts.
- Passwords are changed.
- Sessions expire.

Persistence ensures continued access.

---

# Why Persistence Matters

Suppose an attacker successfully compromises a server.

The server restarts overnight.

Without persistence:

```text
Access Lost
```

With persistence:

```text
Restart

↓

Malicious Component Starts Automatically

↓

Attacker Reconnects
```

---

# Common Persistence Mechanisms

Examples include:

- Startup folders
- Registry Run Keys
- Windows Services
- Scheduled Tasks
- WMI Event Subscriptions
- Startup Scripts
- Browser Extensions
- Login Scripts

Modern endpoint security products actively monitor these mechanisms.

---

# Hiding Files

The PPT introduces techniques used to conceal files from casual observation.

The objective is not to make files impossible to find,

but rather to reduce the chance of detection.

Examples include:

- Hidden file attributes
- Alternate Data Streams
- Steganography
- Rootkits

---

# Hidden File Attributes

Operating systems allow files to be marked as:

```text
Hidden
```

These files are not displayed by default in file explorers.

However,

security professionals can still view them using appropriate tools or settings.

Therefore,

hidden attributes provide very limited protection.

---

# NTFS Alternate Data Streams (ADS)

## Introduction

NTFS supports a feature called Alternate Data Streams.

Normally,

a file contains one stream:

```text
Document.txt
```

However,

NTFS allows additional hidden streams to exist.

Example:

```text
Document.txt:hidden
```

The visible file appears unchanged,

while additional information exists inside another stream.

---

# Legitimate Uses of ADS

ADS was originally introduced to support compatibility with Macintosh file systems.

Windows also uses ADS for metadata.

Examples include:

- Zone information
- Download source
- File properties

---

# Why Attackers Abuse ADS

Attackers may hide:

- Scripts
- Configuration data
- Malware components

inside alternate streams.

Casual inspection may not reveal the hidden content.

Modern forensic tools and endpoint protection products can detect ADS.

---

# Steganography

## Definition

Steganography is the process of hiding information inside another file.

Unlike encryption,

the goal is to conceal the existence of the information itself.

Examples include:

- Hidden text inside images
- Hidden files inside audio
- Hidden messages inside video

---

# Encryption vs Steganography

Students often confuse these concepts.

## Encryption

Protects the content.

Everyone knows data exists,

but cannot read it.

---

## Steganography

Hides the existence of the data.

Observers may not even realize secret information is present.

---

# Example

Image:

```text
holiday.jpg
```

Appears completely normal.

However,

secret information may be embedded inside the image without visibly changing it.

---

# Rootkits

## Definition

A rootkit is malicious software designed to hide the presence of an attacker or malware on a compromised system.

Rather than performing the attack,

its primary purpose is concealment.

---

# Rootkit Objectives

Rootkits attempt to hide:

- Processes
- Files
- Registry entries
- Network connections
- Services
- Drivers

This makes detection more difficult.

---

# Types of Rootkits

Examples include:

### User Mode Rootkits

Operate within user applications.

---

### Kernel Mode Rootkits

Execute inside the operating system kernel.

These are more powerful and more difficult to detect.

---

### Bootkits

Execute before the operating system loads.

---

### Firmware Rootkits

Reside inside firmware components.

These are rare but highly persistent.

---

# Why Rootkits Are Dangerous

A successful rootkit may:

- Hide malware
- Hide attacker activity
- Hide files
- Hide network traffic
- Disable security software

The operating system itself may report false information because the rootkit intercepts requests.

---

# Detecting Rootkits

Detection methods include:

- Memory analysis
- Integrity verification
- Offline scanning
- Boot-time scanning
- EDR monitoring
- Kernel integrity checks

Modern endpoint protection products include specialized rootkit detection capabilities.

---

# Blue Team Perspective

Every technique discussed in this section has corresponding defensive controls.

Examples:

| Offensive Technique | Defensive Measure |
|---------------------|-------------------|
| PsExec | Restrict admin accounts, monitor remote execution |
| PowerShell | Enable PowerShell logging |
| WMI | Monitor WMI event subscriptions |
| WinRM | Restrict access and require MFA |
| Hidden Files | Periodic file integrity monitoring |
| ADS | Endpoint detection tools |
| Rootkits | Secure Boot, EDR, offline scanning |
| Persistence | Startup auditing, scheduled task monitoring |

---

# Principle of Least Privilege

Many post-exploitation techniques become impossible if administrators follow:

```text
Principle of Least Privilege
```

Users should receive only the permissions necessary for their work.

Administrative privileges should be granted only when required.

---

# Defense in Depth

Organizations should never rely on a single security control.

Instead,

multiple layers should work together.

Example:

```text
Firewall

↓

Antivirus

↓

EDR

↓

MFA

↓

Least Privilege

↓

Logging

↓

SIEM

↓

Incident Response
```

Even if one layer fails,

others continue protecting the environment.

---

# Interview Questions

## What is persistence?

Persistence is the ability for an attacker to maintain access to a compromised system even after reboot, logout, or password changes.

---

## What is PsExec?

PsExec is a Microsoft Sysinternals tool used to execute commands on remote Windows systems.

---

## What are Remote Administration Tools?

Remote Administration Tools are legitimate software used by administrators to manage computers remotely. Examples include PsExec, PDQ Deploy, DameWare, and Endpoint Central.

---

## What is an Alternate Data Stream?

An Alternate Data Stream is an NTFS feature that allows multiple data streams to exist within a single file.

---

## Difference between encryption and steganography?

Encryption protects the contents of data.

Steganography hides the existence of the data.

---

## What is a rootkit?

A rootkit is malware designed primarily to hide malicious activity by concealing files, processes, services, drivers, or network connections.

---

# Key Takeaways

- Remote Administration Tools are essential for enterprise system management but may be abused if attackers obtain administrative credentials.
- PsExec, PDQ Deploy, DameWare, NinjaOne, and Endpoint Central are examples of legitimate administrative tools.
- Persistence techniques allow attackers to survive system reboots and session termination.
- NTFS Alternate Data Streams provide additional hidden storage within files and can be abused to conceal malicious content.
- Steganography hides information inside other files, whereas encryption protects the content of visible data.
- Rootkits focus on hiding malicious activity rather than performing the initial attack.
- Defense in depth, least privilege, endpoint detection, monitoring, and regular auditing significantly reduce the effectiveness of post-exploitation techniques.


# Session 10 – Password Cracking, Exploitation, Privilege Escalation and Post Exploitation
# Part 4 – Practical Lab Setup (Kali Linux & Metasploitable 2)

---

# Introduction

The second half of this session shifted from theoretical concepts to a practical penetration testing demonstration.

The instructor demonstrated the complete workflow using two virtual machines:

- Kali Linux (Attacker Machine)
- Metasploitable 2 (Victim Machine)

The purpose of this lab was **not simply to exploit a machine**, but to demonstrate the complete penetration testing methodology discussed in previous sessions.

Students observed how an attacker moves through the following stages:

```text
Prepare Lab
      ↓
Verify Connectivity
      ↓
Discover Hosts
      ↓
Scan Ports
      ↓
Identify Services
      ↓
Search Vulnerabilities
      ↓
Select Exploit
      ↓
Gain Access
      ↓
Perform Post Exploitation
```

This workflow represents one of the most common penetration testing methodologies used in real-world assessments.

---

# Lab Environment

The instructor used the following laboratory environment.

## Attacker Machine

Operating System

```text
Kali Linux
```

Purpose

- Reconnaissance
- Scanning
- Enumeration
- Exploitation
- Password Cracking

Kali Linux comes pre-installed with hundreds of penetration testing tools including:

- Nmap
- Metasploit Framework
- Hydra
- John the Ripper
- Burp Suite
- Wireshark
- sqlmap
- Netdiscover

---

## Victim Machine

Operating System

```text
Metasploitable 2
```

Purpose

Metasploitable is an intentionally vulnerable Linux virtual machine developed for security training.

Unlike a normal Linux server, Metasploitable intentionally contains:

- Outdated software
- Weak passwords
- Vulnerable services
- Misconfigured applications

The goal is to safely practice penetration testing techniques.

---

# Why Metasploitable?

The instructor specifically chose Metasploitable because it contains numerous real-world vulnerabilities.

Examples include:

- Vulnerable FTP server
- Vulnerable Samba service
- Vulnerable Web Server
- Weak authentication
- Default credentials
- Old software versions

Instead of attacking production systems,

students attack a machine that is intentionally insecure.

---

# VirtualBox Architecture

Both machines were running inside Oracle VirtualBox.

```
+------------------------------------------------+
|              Host Computer                     |
|                                                |
|   +--------------------+                       |
|   | Kali Linux VM      |                       |
|   +--------------------+                       |
|                                                |
|   +--------------------+                       |
|   | Metasploitable VM  |                       |
|   +--------------------+                       |
|                                                |
+------------------------------------------------+
```

Communication occurs through VirtualBox virtual networking.

---

# Why Networking Matters

Before scanning,

both virtual machines must communicate.

If networking is incorrect,

nothing else will work.

Examples:

```text
Nmap

×

Metasploit

×

Hydra

×

SSH

×

FTP

×

Ping
```

Everything depends on network connectivity.

---

# Network Adapters in VirtualBox

VirtualBox provides several networking modes.

The instructor discussed these while troubleshooting connectivity.

---

# NAT (Network Address Translation)

In NAT mode,

the virtual machine can access the Internet,

but other virtual machines generally cannot initiate connections to it.

```
VM
 │
 ▼
VirtualBox NAT
 │
 ▼
Internet
```

Advantages

- Easy Internet access
- Simple configuration

Disadvantages

- Difficult for penetration testing
- Machines cannot freely discover each other

---

# Bridged Adapter

In Bridged mode,

the virtual machine behaves like another physical computer on the network.

```
Router
 │
 ├──────── Laptop
 │
 ├──────── Phone
 │
 └──────── Kali VM
```

Advantages

- Receives its own IP
- Accessible from the LAN

Disadvantages

- Not ideal for isolated practice labs

---

# Host-Only Adapter

Host-Only networking creates a private network between:

- Host Computer
- Virtual Machines

```
Host
 │
 ├──── Kali
 │
 └──── Metasploitable
```

Advantages

- Safe
- Isolated
- Commonly used in labs

---

# Internal Network

Internal Network isolates communication completely.

```
Kali
 │
 ▼
Virtual Network
 │
 ▼
Metasploitable
```

No Internet access.

Only participating virtual machines communicate.

---

# Which Mode is Best?

For penetration testing practice,

Host-Only or Internal Network is generally preferred because:

- Safe
- Isolated
- Predictable
- No risk to external devices

---

# IP Address Verification

Before scanning,

both systems must have valid IP addresses.

Typical command on Kali

```bash
ip addr
```

or

```bash
ifconfig
```

Example output

```text
eth0

192.168.56.101
```

Metasploitable

```text
192.168.56.102
```

Both machines must belong to the same subnet.

---

# Understanding the Subnet

Example

```
Kali

192.168.56.101

Metasploitable

192.168.56.102
```

Network

```
192.168.56.0/24
```

Since both belong to the same subnet,

communication is possible.

---

# Connectivity Test

Before performing reconnaissance,

always verify communication.

Command

```bash
ping 192.168.56.102
```

Expected output

```text
64 bytes from 192.168.56.102

icmp_seq=1

ttl=64

time=0.4 ms
```

Successful replies indicate:

- Layer 3 connectivity
- IP configuration correct
- Machines reachable

---

# Understanding Ping

Ping uses:

```text
ICMP

Internet Control Message Protocol
```

Purpose

- Test connectivity
- Measure latency
- Confirm host availability

Ping is one of the first commands executed during penetration testing.

---

# Understanding TTL

The instructor briefly discussed TTL values.

TTL means

```text
Time To Live
```

TTL limits how many routers a packet may traverse.

Every router decreases TTL by one.

When TTL reaches zero,

the packet is discarded.

---

# Why TTL Helps Fingerprinting

Different operating systems use different default TTL values.

Typical examples

```text
Linux

64

Windows

128

Cisco

255
```

These values help estimate the target operating system during reconnaissance.

However,

TTL alone should never be considered definitive.

---

# Common Connectivity Problems

During the demonstration,

networking issues occurred before scanning began.

Typical causes include:

- Wrong adapter selected
- Different subnets
- VM powered off
- Duplicate IP address
- Incorrect DHCP configuration
- Firewall blocking traffic
- Internal Network name mismatch

---

# Troubleshooting Workflow

Whenever two virtual machines cannot communicate,

follow this sequence:

```text
Check VM Power

↓

Check Adapter Type

↓

Check Adapter Enabled

↓

Verify IP Address

↓

Verify Subnet

↓

Ping

↓

Verify Firewall

↓

Proceed to Scanning
```

Skipping these checks often wastes significant troubleshooting time.

---

# Why the Instructor Spent Time on Networking

Students often want to jump directly to exploitation.

However,

professional penetration testers know that **successful attacks depend on proper preparation**.

Poor networking configuration leads to:

- Failed scans
- False assumptions
- Incorrect vulnerability analysis
- Exploit failures

Therefore,

network verification is always the first practical step.

---

# Practical Best Practices

Before beginning any assessment:

- Verify IP addresses.
- Verify subnet masks.
- Test connectivity using `ping`.
- Confirm that the target is reachable.
- Ensure both machines are in the intended virtual network.
- Record IP addresses for documentation.

---

# Interview Questions

## Why is Host-Only networking commonly used in penetration testing labs?

Because it isolates the lab from external networks while allowing communication between virtual machines.

---

## Why should connectivity be verified before running Nmap?

If the target is unreachable, scan results will be misleading or empty. Verifying connectivity prevents unnecessary troubleshooting later.

---

## What is the purpose of Ping?

Ping uses ICMP to verify whether a remote host is reachable and to measure network latency.

---

## What does TTL indicate?

TTL (Time To Live) limits the number of network hops a packet can traverse. Its default value can also provide clues about the target operating system.

---

# Key Takeaways

- Proper lab preparation is the foundation of successful penetration testing.
- Kali Linux serves as the attacker machine, while Metasploitable 2 is an intentionally vulnerable target.
- VirtualBox networking modes determine how virtual machines communicate.
- Host-Only and Internal Network modes are preferred for isolated practice labs.
- Always verify IP configuration and connectivity before beginning reconnaissance.
- Ping and TTL provide valuable initial information during network verification.
- Professional penetration testers always validate the environment before running scanners or exploits.

# Session 10 – Password Cracking, Exploitation, Privilege Escalation and Post Exploitation
# Part 4B – Host Discovery and Enumeration using Netdiscover and Nmap

---

# Introduction

After configuring the laboratory environment and verifying that Kali Linux and Metasploitable could communicate, the instructor began the reconnaissance phase.

The primary objective of reconnaissance is to answer four fundamental questions:

1. Is the target alive?
2. What is the target's IP address?
3. Which services are running?
4. Which vulnerabilities might exist?

Rather than attacking immediately, ethical hackers first collect as much information as possible.

The instructor repeatedly emphasized an important penetration testing principle:

```text
More Information

↓

Better Attack Decisions

↓

Higher Probability of Success
```

Reconnaissance is therefore one of the most important stages of any penetration test.

---

# Passive vs Active Reconnaissance

Before beginning practical scanning, it is important to understand the two types of reconnaissance.

## Passive Reconnaissance

Passive reconnaissance gathers information **without directly interacting with the target**.

Examples:

- Google Search
- Company Website
- LinkedIn
- DNS Records
- WHOIS
- Social Media
- Public GitHub Repositories
- Shodan

Advantages:

- Difficult to detect
- No direct contact with the target
- Useful before penetration testing

---

## Active Reconnaissance

Active reconnaissance involves directly communicating with the target system.

Examples:

- Ping
- Nmap
- Netdiscover
- Banner Grabbing
- Service Enumeration

Advantages:

- Provides accurate technical information
- Reveals live hosts
- Identifies running services

Disadvantages:

- May generate logs
- Can trigger intrusion detection systems
- Easier for defenders to notice

The practical demonstration focused primarily on **active reconnaissance**.

---

# Host Discovery

Before scanning ports, the attacker must determine whether the target machine is online.

Typical workflow:

```text
Unknown Network

↓

Discover Live Hosts

↓

Identify Target IP

↓

Scan Ports

↓

Enumerate Services
```

---

# Netdiscover

## Introduction

The first tool demonstrated during reconnaissance was **Netdiscover**.

Netdiscover is a network reconnaissance tool used to discover live hosts on a local network.

Unlike Nmap, which primarily scans ports, Netdiscover focuses on identifying devices connected to the local subnet.

---

# How Netdiscover Works

Netdiscover uses the **Address Resolution Protocol (ARP)**.

Workflow:

```text
Broadcast ARP Request

↓

Devices Reply

↓

Collect MAC Addresses

↓

Display Live Hosts
```

Since ARP operates within the local network, Netdiscover is extremely effective for LAN host discovery.

---

# Why ARP?

ARP (Address Resolution Protocol) maps:

```text
IP Address

↓

MAC Address
```

When Kali broadcasts an ARP request asking:

```text
Who has 192.168.56.102?
```

The device owning that IP responds with its MAC address.

This allows Netdiscover to build a table of active systems.

---

# Command Used

The instructor demonstrated:

```bash
netdiscover
```

or

```bash
netdiscover -r 192.168.56.0/24
```

where:

- `-r` specifies the IP range to scan.

---

# Sample Output

```text
IP Address        MAC Address             Vendor

192.168.56.1      08:00:27:AA:11:22      Oracle

192.168.56.101    08:00:27:11:22:33      Oracle

192.168.56.102    08:00:27:44:55:66      Oracle
```

---

# Understanding the Output

Each row provides:

### IP Address

The network address of the device.

Example:

```text
192.168.56.102
```

---

### MAC Address

The hardware address of the network interface.

Example:

```text
08:00:27:44:55:66
```

---

### Vendor

The manufacturer identified from the MAC prefix.

Example:

```text
Oracle
```

Since both virtual machines are running in Oracle VirtualBox, Oracle appears as the vendor.

---

# Why Netdiscover is Useful

Netdiscover quickly answers:

- Which devices are online?
- Which IP addresses exist?
- Which MAC addresses belong to those devices?
- Which vendor manufactured the network interface?

This information is valuable before performing deeper scans.

---

# Transition to Nmap

Once the instructor identified the Metasploitable machine, the next step was to determine:

- Which ports are open?
- Which services are running?
- Which operating system is installed?
- Which versions of software are present?

For this purpose, the instructor used **Nmap**.

---

# What is Nmap?

Nmap stands for:

```text
Network Mapper
```

It is one of the most widely used network reconnaissance and security auditing tools.

Nmap is capable of:

- Host discovery
- Port scanning
- Service detection
- Operating system detection
- Version detection
- Script execution
- Vulnerability identification

---

# Why Nmap is Essential

Almost every penetration test begins with Nmap.

Without knowing:

- Open ports
- Running services
- Operating system

it is impossible to choose appropriate exploits.

---

# General Nmap Workflow

```text
Target IP

↓

Host Discovery

↓

Port Scan

↓

Identify Open Ports

↓

Service Detection

↓

Version Detection

↓

Operating System Detection

↓

Attack Planning
```

---

# TCP Ports

A TCP port identifies a specific network service running on a computer.

Examples:

| Port | Service |
|------|----------|
| 21 | FTP |
| 22 | SSH |
| 23 | Telnet |
| 25 | SMTP |
| 53 | DNS |
| 80 | HTTP |
| 110 | POP3 |
| 139 | NetBIOS |
| 143 | IMAP |
| 443 | HTTPS |
| 445 | SMB |
| 3306 | MySQL |

Open ports indicate services that may become attack targets.

---

# Basic Nmap Scan

The instructor demonstrated a basic scan using:

```bash
nmap <target-ip>
```

Example:

```bash
nmap 192.168.56.102
```

Nmap attempts to identify:

- Live host
- Open ports
- Closed ports
- Filtered ports

---

# Understanding Port States

### Open

A service is actively listening.

Example:

```text
22/tcp open ssh
```

---

### Closed

No service is listening.

The machine is reachable.

---

### Filtered

A firewall or filtering device prevented Nmap from determining the port state.

---

# Service Detection

The instructor then demonstrated service detection.

Example command:

```bash
nmap -sV 192.168.56.102
```

The `-sV` option enables:

```text
Service Version Detection
```

Instead of displaying only:

```text
21 open
```

Nmap displays:

```text
21 open ftp vsftpd 2.3.4
```

Software versions are critical because exploits are almost always version-specific.

---

# Operating System Detection

The instructor also demonstrated OS fingerprinting.

Command:

```bash
nmap -O 192.168.56.102
```

The `-O` option attempts to determine the operating system.

Example output:

```text
Linux 2.6.x
```

Nmap estimates the operating system by analyzing:

- TCP responses
- ICMP behavior
- TCP window sizes
- TTL values
- Packet characteristics

---

# Aggressive Scan

One of the most useful demonstrations was the aggressive scan.

Command:

```bash
nmap -A 192.168.56.102
```

The `-A` option combines several advanced features:

- Operating system detection
- Version detection
- Default NSE scripts
- Traceroute

This provides a large amount of information in a single scan.

---

# SYN Scan

The instructor discussed the SYN scan.

Command:

```bash
nmap -sS 192.168.56.102
```

This is often called a **Stealth Scan**.

Instead of completing the full TCP handshake, Nmap sends only the SYN packet and analyzes the response.

Advantages:

- Faster
- Lower network overhead
- Historically more difficult to detect

---

# Understanding Banner Grabbing

Many network services identify themselves when contacted.

Example:

```text
220 (vsFTPd 2.3.4)
```

This is known as a **banner**.

Banner grabbing helps identify:

- Software
- Version
- Vendor

This information guides vulnerability research.

---

# Practical Output Interpretation

Suppose Nmap reports:

```text
21/tcp open ftp vsftpd 2.3.4

22/tcp open ssh OpenSSH

80/tcp open http Apache

3306/tcp open mysql
```

A penetration tester immediately begins asking:

- Is VSFTPD vulnerable?
- Is Apache outdated?
- Can MySQL be accessed?
- Are default credentials present?
- Is anonymous FTP enabled?

Scanning is not the goal.

Scanning provides the information needed to decide **what to test next**.

---

# Professional Penetration Testing Mindset

The instructor emphasized that professionals do **not** attack every open port blindly.

Instead, they prioritize based on:

- Software version
- Known vulnerabilities
- Business impact
- Ease of exploitation

This approach reduces unnecessary risk and improves efficiency.

---

# Interview Questions

## What is Netdiscover?

Netdiscover is a host discovery tool that uses ARP requests to identify live devices on a local network.

---

## Why is ARP used by Netdiscover?

ARP maps IP addresses to MAC addresses, allowing Netdiscover to identify active hosts on the local subnet.

---

## What is Nmap?

Nmap (Network Mapper) is a network scanning tool used for host discovery, port scanning, service detection, operating system fingerprinting, and security auditing.

---

## What does `-sV` do?

It enables service version detection.

---

## What does `-O` do?

It attempts to identify the target operating system.

---

## What does `-A` do?

It performs an aggressive scan by combining OS detection, version detection, default NSE scripts, and traceroute.

---

## What is a SYN scan?

A SYN scan (`-sS`) sends TCP SYN packets without completing the full handshake, making it efficient and historically more difficult to detect than a full TCP connect scan.

---

# Key Takeaways

- Reconnaissance begins by identifying live hosts.
- Netdiscover uses ARP to discover devices on the local network.
- Nmap is one of the most important tools in penetration testing.
- Port scanning identifies potential attack surfaces.
- Service version detection is essential because exploits are version-specific.
- Operating system fingerprinting helps narrow down possible vulnerabilities.
- Banner grabbing provides software and version information.
- The purpose of scanning is to build an informed attack plan, not to attack blindly.

# Session 10 – Password Cracking, Exploitation, Privilege Escalation and Post-Exploitation
## Part 4C – Exploitation using the Metasploit Framework (VSFTPD 2.3.4 Practical)

---

# Introduction

After identifying the target operating system, open ports, and running services using Nmap, the instructor moved to the exploitation phase.

At this point, the penetration tester already knows:

- The target IP address
- The operating system
- The software versions
- The exposed services

Now the objective is to determine whether any of these services contain known vulnerabilities that can be safely demonstrated in the lab.

Rather than writing custom exploit code from scratch, penetration testers commonly use the **Metasploit Framework**, one of the most widely used penetration testing platforms.

---

# What is Metasploit?

The Metasploit Framework is an open-source penetration testing framework that provides a large collection of exploits, payloads, auxiliary modules, encoders, post-exploitation modules, and tools.

It simplifies the exploitation process by providing reusable modules for thousands of known vulnerabilities.

Instead of manually writing exploit code, the tester selects the appropriate exploit module, configures it, and executes it.

---

# Why Metasploit is Important

Metasploit helps security professionals:

- Validate vulnerabilities
- Demonstrate real-world impact
- Test exploitability
- Verify patches
- Perform penetration testing
- Conduct security research

It is used extensively by:

- Penetration Testers
- Red Teams
- Security Researchers
- Incident Response Teams
- Security Consultants

---

# Metasploit Architecture

The framework consists of several module types.

```text
                 Metasploit Framework
                         │
 ┌──────────────┬───────────────┬───────────────┬───────────────┐
 │              │               │               │
Exploits     Payloads      Auxiliary       Post Modules
 │              │               │               │
Exploit     Reverse Shell    Scanner      Privilege Escalation
Buffer OF    Meterpreter     Brute Force  Credential Dumping
RCE          Bind Shell      Fuzzing      Enumeration
```

Each module serves a different purpose.

---

# Main Module Types

## Exploit Modules

Exploit modules take advantage of vulnerabilities.

Example:

```text
vsftpd Backdoor

MS08-067

EternalBlue

Apache Exploits
```

---

## Payload Modules

Payloads determine what happens after exploitation succeeds.

Examples:

- Command Shell
- Reverse Shell
- Meterpreter
- File Download
- PowerShell Execution

---

## Auxiliary Modules

Auxiliary modules perform tasks that do not necessarily exploit vulnerabilities.

Examples:

- Port Scanning
- Banner Grabbing
- SMB Enumeration
- FTP Enumeration
- SSH Login Testing
- Brute Force Attacks

---

## Post Modules

These are executed after successful exploitation.

Examples:

- System Enumeration
- Password Hash Collection
- Privilege Escalation
- Network Discovery
- Persistence

---

# Starting Metasploit

The instructor launched Metasploit using:

```bash
msfconsole
```

This starts the Metasploit interactive console.

During startup,

Metasploit loads:

- Modules
- Plugins
- Database
- Framework Components

After loading,

the user is presented with the Metasploit prompt.

Example:

```text
msf6 >
```

This prompt indicates that the framework is ready.

---

# Searching for Exploits

Rather than memorizing thousands of exploits,

Metasploit provides a search feature.

General syntax:

```bash
search <keyword>
```

Example:

```bash
search vsftpd
```

Metasploit searches its exploit database and returns matching modules.

---

# Understanding Search Results

Typical output contains:

- Module Name
- Disclosure Date
- Rank
- Description

Example:

```text
exploit/unix/ftp/vsftpd_234_backdoor
```

This tells us:

Target Software:

```text
vsftpd
```

Version:

```text
2.3.4
```

Exploit Type:

```text
FTP Backdoor
```

---

# Why Search First?

Professionals never assume an exploit exists.

Instead they:

```text
Identify Service

↓

Identify Version

↓

Search Exploit

↓

Verify Compatibility

↓

Configure Module
```

---

# Selecting an Exploit

Once the correct exploit is found,

the instructor selected it using:

```bash
use exploit/unix/ftp/vsftpd_234_backdoor
```

The console prompt changes.

Example:

```text
msf6 exploit(vsftpd_234_backdoor) >
```

This confirms that the exploit module has been loaded.

---

# Viewing Module Information

Before launching any exploit,

a penetration tester should understand:

- What vulnerability it targets
- Supported platforms
- Required parameters
- References
- Limitations

Command:

```bash
info
```

This displays detailed information about the selected module.

---

# Viewing Required Options

Each exploit requires certain parameters.

The instructor demonstrated:

```bash
show options
```

Typical output includes:

```text
RHOSTS

RPORT

SSL

TARGET
```

Only after the required values are configured can the exploit execute.

---

# Understanding Important Parameters

## RHOSTS

Remote Host.

The target IP address.

Example:

```text
192.168.56.102
```

---

## RPORT

Remote Port.

Default FTP port:

```text
21
```

---

## TARGET

Specifies the operating system or application version if multiple targets are supported.

---

# Configuring the Target

The instructor configured the target machine using:

```bash
set RHOSTS 192.168.56.102
```

Metasploit responds:

```text
RHOSTS => 192.168.56.102
```

This confirms the parameter has been set successfully.

---

# Verifying Configuration

After setting parameters,

experienced penetration testers run:

```bash
show options
```

again to verify that:

- Required values are present
- No mandatory parameters are missing

Skipping this step often causes exploit failures.

---

# Launching the Exploit

After configuration,

the instructor executed:

```bash
run
```

or equivalently:

```bash
exploit
```

Metasploit begins interacting with the target service.

Typical workflow:

```text
Connect

↓

Verify Service

↓

Trigger Vulnerability

↓

Send Payload

↓

Wait for Response
```

---

# VSFTPD 2.3.4 Backdoor Vulnerability

The practical demonstration focused on:

```text
vsftpd 2.3.4
```

This version contains a well-known backdoor that was accidentally introduced into a maliciously modified source package in 2011.

The backdoored version allows an attacker to obtain a shell under specific conditions.

Because Metasploitable intentionally includes this vulnerable version,

it is commonly used in cybersecurity training.

---

# Why This Works in Metasploitable

Metasploitable is intentionally designed to contain vulnerable software.

The objective is educational.

This exploit succeeds because:

- The vulnerable version is installed.
- No security patches have been applied.
- The environment is isolated.

In production environments,

patched versions would not be vulnerable.

---

# Successful Exploitation

If exploitation succeeds,

Metasploit displays output similar to:

```text
Command shell session opened
```

This indicates that the attacker has successfully obtained command execution on the target.

---

# What is a Session?

A session represents an active connection between the attacker and the compromised machine.

Example:

```text
Session 1
```

Each successful exploit generally creates a new session.

Multiple compromised machines may result in multiple active sessions.

---

# Interacting with the Session

To interact with the shell:

```bash
sessions
```

Displays all active sessions.

Example:

```text
ID   Name    Type

1            Shell
```

To connect:

```bash
sessions -i 1
```

Metasploit switches to the compromised system.

---

# Verifying Access

One of the first commands executed after exploitation is:

```bash
whoami
```

Purpose:

Determine the current user.

Example output:

```text
root
```

This confirms that exploitation resulted in root-level access.

---

# Basic Post-Exploitation Commands

The instructor demonstrated simple Linux commands to verify control over the victim machine.

Examples include:

Current directory:

```bash
pwd
```

List files:

```bash
ls
```

Display operating system information:

```bash
uname -a
```

Current user:

```bash
whoami
```

Hostname:

```bash
hostname
```

These commands help the tester understand the compromised environment.

---

# Demonstrating Control

To demonstrate successful exploitation,

the instructor performed simple file operations.

Examples:

Create a directory:

```bash
mkdir demo
```

Create a file:

```bash
touch test.txt
```

List files:

```bash
ls
```

Remove the file:

```bash
rm test.txt
```

These actions demonstrate that commands are executing on the victim machine rather than on Kali Linux.

---

# Why Simple Commands Matter

The objective is **not** to damage the system.

Instead,

the penetration tester proves that:

- Code execution exists.
- Administrative privileges have been obtained.
- The vulnerability is real.

This proof is later included in the penetration testing report.

---

# Cleaning Up

Professional penetration testers avoid leaving unnecessary changes on the target.

After demonstrating the vulnerability,

temporary files created during testing should be removed.

The system should be returned to its original state whenever possible.

---

# Practical Lessons from the Demonstration

The VSFTPD lab demonstrates several important concepts:

- Vulnerable software versions are dangerous.
- Service version detection directly influences exploit selection.
- Metasploit simplifies exploitation but still requires understanding of the target.
- Successful exploitation should always be verified.
- Ethical penetration testing focuses on demonstrating impact, not causing damage.

---

# Interview Questions

## What is the Metasploit Framework?

Metasploit is an open-source penetration testing framework that provides exploits, payloads, scanners, and post-exploitation modules for security testing.

---

## What does `msfconsole` do?

It launches the interactive Metasploit Framework console.

---

## What is the purpose of the `search` command?

It searches the Metasploit module database for exploits, payloads, auxiliary modules, or post-exploitation modules.

---

## What is `RHOSTS`?

`RHOSTS` specifies the IP address or addresses of the target system.

---

## What is the difference between `run` and `exploit`?

Both commands execute the configured exploit. In most modules, they are functionally equivalent.

---

## What is a Metasploit session?

A session is an active connection established between the attacker and a successfully exploited target.

---

## Why was VSFTPD 2.3.4 vulnerable?

The version used in Metasploitable contains a well-known backdoored release intended for educational demonstration. Modern patched versions are not affected.

---

# Key Takeaways

- Metasploit is a modular penetration testing framework that simplifies vulnerability validation.
- Exploit selection is based on accurate service and version detection.
- `msfconsole`, `search`, `use`, `show options`, `set RHOSTS`, and `run` form the core exploitation workflow.
- Successful exploitation creates a session that allows interaction with the compromised system.
- Simple verification commands such as `whoami`, `pwd`, and `ls` confirm successful remote code execution.
- Ethical penetration testing emphasizes demonstrating vulnerabilities safely and documenting evidence rather than damaging the target system.


