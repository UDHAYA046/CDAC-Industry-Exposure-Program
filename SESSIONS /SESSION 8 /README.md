
# Session 8 – Web Application Security: Vulnerability Scanning

**Course:** CDAC Industry Exposure Program – Cybersecurity  
**Module:** 4 – Web Application Security  
**Topic:** Vulnerability Scanning

---

# Overview

After learning manual web application security testing using tools such as **Burp Suite**, **OWASP ZAP**, and vulnerable applications like **DVWA**, this session introduces the concept of **automated vulnerability scanning**.

The instructor described vulnerability scanners as:

> "The automated first sweep — the tools that tell you where to point your manual skills."

A penetration tester should never rely solely on automated tools. Instead, scanners are used to quickly identify **potential weaknesses**, which are later verified manually.

This session focuses on three widely used vulnerability scanners:

- **Nmap NSE**
- **Nikto**
- **OpenVAS (Greenbone Vulnerability Manager)**

The practical section demonstrates how these tools are used in an isolated penetration testing lab consisting of Kali Linux and DVWA/Metasploitable.

---

# Learning Objectives

By the end of this session, you should understand:

- What vulnerability scanning is.
- Why vulnerability scanning is different from penetration testing.
- Where vulnerability scanning fits within the penetration testing lifecycle.
- The strengths and weaknesses of automated scanners.
- The purpose of Nmap NSE, Nikto, and OpenVAS.
- Why scanner results must always be validated manually.
- How automated scanning complements Burp Suite and OWASP ZAP.

---

# Position of Vulnerability Scanning in the Penetration Testing Lifecycle

The slide introduces the following workflow:

```text
Reconnaissance
        ↓
Scanning
        ↓
Validation
        ↓
Exploitation
        ↓
Reporting
```

Each phase has a distinct purpose.

---

## 1. Reconnaissance

The objective is to gather information about the target.

Typical information includes:

- IP addresses
- Domain names
- Subdomains
- Technologies
- Employees
- Public documents

Example tools:

- Google Dorks
- WHOIS
- DNS lookup
- Shodan
- theHarvester

Output of this phase:

```text
"I know what the target looks like."
```

---

## 2. Vulnerability Scanning

After identifying the target, automated scanners perform hundreds or thousands of security checks.

Their objective is to answer:

```text
"What is probably vulnerable?"
```

Examples:

- Outdated Apache server
- Weak TLS configuration
- Missing HTTP security headers
- Dangerous HTTP methods
- Known CVEs
- Default credentials
- Misconfigurations

The scanner compares observations against a database of known vulnerabilities.

Output:

```text
"These services might be vulnerable."
```

---

## 3. Validation

The instructor repeatedly emphasized:

> **Never trust scanner output blindly.**

Automated scanners may produce:

- False positives
- Duplicate findings
- Low-impact findings
- Misidentified software versions

Therefore every important finding must be manually confirmed.

Example:

Scanner reports:

```text
Apache 2.4.29
Possible CVEs
```

Validation includes:

- Checking the exact version.
- Confirming the vulnerable module.
- Attempting controlled exploitation.
- Reviewing vendor patches.

Only after validation can the finding be considered genuine.

---

## 4. Exploitation

After validation, the tester attempts to exploit the confirmed vulnerability.

Examples:

- SQL Injection
- Cross-Site Scripting
- File Inclusion
- Authentication bypass

Unlike vulnerability scanners, exploitation demonstrates **actual impact**.

---

## 5. Reporting

Finally, findings are documented.

A report includes:

- Description
- Evidence
- Risk
- Screenshots
- CVSS score
- Remediation

---

# Why Scanning Alone Is Not a Pentest

One of the key concepts in this session is the distinction between **vulnerability scanning** and **penetration testing**.

A scanner can tell you:

```text
"This server MAY be vulnerable."
```

A penetration tester proves:

```text
"This server IS vulnerable."
```

Example:

Scanner:

```text
Apache Version:
2.4.29

Possible CVE-XXXX-XXXX
```

Penetration Tester:

- Verifies version.
- Confirms module.
- Demonstrates exploitation.
- Assesses business impact.
- Documents evidence.

---

# What is Vulnerability Scanning?

## Definition

Vulnerability scanning is an automated process that identifies **known weaknesses** in systems, networks, or web applications by comparing observed configurations and software versions against a vulnerability database.

Unlike manual testing, scanners perform hundreds or thousands of checks automatically.

The PPT defines vulnerability scanning as:

> Automated detection of **known weaknesses** using databases such as CVEs and predefined security checks. :contentReference[oaicite:0]{index=0}

---

# Characteristics of Vulnerability Scanning

## 1. Automated

Once started, the scanner performs all configured checks without human intervention.

Examples:

- Version detection
- Banner grabbing
- Header inspection
- Port analysis
- Known CVE matching

---

## 2. Fast

A scanner may perform hundreds of tests in only a few minutes.

For example:

Instead of manually checking:

- Apache version
- TLS configuration
- HTTP methods
- Directory listings

the scanner performs all checks automatically.

---

## 3. Broad Coverage

Scanners examine many different components simultaneously.

Examples:

- Operating System
- Web Server
- Database
- SSL/TLS
- Authentication
- File Permissions
- HTTP Headers

---

## 4. Detects Only Known Vulnerabilities

This is perhaps the most important limitation.

Scanners compare observations against:

- CVE databases
- Vendor advisories
- Known signatures
- Security rules

They **cannot discover completely new vulnerabilities**.

Examples of issues scanners usually cannot detect:

- Business logic flaws
- Authorization mistakes
- Multi-step workflow issues
- Creative privilege escalation paths
- Novel zero-day vulnerabilities

These require human reasoning.

---

## 5. False Positives

A false positive occurs when the scanner reports a vulnerability that does not actually exist.

Example:

Scanner detects:

```text
Apache 2.4.29
```

and assumes:

```text
Potential Remote Code Execution
```

However,

the administrator may already have backported the security patch.

The version number remains unchanged, but the vulnerability has been fixed.

Therefore:

```text
Scanner says:
Vulnerable

Reality:
Patched
```

This is why:

```text
Validation is mandatory.
```

---

## 6. Noisy

Scanners generate large amounts of network traffic.

They send:

- HTTP requests
- TCP connections
- Banner requests
- Version probes
- Enumeration requests

Because of this:

- Firewalls log them.
- IDS/IPS detects them.
- SOC analysts may receive alerts.

This is why penetration tests are coordinated with the client.

---

# Scanner Philosophy

The instructor summarized the role of scanners very well:

> **A scanner points you toward potential problems. A human confirms whether those problems are real.**

Think of scanners as:

```text
Lead generators
```

not

```text
Decision makers.
```

---

# The Vulnerability Scanning Toolkit

The session introduces three primary tools.

Although they overlap, each focuses on a different layer.

---

## Nmap NSE

### Full Form

Network Mapper

Nmap Scripting Engine

---

### Primary Purpose

Originally, Nmap was designed for:

- Host discovery
- Port scanning
- Service detection

With NSE (Nmap Scripting Engine), it also becomes a lightweight vulnerability scanner.

---

### Best Use Cases

- Service enumeration
- Version detection
- Known vulnerability scripts
- Web enumeration
- Authentication checks

---

### Advantages

- Fast
- Lightweight
- Extremely flexible
- Hundreds of built-in scripts
- Easy integration into penetration testing

---

### Limitations

- Smaller vulnerability database than OpenVAS.
- Requires choosing appropriate scripts.
- Results still require validation.

---

## Nikto

### Definition

Nikto is an open-source web server vulnerability scanner.

Unlike Nmap, Nikto focuses exclusively on web servers.

---

### What Nikto Checks

- Dangerous files
- Default files
- Backup files
- Outdated software
- Risky HTTP methods
- Missing security headers
- Common web server misconfigurations

---

### Advantages

- Very quick.
- Excellent first assessment.
- Free and open source.
- Generates HTML reports.

---

### Limitations

- Very noisy.
- Many false positives.
- Limited to web server assessment.

---

## OpenVAS (Greenbone Vulnerability Manager)

OpenVAS is a comprehensive enterprise vulnerability scanner.

Unlike Nmap or Nikto, OpenVAS performs:

- Infrastructure scanning
- Operating system assessment
- Service analysis
- CVE correlation
- Risk scoring
- Report generation

---

### Features

- Huge vulnerability feed.
- CVSS scoring.
- Web dashboard.
- Report export.
- Remediation suggestions.

---

### Advantages

- Enterprise-grade.
- Very comprehensive.
- Excellent reporting.
- Large vulnerability database.

---

### Limitations

- Heavy installation.
- Large feed downloads.
- Long scan times.
- Requires significant system resources.

---

# Choosing the Right Tool

| Tool | Primary Focus | Best Used For |
|------|---------------|---------------|
| **Nmap NSE** | Network & services | Port scanning, service detection, lightweight vulnerability checks |
| **Nikto** | Web servers | Fast web server assessment and misconfiguration detection |
| **OpenVAS** | Entire infrastructure | Comprehensive vulnerability assessment with risk scoring |

---

# Rule of Thumb

The instructor summarized the tools with a simple rule:

```text
Nmap NSE
↓
Network & Service Layer

Nikto
↓
Web Server Layer

OpenVAS
↓
Complete Infrastructure Assessment
```

These tools complement each other rather than replace one another.

---

# Key Takeaways

- Vulnerability scanning is the automated identification of **known** weaknesses.
- Scanning fits between reconnaissance and manual validation.
- Scanners are fast and broad but not intelligent.
- False positives are common and require validation.
- Nmap NSE focuses on services and network vulnerabilities.
- Nikto specializes in web server assessments.
- OpenVAS provides enterprise-level vulnerability management.
- Automated scanners identify **where** to investigate; penetration testers determine **whether the vulnerability is real**.

  # Session 8 – Web Application Security: Vulnerability Scanning
## Part 2 – Nmap NSE, Nikto and OpenVAS (Detailed)

---

# 1. Nmap Scripting Engine (NSE)

## Introduction

Originally, Nmap (Network Mapper) was developed as a network discovery and port scanning tool.

However, over time it evolved into a powerful penetration testing framework through the addition of the **Nmap Scripting Engine (NSE)**.

Instead of only answering:

```text
Which ports are open?
```

NSE can answer questions like:

```text
Is this service vulnerable?

Does this FTP server allow anonymous login?

Is SMB vulnerable to EternalBlue?

Is the web server exposing dangerous files?

Can I enumerate HTTP directories?
```

NSE transforms Nmap from a network scanner into a lightweight vulnerability scanner.

---

# What is NSE?

NSE stands for:

```text
Nmap Scripting Engine
```

It allows Nmap to execute **Lua scripts** after discovering hosts and services.

Instead of writing separate tools for every protocol, Nmap provides hundreds of reusable scripts.

Each script performs a specific security check.

Example:

```text
HTTP Enumeration

FTP Anonymous Login

SMB Vulnerability Checks

SSL Certificate Analysis

DNS Enumeration

SNMP Enumeration

SSH Algorithms

Known CVE Detection
```

---

# Why NSE is Powerful

Suppose a normal Nmap scan produces:

```text
80/tcp open http Apache 2.4.29

22/tcp open ssh OpenSSH 7.2
```

A normal scan only tells you:

```text
These services exist.
```

NSE goes further.

It asks:

```text
Is Apache vulnerable?

Is SSH using weak algorithms?

Does HTTP expose hidden directories?

Is SMB affected by known vulnerabilities?
```

---

# Internal Working of NSE

```text
Target
      │
      ▼

Host Discovery

      │

Port Scan

      │

Version Detection

      │

Execute Selected NSE Scripts

      │

Collect Results

      │

Generate Findings
```

This makes NSE much more efficient than blindly running scripts against every machine.

---

# NSE Script Categories

The PPT briefly lists categories.

Let's understand each one.

---

## 1. safe

Scripts that are unlikely to affect the target.

Examples:

- Version detection
- Banner grabbing
- Header inspection

Safe scripts are generally suitable even on production systems.

---

## 2. discovery

Used to gather additional information.

Examples:

- DNS information
- SMB shares
- SNMP information
- Hostnames

Purpose:

Increase knowledge about the target.

---

## 3. version

Attempts to identify:

- Software
- Service versions
- Server banners

Example:

```text
Apache 2.4.29

OpenSSH 7.2

MySQL 5.7
```

---

## 4. auth

Authentication-related scripts.

Checks:

- Anonymous FTP login
- Weak authentication
- Default credentials

---

## 5. vuln

The most important category discussed in class.

Purpose:

Search for known vulnerabilities.

These scripts compare:

```text
Observed Service

↓

Known CVEs

↓

Possible Vulnerabilities
```

Example output:

```text
Apache 2.4.29

Possible CVE-2021-41773
```

Notice the wording.

The script says:

```text
Possible
```

It does **not** guarantee exploitation.

---

## 6. exploit

Some scripts attempt controlled exploitation.

These are much more intrusive.

Should only be executed:

- During authorized penetration testing.
- Inside isolated labs.

---

## 7. intrusive

May:

- Crash services
- Consume resources
- Trigger IDS alerts

Never run these on unauthorized systems.

---

# Important NSE Commands

The instructor specifically highlighted these.

---

## Service Detection

```bash
nmap -sV <TARGET>
```

Meaning:

```text
-sV

Service Version Detection
```

Purpose:

Identify:

- Web server
- SSH server
- Database version
- FTP version

Example output:

```text
80/tcp open Apache 2.4.29

22/tcp OpenSSH 8.2
```

---

## Vulnerability Scan

```bash
nmap -sV --script vuln <TARGET>
```

Breakdown:

```text
-sV

↓

Identify service versions

↓

--script vuln

↓

Run vulnerability scripts
```

Output:

Possible:

- CVEs
- SSL issues
- Authentication problems
- Weak services

---

## HTTP Enumeration

```bash
nmap -p80 --script http-enum <TARGET>
```

Purpose:

Enumerate common web directories.

May discover:

```text
/admin

/login

/phpmyadmin

/images

/uploads

/test
```

Useful before manual testing.

---

## Script Help

```bash
nmap --script-help http-enum
```

Purpose:

Explain:

- What the script does.
- Arguments.
- Usage.

Very useful when learning NSE.

---

# Advantages of NSE

✅ Fast

✅ Built into Nmap

✅ Large script library

✅ Easy automation

✅ Excellent reconnaissance

---

# Limitations

Cannot replace manual testing.

May produce:

- False positives
- Missed vulnerabilities
- Version misidentification

---

# Nikto

---

## What is Nikto?

Nikto is an **open-source web server vulnerability scanner**.

Unlike Nmap,

Nikto focuses only on:

```text
Web Servers
```

Examples:

Apache

Nginx

IIS

Lighttpd

Tomcat

---

# Goal of Nikto

Answer:

```text
Is this web server configured securely?
```

Instead of scanning ports,

Nikto examines:

- Dangerous files
- Misconfigurations
- Old software
- Default pages
- Missing headers

---

# How Nikto Works

```text
Target URL

↓

HTTP Requests

↓

Check Thousands of Rules

↓

Generate Findings

↓

Produce Report
```

---

# Things Nikto Checks

## Dangerous Files

Examples:

```text
test.php

backup.zip

admin.old

config.bak
```

These files should never be publicly accessible.

---

## Default Files

Many applications leave:

```text
README

CHANGELOG

INSTALL

examples/
```

These leak valuable information.

---

## Outdated Software

Nikto compares server versions against known databases.

Example:

```text
Apache 2.2

↓

Known Vulnerabilities
```

---

## Dangerous HTTP Methods

HTTP supports methods like:

```text
GET

POST

PUT

DELETE

OPTIONS
```

If PUT or DELETE is enabled unnecessarily,

attackers may upload or remove files.

---

## Missing Security Headers

Nikto checks for headers like:

```text
X-Frame-Options

Content-Security-Policy

X-Content-Type-Options

Strict-Transport-Security
```

Missing headers increase attack surface.

---

# Nikto Commands

## Basic Scan

```bash
nikto -h http://<TARGET>
```

Scans:

Entire web server.

---

## Scan DVWA

```bash
nikto -h http://<TARGET>/dvwa/
```

Targets:

Only the DVWA application.

---

## Generate HTML Report

```bash
nikto -h http://<TARGET> \
-o report.html \
-Format htm
```

Produces:

Evidence suitable for penetration testing reports.

---

# Nikto Output

May report:

```text
Outdated Apache

Directory Listing Enabled

Missing X-Frame-Options

Interesting File Found

Dangerous HTTP Method Enabled
```

Again:

These are leads.

Not confirmed vulnerabilities.

---

# Strengths

Excellent for:

- Initial web server assessment.
- Quick security review.
- Reporting.

---

# Weaknesses

Very noisy.

Can trigger:

- IDS
- WAF
- Firewall alerts

Many findings require manual validation.

---

# OpenVAS (Greenbone Vulnerability Manager)

---

## Introduction

OpenVAS is an enterprise vulnerability management platform.

Unlike Nmap and Nikto,

it performs:

```text
Large Scale Infrastructure Assessment
```

---

# Components

OpenVAS consists of:

```text
Scanner

↓

Vulnerability Feed

↓

Manager

↓

Web Interface

↓

Reports
```

---

# Vulnerability Feed

OpenVAS downloads:

Thousands of vulnerability definitions.

Includes:

- CVEs
- Vendor advisories
- Configuration checks
- Compliance checks

The feed must remain updated.

---

# Workflow

The PPT summarizes the workflow.

Let's expand it.

---

## Step 1

Create Target

Specify:

- IP
- Hostname
- Credentials (optional)

---

## Step 2

Create Scan Task

Choose:

- Scan profile
- Schedule
- Credentials

---

## Step 3

Run Scan

Scanner performs:

Thousands of checks.

---

## Step 4

Generate Report

Findings sorted by:

Critical

High

Medium

Low

Informational

---

## Step 5

Review Remediation

Each finding includes:

- Description
- CVSS
- References
- Solution

---

# Why OpenVAS is Heavy

Compared to Nikto:

OpenVAS:

- Downloads huge feeds.
- Performs thousands of tests.
- Requires database synchronization.
- Consumes significant CPU and RAM.

This makes it unsuitable for quick scans.

---

# Why Organizations Use OpenVAS

Because it provides:

- Scheduled scans.
- Historical tracking.
- Risk dashboards.
- Compliance reports.
- Asset management.

Large enterprises may scan:

Thousands of systems.

---

# Comparison of All Three Tools

| Feature | Nmap NSE | Nikto | OpenVAS |
|----------|----------|--------|----------|
| Focus | Network & Services | Web Server | Entire Infrastructure |
| Speed | Fast | Fast | Slow |
| Resource Usage | Low | Low | High |
| CVE Database | Limited | Moderate | Extensive |
| Reports | Basic | HTML | Enterprise |
| Best Use | Enumeration | Web Assessment | Full Vulnerability Management |

---

# Interview Questions

### Why use Nmap before Nikto?

Because Nmap first identifies:

- Live hosts
- Open ports
- Running services

Nikto can then focus on the discovered web server.

---

### Why is OpenVAS considered enterprise-grade?

Because it includes:

- Large vulnerability feeds
- CVSS scoring
- Scheduling
- Dashboards
- Historical reporting
- Remediation guidance

---

### Can Nikto replace Burp Suite?

No.

Nikto identifies:

```text
Potential web server issues.
```

Burp Suite performs:

```text
Manual application security testing.
```

Both complement each other.

---

# Key Takeaways

- Nmap NSE extends Nmap using Lua scripts for service and vulnerability checks.
- Nikto specializes in identifying web server misconfigurations and exposed resources.
- OpenVAS is a comprehensive enterprise vulnerability management platform.
- None of these tools confirm vulnerabilities automatically.
- Every finding must be manually validated before reporting or exploitation.

  # Session 8 – Web Application Security: Vulnerability Scanning
## Part 3 – Practical Demonstration (Nmap NSE, Nikto & OpenVAS)

---

# Practical Overview

The practical section of this session demonstrates how automated vulnerability scanners are used inside an isolated penetration testing laboratory.

Unlike previous sessions where the focus was on manual testing using Burp Suite or OWASP ZAP, this session demonstrates how scanners quickly identify **potential vulnerabilities** before manual verification.

The instructor repeatedly emphasized:

> **Scanners are noisy. Only scan systems you own or have explicit authorization to test.**

The laboratory environment consisted of:

- Kali Linux (Attacker Machine)
- DVWA (Damn Vulnerable Web Application)
- Metasploitable 2
- Host-only VirtualBox Network

---

# Why Use an Isolated Lab?

Vulnerability scanners actively send thousands of packets toward the target.

These packets include:

- TCP connection attempts
- HTTP requests
- Version detection probes
- Banner grabbing requests
- Vulnerability checks
- Enumeration requests

On a production network, these activities may:

- Trigger Intrusion Detection Systems (IDS)
- Trigger Intrusion Prevention Systems (IPS)
- Generate SIEM alerts
- Cause SOC investigations
- Violate organizational policies

Therefore, the instructor clearly stated that all demonstrations should be performed only in an isolated laboratory.

---

# Step 0 – Discover the Target

Before scanning, we must first identify the target IP address.

The instructor demonstrated:

```bash
sudo arp-scan --localnet
```

---

## Purpose

ARP Scan performs Layer-2 host discovery.

Instead of relying on ICMP (Ping), it sends ARP Requests across the local network.

Every active machine replies with its MAC address.

Example output:

```text
10.0.2.1
52:55:0A:00:02:01

10.0.2.3
08:00:27:00:5D:6A

10.0.2.15
08:00:27:95:B9:E6
```

---

## Interpretation

Each discovered host provides:

- IP Address
- MAC Address
- Vendor (through OUI lookup)

This helps identify:

- Gateway
- Victim
- Other virtual machines

---

# Why Not Guess the Target IP?

Many beginners assume:

```text
Target = 192.168.1.100
```

However, penetration testing should always begin with discovery.

Reasons:

- IP addresses may change.
- DHCP may assign different addresses.
- Multiple targets may exist.
- Unknown hosts may appear.

Therefore:

```text
Discover First
↓

Scan Later
```

---

# Practical 1 – Nmap Service Detection

Command:

```bash
nmap -sV <TARGET>
```

---

## Understanding the Command

```text
nmap

↓

Network Mapper
```

```text
-sV

↓

Service Version Detection
```

---

## What Happens Internally?

Nmap performs:

1.

Host discovery

↓

2.

Port scanning

↓

3.

Banner grabbing

↓

4.

Version detection

---

Example output:

```text
PORT     STATE SERVICE VERSION

21/tcp   open  ftp     vsftpd 2.3.4

22/tcp   open  ssh     OpenSSH 4.7

80/tcp   open  http    Apache httpd 2.2.8
```

---

## What Can We Learn?

Without exploiting anything, we already know:

- FTP Server
- SSH Server
- Apache Web Server

More importantly:

We know their versions.

Version information becomes extremely useful because:

```text
Version

↓

Known CVEs

↓

Potential Vulnerabilities
```

---

# Practical 2 – NSE Vulnerability Scripts

Command:

```bash
nmap -sV --script vuln <TARGET>
```

---

## What Changes?

Earlier:

```text
Identify Services
```

Now:

```text
Identify Services

↓

Run Vulnerability Scripts
```

---

## Internally

Nmap:

1.

Detects service version.

↓

2.

Chooses matching vulnerability scripts.

↓

3.

Runs Lua scripts.

↓

4.

Produces possible findings.

---

Example:

```text
Apache 2.2.8

↓

Possible CVEs
```

---

Important observation:

The result is:

```text
Possible Vulnerability
```

NOT

```text
Confirmed Vulnerability
```

This distinction is extremely important.

---

# Why Validation Is Required

Suppose:

```text
Apache 2.4.29
```

appears vulnerable according to public CVEs.

However,

the administrator may already have:

- Applied vendor patches.
- Backported security fixes.
- Disabled vulnerable modules.

The scanner cannot always determine this.

Therefore:

```text
Scanner

↓

Possible Vulnerability

↓

Human Validation

↓

Confirmed Finding
```

---

# Practical 3 – HTTP Enumeration

Command:

```bash
nmap -p80 --script http-enum <TARGET>
```

---

## Purpose

Instead of checking vulnerabilities,

this script attempts to enumerate common web content.

Examples:

```text
/admin

/login

/images

/uploads

/phpmyadmin

/test

/backup
```

---

## Why Is This Useful?

Suppose the scanner discovers:

```text
/admin
```

This immediately becomes an interesting target for:

- Authentication testing
- Access control testing
- IDOR testing

Similarly:

```text
/uploads
```

may indicate:

- File upload functionality
- Potential unrestricted upload vulnerabilities

---

# Practical 4 – Nikto Scan

Command:

```bash
nikto -h http://<TARGET>
```

---

## What Nikto Does

Nikto immediately starts sending HTTP requests.

It checks:

- Default files
- Dangerous files
- HTTP methods
- Missing headers
- Known server vulnerabilities
- Interesting directories

---

Example output:

```text
Server: Apache

Missing X-Frame-Options

OPTIONS Method Enabled

Directory Listing Enabled

Apache Outdated
```

---

# Understanding Nikto Findings

Suppose Nikto reports:

```text
OPTIONS Method Enabled
```

Is this automatically a vulnerability?

No.

We must ask:

- Is it required?
- Is it restricted?
- Can it be abused?

This demonstrates why scanners provide leads rather than conclusions.

---

# Practical 5 – Scanning DVWA

Command:

```bash
nikto -h http://<TARGET>/dvwa/
```

---

Instead of scanning the entire server,

Nikto now focuses on:

```text
DVWA
```

The scan may reveal:

- Missing headers
- Interesting files
- Directory listings
- Weak configurations

These become starting points for manual Burp Suite testing.

---

# Practical 6 – Saving Evidence

Command:

```bash
nikto -h http://<TARGET> \
-o nikto_report.html \
-Format htm
```

---

## Why Save Reports?

Professional penetration testing requires evidence.

Evidence includes:

- Terminal output
- Screenshots
- HTML reports
- Vulnerability descriptions

Nikto automatically generates an HTML report suitable for attachment to a penetration testing report.

---

# OpenVAS Demonstration

The instructor intentionally avoided running a complete OpenVAS scan live.

Reason:

OpenVAS is resource-intensive.

---

## Why?

During the first installation,

OpenVAS downloads:

- Vulnerability feeds
- CVE databases
- Configuration checks

This synchronization may take:

- Several minutes
- Sometimes hours

Therefore,

instead of waiting,

the instructor demonstrated a previously completed report.

---

# OpenVAS Workflow

Step 1

Create Target

↓

Step 2

Create Scan Task

↓

Step 3

Run Scan

↓

Step 4

Generate Report

↓

Step 5

Review Findings

---

# Reading an OpenVAS Report

Unlike Nikto,

OpenVAS prioritizes findings.

Typical severity levels:

```text
Critical

High

Medium

Low

Informational
```

Each finding contains:

- CVSS Score
- Description
- Impact
- References
- Remediation

---

# Why CVSS Matters

Two vulnerabilities may both exist.

Example:

Finding A

```text
CVSS 9.8
```

Finding B

```text
CVSS 3.4
```

Obviously,

Finding A should be addressed first.

OpenVAS automatically helps prioritize remediation.

---

# Why Automated Reports Are Not Final Reports

Scanner reports are:

```text
Evidence

+

Potential Findings
```

They are NOT:

```text
Final Penetration Test Reports
```

A professional pentester:

- Validates findings.
- Removes false positives.
- Adds screenshots.
- Explains business impact.
- Recommends remediation.

Only then is the report delivered.

---

# False Positives vs Confirmed Vulnerabilities

Example:

Scanner:

```text
Apache Vulnerable
```

↓

Manual Testing

↓

No exploit possible

↓

False Positive

---

Another case:

Scanner:

```text
Directory Listing Enabled
```

↓

Manual Verification

↓

Sensitive files accessible

↓

Confirmed Vulnerability

---

# Practical Lessons Learned

The practical demonstrated an important penetration testing mindset:

```text
Reconnaissance

↓

Automated Scanning

↓

Manual Validation

↓

Manual Exploitation

↓

Documentation
```

The scanner accelerates the reconnaissance process but never replaces manual testing.

---

# Key Practical Takeaways

- Always discover the target before scanning.
- Nmap identifies services and versions.
- NSE scripts identify possible vulnerabilities.
- Nikto focuses on web server misconfigurations.
- HTML reports become valuable evidence.
- OpenVAS provides enterprise-level vulnerability management.
- Scanner findings must always be validated.
- Professional penetration testing combines automation with human expertise.

  # Session 8 – Web Application Security: Vulnerability Scanning
## Part 4 – Manual Validation, Professional Workflow and Best Practices

---

# Why Automated Scanners Are Not Enough

Throughout this session, the instructor repeatedly emphasized one important principle:

> **A scanner only identifies potential vulnerabilities. A penetration tester confirms whether those vulnerabilities are actually exploitable.**

Many beginners believe that once a vulnerability scanner reports an issue, the system is definitely vulnerable.

This is incorrect.

Automated scanners perform pattern matching and version comparisons.

They do **not** understand:

- Business logic
- Application workflow
- User roles
- Context
- Custom security controls

Therefore, scanner output must always be treated as **potential findings**, not confirmed vulnerabilities.

---

# Why Human Validation is Necessary

Suppose a scanner reports:

```text
Apache 2.4.49

Possible Remote Code Execution
```

Does this mean the server is definitely vulnerable?

Not necessarily.

The administrator may have:

- Applied vendor patches
- Disabled vulnerable modules
- Added Web Application Firewall (WAF) protections
- Backported security fixes

Although the version number appears vulnerable, exploitation may fail.

This situation is known as a **False Positive**.

---

## Example of False Positive

Scanner Output:

```text
Apache 2.4.49

Potential CVE-2021-41773
```

Manual Validation:

- Test exploit
- Verify server response
- Check affected module
- Compare vendor patches

Result:

```text
Exploit Failed

↓

False Positive
```

---

## Example of True Positive

Scanner Output:

```text
Directory Listing Enabled
```

Manual Validation:

Navigate to:

```text
http://target/uploads/
```

Result:

```text
Entire directory is publicly accessible.
```

Sensitive files become downloadable.

This confirms:

```text
True Positive
```

---

# Scanner Findings vs Confirmed Vulnerabilities

| Scanner Output | Reality |
|---------------|----------|
| Potential Vulnerability | Requires verification |
| Software Version | Must be confirmed |
| Missing Header | Verify impact |
| Weak Configuration | Validate exploitability |
| CVE Match | Attempt controlled testing |

---

# Relationship Between Vulnerability Scanners and Burp Suite

Students often ask:

> "If Nikto and OpenVAS already find vulnerabilities, why do we still need Burp Suite?"

The answer lies in understanding their different purposes.

---

## Vulnerability Scanner

Purpose:

Automatically identify **known weaknesses**.

Examples:

- Missing headers
- Outdated software
- Open ports
- Weak TLS
- Default files

Workflow:

```text
Target

↓

Automated Requests

↓

Pattern Matching

↓

Possible Findings
```

---

## Burp Suite

Purpose:

Manual testing of application logic.

Burp allows the tester to:

- Modify HTTP requests
- Change parameters
- Replay requests
- Test authentication
- Test authorization
- Manipulate cookies
- Intercept traffic

Workflow:

```text
Browser

↓

Burp Proxy

↓

Modify Request

↓

Server

↓

Analyze Response
```

---

# Nikto vs Burp Suite

| Nikto | Burp Suite |
|--------|------------|
| Automated | Manual |
| Fast | Detailed |
| Checks known issues | Finds logic flaws |
| Limited interaction | Complete request manipulation |
| Generates reports | Assists exploitation |

---

# OpenVAS vs Burp Suite

OpenVAS focuses on:

```text
Infrastructure
```

Burp Suite focuses on:

```text
Web Applications
```

OpenVAS asks:

```text
Is the server vulnerable?
```

Burp asks:

```text
Can I manipulate the application?
```

---

# Where OWASP ZAP Fits

The instructor previously introduced OWASP ZAP.

ZAP is similar to Burp Suite.

It provides:

- Proxy
- Spider
- Passive Scan
- Active Scan
- Fuzzer

Unlike Nikto,

ZAP understands application workflows much better.

---

# Complete Penetration Testing Workflow

The PPT summarizes vulnerability scanning as only one step of penetration testing.

Let's expand the complete workflow.

---

## Step 1 – Reconnaissance

Collect information.

Examples:

- Domains
- IPs
- Employees
- Technologies

Tools:

- Google Dorks
- WHOIS
- Shodan
- theHarvester

---

## Step 2 – Host Discovery

Identify live systems.

Tools:

- ping
- arp-scan
- Nmap

Output:

```text
Live Hosts
```

---

## Step 3 – Port Scanning

Discover:

- Open Ports
- Services
- Versions

Command:

```bash
nmap -sV TARGET
```

---

## Step 4 – Vulnerability Scanning

Identify:

- Weak configurations
- Known CVEs
- Missing security controls

Tools:

- Nmap NSE
- Nikto
- OpenVAS

---

## Step 5 – Manual Validation

Verify:

- Is the issue real?
- Can it be exploited?
- What is the impact?

Tools:

- Burp Suite
- Browser
- curl
- Manual testing

---

## Step 6 – Exploitation

Attempt controlled exploitation.

Examples:

- SQL Injection
- XSS
- File Inclusion
- Authentication Bypass

Purpose:

Demonstrate actual business impact.

---

## Step 7 – Post Exploitation

If exploitation succeeds:

Determine:

- Privilege level
- Accessible data
- Internal movement
- Persistence (if within scope)

---

## Step 8 – Reporting

Document:

- Vulnerability
- Evidence
- Risk
- Impact
- Recommendation

---

# Manual Testing Examples

A scanner may report:

```text
Login Page Found
```

Manual testing determines:

- SQL Injection
- Username Enumeration
- Brute Force Protection
- Password Policy
- MFA Implementation

---

Scanner reports:

```text
Upload Page
```

Manual testing determines:

- File Type Validation
- Extension Filtering
- Content-Type Validation
- Remote Code Execution

---

Scanner reports:

```text
Directory Listing Enabled
```

Manual testing determines:

- Sensitive Files
- Configuration Leakage
- Backup Files
- Source Code Exposure

---

# Ethical Considerations

The instructor emphasized that these tools are designed for:

- Security Audits
- Penetration Testing
- Authorized Assessments

Never use them against:

- Public websites without permission
- Production systems without authorization
- Third-party infrastructure

Unauthorized scanning may:

- Trigger security alerts
- Disrupt services
- Violate organizational policies
- Lead to legal consequences

Always obtain written authorization before conducting scans.

---

# Advantages of Automated Vulnerability Scanning

- Rapid assessment
- Broad coverage
- Repeatable process
- Consistent results
- Large vulnerability databases
- Supports compliance audits
- Generates evidence for reports

---

# Limitations of Automated Scanning

- Cannot detect business logic flaws
- Cannot understand application context
- False positives
- False negatives
- No understanding of user workflows
- Cannot replace human reasoning

---

# Best Practices

- Perform reconnaissance before scanning.
- Scan only authorized targets.
- Keep vulnerability databases updated.
- Validate every critical finding manually.
- Do not rely on CVE matches alone.
- Combine multiple tools for better coverage.
- Maintain detailed evidence during testing.
- Re-scan after remediation to verify fixes.

---

# Interview Questions

## 1. What is vulnerability scanning?

An automated process that identifies known vulnerabilities by comparing system configurations, software versions, and services against vulnerability databases.

---

## 2. Why can't vulnerability scanners replace penetration testers?

Because scanners detect potential vulnerabilities, while penetration testers validate findings, assess business impact, and identify complex issues such as business logic flaws and authorization problems.

---

## 3. What is a false positive?

A finding reported by a scanner that does not actually represent a real vulnerability after manual verification.

---

## 4. Differentiate Nmap NSE, Nikto and OpenVAS.

| Tool | Primary Purpose |
|------|------------------|
| Nmap NSE | Network enumeration and lightweight vulnerability checks |
| Nikto | Web server vulnerability scanning |
| OpenVAS | Enterprise vulnerability management and infrastructure assessment |

---

## 5. Why should findings always be validated manually?

Because automated tools may produce false positives, miss contextual security controls, or incorrectly identify software versions.

---

# Session Summary

This session introduced **automated vulnerability scanning** as a critical phase within the penetration testing lifecycle. Students learned that scanners such as **Nmap NSE**, **Nikto**, and **OpenVAS** rapidly identify potential weaknesses across networks, web servers, and infrastructure. However, the session also stressed that automated findings are only the beginning. Every reported issue must be manually validated, tested for exploitability, and documented before being included in a professional penetration testing report.

The key takeaway from this session is:

```text
Reconnaissance
        ↓
Scanning
        ↓
Validation
        ↓
Exploitation
        ↓
Reporting
```

Automation accelerates discovery, but professional penetration testing always depends on human analysis, verification, and sound judgment.

