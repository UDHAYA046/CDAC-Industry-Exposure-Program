<img width="634" height="860" alt="image" src="https://github.com/user-attachments/assets/3f49eb4f-caf6-4fe5-8c8e-d9b932070109" />
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

