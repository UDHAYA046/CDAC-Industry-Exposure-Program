# Appendix B – Interview & Revision Guide
## Part 1 – Frequently Asked Interview Questions (Session 10)

---

# Introduction

This appendix contains the most important interview, viva, certification, and exam questions from Session 10.

These questions are based on:

- Password Cracking
- Exploitation
- Privilege Escalation
- Metasploit
- Nmap
- Windows Services
- WMI
- WinRM
- Rootkits
- Persistence
- Practical Demonstration

---

# Authentication & Passwords

## Q1. What is Authentication?

Authentication is the process of verifying the identity of a user, system, or application before access is granted.

Examples include:

- Username and Password
- OTP
- Biometrics
- Smart Cards
- Security Keys

---

## Q2. What is Authorization?

Authorization determines what an authenticated user is allowed to access or perform.

Authentication answers:

```text
Who are you?
```

Authorization answers:

```text
What are you allowed to do?
```

---

## Q3. Authentication vs Authorization

| Authentication | Authorization |
|---------------|---------------|
| Verifies identity | Determines permissions |
| Happens first | Happens after authentication |
| Example: Login | Example: File access |

---

## Q4. Why are passwords hashed?

Passwords are hashed to prevent storing plaintext passwords.

Benefits:

- Prevents direct password disclosure
- Protects user credentials
- Makes password databases harder to abuse

---

## Q5. What is a password hash?

A password hash is the output of a one-way cryptographic hash function applied to a password.

Example:

```text
Password

↓

Hash Function

↓

Hash Value
```

---

## Q6. What is password salting?

Salting adds a unique random value to every password before hashing.

Benefits:

- Prevents identical hashes
- Defeats rainbow tables
- Improves password security

---

## Q7. What are rainbow tables?

Rainbow tables are precomputed databases of password hashes used to recover weak passwords quickly.

Modern password salting makes rainbow tables much less effective.

---

## Q8. Dictionary Attack vs Brute Force Attack

| Dictionary Attack | Brute Force |
|-------------------|------------|
| Uses wordlist | Tries every combination |
| Faster | Slower |
| Relies on common passwords | Works regardless of password choice |
| Efficient against weak passwords | Guaranteed eventually but time-consuming |

---

## Q9. What is a Rule-Based Attack?

A rule-based attack modifies existing words by applying predictable patterns.

Example:

```text
admin

↓

Admin123

↓

Admin@2025

↓

@dm1n123
```

---

## Q10. Difference between Online and Offline Password Cracking

| Online | Offline |
|----------|----------|
| Attacks live login services | Attacks password hashes |
| Slower | Faster |
| Subject to account lockout | No account lockout |
| Generates logs | Usually silent |

---

# Exploitation

## Q11. What is a Vulnerability?

A vulnerability is a weakness that can be exploited to violate system security.

Examples:

- Buffer Overflow
- SQL Injection
- Weak Permissions
- Outdated Software

---

## Q12. What is an Exploit?

An exploit is code or a technique that abuses a vulnerability.

---

## Q13. Vulnerability vs Exploit

| Vulnerability | Exploit |
|---------------|----------|
| Weakness | Tool or code that abuses the weakness |
| Passive condition | Active attack mechanism |

---

## Q14. What is Remote Code Execution (RCE)?

Remote Code Execution allows an attacker to execute arbitrary code on a remote system.

It is one of the most severe vulnerability categories because it may lead to complete system compromise.

---

## Q15. Why is RCE dangerous?

Successful Remote Code Execution may allow:

- Full system control
- Malware installation
- Data theft
- Privilege escalation
- Lateral movement

---

## Q16. Client-side vs Server-side Exploitation

| Client-side | Server-side |
|--------------|-------------|
| Targets user applications | Targets network services |
| Victim opens malicious file | Attacker targets exposed service |
| Example: PDF exploit | Example: FTP exploit |

---

# CVE and Vulnerabilities

## Q17. What is CVE?

CVE stands for:

```text
Common Vulnerabilities and Exposures
```

It provides standardized identifiers for publicly disclosed vulnerabilities.

---

## Q18. What is CVSS?

CVSS stands for:

```text
Common Vulnerability Scoring System
```

It measures vulnerability severity.

---

## Q19. What is Exploit-DB?

Exploit Database is a public repository containing proof-of-concept exploits for educational and research purposes.

---

## Q20. Difference between CVE and Exploit-DB

| CVE | Exploit-DB |
|------|------------|
| Vulnerability identifier | Exploit repository |
| Describes vulnerability | Contains exploit code |
| Standardized naming | Practical exploitation |

---

# Privilege Escalation

## Q21. What is Privilege Escalation?

Privilege escalation is the process of obtaining permissions higher than those originally assigned.

---

## Q22. Vertical vs Horizontal Privilege Escalation

| Vertical | Horizontal |
|-----------|------------|
| Gain higher privileges | Access another user with same privilege |
| User → Administrator | User A → User B |

---

## Q23. Why is Privilege Escalation important?

Because initial access often provides limited permissions.

Higher privileges enable:

- Password dumping
- Service modification
- Security bypass
- System control

---

## Q24. What is UAC?

User Account Control is a Windows security mechanism that prompts users before privileged operations.

---

## Q25. Why is Least Privilege important?

Least Privilege limits the damage that attackers can cause after compromising an account.

---

# Windows Services

## Q26. What is a Windows Service?

A Windows Service is a background program that runs independently of user interaction.

---

## Q27. What is the Service Control Manager (SCM)?

SCM manages Windows Services by:

- Starting services
- Stopping services
- Monitoring services
- Managing dependencies

---

## Q28. Why are Windows Services attractive attack targets?

Many services run with SYSTEM privileges.

Misconfigured services may allow privilege escalation.

---

# WMI & WinRM

## Q29. What is WMI?

Windows Management Instrumentation is a management framework used to collect system information and perform administrative tasks.

---

## Q30. What is WinRM?

Windows Remote Management is Microsoft's implementation of the WS-Management protocol for remote administration.

---

## Q31. Difference between WMI and WinRM

| WMI | WinRM |
|------|--------|
| Management framework | Remote management protocol |
| System information | Remote administration |
| Inventory | PowerShell remoting |

---

# Remote Administration

## Q32. What is PsExec?

PsExec is a Microsoft Sysinternals utility that executes commands remotely on Windows systems.

---

## Q33. What are Remote Administration Tools?

Examples include:

- PsExec
- PDQ Deploy
- DameWare
- NinjaOne
- Endpoint Central

They simplify enterprise administration but may be abused if attackers obtain administrative credentials.

---

# Rootkits & Persistence

## Q34. What is Persistence?

Persistence allows attackers to maintain access after reboot, logout, or password changes.

---

## Q35. What is a Rootkit?

A rootkit is malware designed to hide malicious activity by concealing files, processes, services, or drivers.

---

## Q36. What is Steganography?

Steganography hides information inside another file, such as an image or audio file.

---

## Q37. Encryption vs Steganography

| Encryption | Steganography |
|-------------|---------------|
| Protects content | Hides existence of data |
| Data remains visible | Data is concealed |

---

# Practical Questions

## Q38. Why was Metasploitable used?

Metasploitable is intentionally vulnerable, making it suitable for practicing penetration testing safely.

---

## Q39. Why was Kali Linux used?

Kali Linux includes hundreds of penetration testing tools such as:

- Nmap
- Metasploit
- Hydra
- Burp Suite
- Wireshark

---

## Q40. Why is Nmap used before Metasploit?

Metasploit requires knowledge of:

- Open ports
- Running services
- Software versions

Nmap provides this information.

---

## Q41. What is a Metasploit Session?

A session is an active connection between the attacker and a compromised system.

---

## Q42. Difference between an Exploit and a Payload

| Exploit | Payload |
|----------|----------|
| Gains execution | Performs action after exploitation |

---

## Q43. What is a Reverse Shell?

A Reverse Shell is a shell where the victim initiates the connection back to the attacker.

---

## Q44. Why are Reverse Shells common?

Because outbound connections are often allowed through firewalls, while inbound connections are blocked.

---

## Q45. What is Banner Grabbing?

Banner grabbing retrieves service information such as:

- Software name
- Version
- Vendor

It helps identify vulnerabilities.

---

# Scenario-Based Questions

## Q46.

A service is running as SYSTEM but its executable is writable by normal users.

What vulnerability exists?

**Answer:**

Privilege Escalation through insecure service permissions.

---

## Q47.

An Nmap scan shows:

```text
21/tcp open ftp vsftpd 2.3.4
```

What should you do next?

**Answer:**

Research known vulnerabilities affecting VSFTPD 2.3.4 and verify whether an exploit exists before attempting exploitation.

---

## Q48.

Why should a penetration tester verify software versions before exploiting a target?

**Answer:**

Exploits are usually version-specific. Using the wrong exploit wastes time and may crash services without achieving the objective.

---

## Q49.

Why should penetration testers document every successful exploit?

**Answer:**

To provide evidence for the client, demonstrate impact, and support remediation recommendations.

---

## Q50.

What is the most important lesson from Session 10?

**Answer:**

A successful penetration test is a structured process:

```text
Reconnaissance

↓

Scanning

↓

Enumeration

↓

Vulnerability Identification

↓

Exploitation

↓

Privilege Escalation

↓

Post Exploitation

↓

Reporting
```

The objective is not simply to compromise systems but to identify, validate, document, and help remediate security weaknesses in an ethical and authorized manner.


# Appendix B – Interview & Revision Guide
## Part 2 – Complete Revision Sheet, Important Ports, Mind Maps and Final Cheat Sheet

---

# Complete Penetration Testing Workflow

The entire penetration testing lifecycle discussed throughout the CDAC sessions can be summarized as follows:

```text
Planning & Scope Definition
            │
            ▼
Reconnaissance
(Passive + Active)
            │
            ▼
Host Discovery
            │
            ▼
Port Scanning
            │
            ▼
Service Enumeration
            │
            ▼
Operating System Detection
            │
            ▼
Vulnerability Identification
            │
            ▼
Exploit Research
            │
            ▼
Exploitation
            │
            ▼
Privilege Escalation
            │
            ▼
Post Exploitation
            │
            ▼
Persistence
            │
            ▼
Cleanup
            │
            ▼
Reporting
```

---

# End-to-End Practical Workflow

The practical session followed approximately the following workflow:

```text
Start Kali Linux

↓

Start Metasploitable

↓

Verify VirtualBox Network

↓

Verify IP Address

↓

Ping Target

↓

Discover Host

↓

Nmap Scan

↓

Detect Services

↓

Detect Versions

↓

Search Exploit

↓

Launch Metasploit

↓

Configure Exploit

↓

Execute Exploit

↓

Obtain Shell

↓

Verify Access

↓

Run Linux Commands

↓

Document Results
```

---

# Password Attack Decision Tree

```text
Need Password?

        │

        ▼

Is Login Available?

       │

 ┌─────┴─────┐

 │           │

Yes         No

 │           │

 ▼           ▼

Hydra      Hash Available?

               │

        ┌──────┴──────┐

        │             │

      Yes            No

        │

        ▼

Hashcat / John

        │

        ▼

Dictionary Attack

        │

        ▼

Rule-Based Attack

        │

        ▼

Brute Force
```

---

# Vulnerability Assessment Workflow

```text
Software Found

↓

Identify Version

↓

Search CVE

↓

Search ExploitDB

↓

Read Vulnerability Details

↓

Verify Conditions

↓

Choose Appropriate Exploit

↓

Lab Testing

↓

Document Findings
```

---

# Exploitation Workflow

```text
Reconnaissance

↓

Scanning

↓

Enumeration

↓

Identify Vulnerability

↓

Load Exploit

↓

Configure Options

↓

Execute

↓

Gain Shell

↓

Privilege Escalation

↓

Post Exploitation
```

---

# Post Exploitation Workflow

```text
Shell Obtained

↓

Identify Current User

↓

Check Operating System

↓

Check Network

↓

Check Installed Software

↓

Collect Information

↓

Privilege Escalation

↓

Persistence

↓

Cleanup

↓

Reporting
```

---

# Metasploit Workflow

```text
msfconsole

↓

search

↓

use

↓

info

↓

show options

↓

set RHOSTS

↓

set RPORT

↓

run / exploit

↓

sessions

↓

sessions -i

↓

Verify Access
```

---

# Nmap Workflow

```text
Target IP

↓

Host Discovery

↓

Port Scan

↓

Service Detection

↓

Version Detection

↓

OS Detection

↓

Banner Grabbing

↓

Exploit Research
```

---

# Network Troubleshooting Workflow

```text
VM Running?

↓

Correct Adapter?

↓

Correct IP?

↓

Same Subnet?

↓

Ping Successful?

↓

Nmap Scan

↓

Exploit
```

---

# Important Ports

| Port | Service | Protocol | Common Usage |
|------|----------|----------|--------------|
| 20 | FTP Data | TCP | File Transfer |
| 21 | FTP | TCP | File Transfer |
| 22 | SSH | TCP | Secure Remote Login |
| 23 | Telnet | TCP | Remote Login |
| 25 | SMTP | TCP | Email Sending |
| 53 | DNS | TCP/UDP | Domain Resolution |
| 67 | DHCP | UDP | IP Assignment |
| 68 | DHCP Client | UDP | Client Configuration |
| 69 | TFTP | UDP | Trivial File Transfer |
| 80 | HTTP | TCP | Web Traffic |
| 110 | POP3 | TCP | Email Retrieval |
| 123 | NTP | UDP | Time Synchronization |
| 135 | RPC | TCP | Windows RPC |
| 137 | NetBIOS Name | UDP | Windows Networking |
| 138 | NetBIOS Datagram | UDP | Windows Networking |
| 139 | NetBIOS Session | TCP | File Sharing |
| 143 | IMAP | TCP | Email Retrieval |
| 161 | SNMP | UDP | Network Monitoring |
| 389 | LDAP | TCP | Directory Services |
| 443 | HTTPS | TCP | Secure Web |
| 445 | SMB | TCP | Windows File Sharing |
| 514 | Syslog | UDP | Logging |
| 636 | LDAPS | TCP | Secure LDAP |
| 1433 | MS SQL | TCP | Database |
| 1521 | Oracle | TCP | Database |
| 2049 | NFS | TCP | File Sharing |
| 3306 | MySQL | TCP | Database |
| 3389 | RDP | TCP | Remote Desktop |
| 5432 | PostgreSQL | TCP | Database |
| 5900 | VNC | TCP | Remote Desktop |
| 6379 | Redis | TCP | In-Memory Database |
| 8080 | HTTP Alternate | TCP | Web Applications |

---

# Common Kali Tools

| Tool | Purpose |
|------|----------|
| Nmap | Network Scanning |
| Netdiscover | Host Discovery |
| Metasploit | Exploitation Framework |
| Hydra | Online Password Cracking |
| John the Ripper | Offline Password Cracking |
| Hashcat | GPU Password Cracking |
| Burp Suite | Web Security Testing |
| Wireshark | Packet Analysis |
| sqlmap | SQL Injection Testing |
| Gobuster | Directory Enumeration |
| Nikto | Web Server Scanning |
| Aircrack-ng | Wireless Security |

---

# Common Metasploit Commands

| Command | Purpose |
|----------|----------|
| msfconsole | Start Framework |
| search | Search Modules |
| use | Load Module |
| info | Module Details |
| show options | Display Parameters |
| set | Configure Parameters |
| run | Execute Module |
| exploit | Execute Exploit |
| sessions | List Sessions |
| sessions -i | Interact with Session |
| back | Exit Current Module |
| exit | Quit Metasploit |

---

# Common Linux Commands

| Command | Purpose |
|----------|----------|
| pwd | Current Directory |
| ls | List Files |
| ls -la | Show Hidden Files |
| cd | Change Directory |
| mkdir | Create Directory |
| touch | Create File |
| cat | Display File |
| rm | Delete File |
| rmdir | Delete Directory |
| whoami | Current User |
| hostname | Host Name |
| id | User Information |
| uname -a | System Information |
| ifconfig | Network Configuration |
| ip addr | Network Configuration |
| ping | Connectivity Test |

---

# Common Nmap Options

| Option | Description |
|---------|-------------|
| -sS | SYN Scan |
| -sT | TCP Connect Scan |
| -sU | UDP Scan |
| -sV | Version Detection |
| -O | OS Detection |
| -A | Aggressive Scan |
| -p | Specific Ports |
| -p- | All Ports |
| -v | Verbose Output |
| -oN | Save Normal Output |
| -oX | Save XML Output |
| -oA | Save All Formats |

---

# Remember These Definitions

### Authentication

Verifying identity.

---

### Authorization

Determining permissions.

---

### Vulnerability

A weakness in a system.

---

### Exploit

Code that abuses a vulnerability.

---

### Payload

Action executed after exploitation.

---

### Session

An active connection with a compromised machine.

---

### Privilege Escalation

Obtaining higher permissions.

---

### Persistence

Maintaining access after reboot or logout.

---

### Rootkit

Malware designed to hide malicious activity.

---

### Steganography

Hiding data inside another file.

---

### Alternate Data Stream

Additional hidden data stream supported by NTFS.

---

### CVE

Common Vulnerabilities and Exposures.

---

### CVSS

Common Vulnerability Scoring System.

---

# Common Mistakes During Practical

Students frequently make the following mistakes:

- Using the wrong target IP address.
- Placing VMs on different VirtualBox networks.
- Forgetting to verify connectivity before scanning.
- Running exploits without confirming the software version.
- Assuming every open port is vulnerable.
- Ignoring service banners.
- Forgetting to document successful exploitation.
- Leaving test files on the victim machine.
- Confusing the attacker machine with the victim machine.
- Forgetting to verify current privileges after exploitation.

---

# Practical Best Practices

Before scanning:

- Verify networking.
- Verify IP addresses.
- Test connectivity.

Before exploiting:

- Confirm service version.
- Read exploit documentation.
- Configure options carefully.

After exploitation:

- Verify current user.
- Record screenshots.
- Document evidence.
- Remove temporary files.
- Close sessions properly.

---

# Common Interview Mistakes

Avoid saying:

❌ "Nmap is a hacking tool."

Instead say:

✅ "Nmap is a network discovery and security auditing tool."

---

❌ "Metasploit hacks computers."

Instead say:

✅ "Metasploit is a penetration testing framework used to validate known vulnerabilities in authorized environments."

---

❌ "Hydra cracks passwords."

Instead say:

✅ "Hydra performs online password auditing against supported network authentication services."

---

❌ "Rootkits attack computers."

Instead say:

✅ "Rootkits are designed primarily to conceal malicious activity after compromise."

---

# One-Page Last-Minute Revision

Remember the sequence:

```text
Recon

↓

Scanning

↓

Enumeration

↓

Version Detection

↓

Vulnerability Research

↓

Exploitation

↓

Privilege Escalation

↓

Persistence

↓

Reporting
```

Remember the important tools:

```text
Netdiscover

↓

Nmap

↓

Metasploit

↓

Hydra

↓

John

↓

Hashcat

↓

Burp Suite
```

Remember the important concepts:

```text
Authentication

↓

Authorization

↓

Password Security

↓

Reconnaissance

↓

Scanning

↓

Exploitation

↓

Privilege Escalation

↓

Post Exploitation
```

---

# Final Session Summary

By the end of this session, students should be able to:

- Explain password storage and password cracking techniques.
- Differentiate between dictionary, brute-force, and rule-based attacks.
- Understand CVEs, CVSS, and exploit databases.
- Describe privilege escalation techniques and defensive controls.
- Explain Windows Services, SCM, WMI, and WinRM.
- Understand persistence, rootkits, ADS, and steganography.
- Configure a penetration testing lab using Kali Linux and Metasploitable.
- Discover hosts using Netdiscover.
- Perform reconnaissance using Nmap.
- Identify vulnerable services and software versions.
- Use the Metasploit Framework to validate a known vulnerability.
- Verify successful exploitation through a remote shell.
- Document findings following ethical penetration testing practices.

---

# Final Note

The most important lesson from this session is that penetration testing is **a structured, repeatable, and ethical process**. Successful assessments depend far more on careful reconnaissance, accurate analysis, disciplined methodology, and clear documentation than on simply running exploit tools. Understanding each stage of the attack lifecycle enables security professionals to identify weaknesses responsibly and recommend effective defenses.
