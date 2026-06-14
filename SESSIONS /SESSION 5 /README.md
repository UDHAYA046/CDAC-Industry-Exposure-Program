# Session 5 – Vulnerability Assessment, Reconnaissance & Social Engineering

**Date:** 13 June 2026
**Course:** CDAC Industry Exposure Program – Cybersecurity
**Session:** 5
**Duration:** 2:00 PM – 5:00 PM

---

# Overview

This session focused on the concepts of vulnerabilities, vulnerability scoring systems, reconnaissance, information gathering, enumeration, OSINT, social engineering, phishing attacks, and practical demonstrations using cybersecurity tools such as Nmap, WHOIS, and Gobuster.

One of the most important ideas discussed during the session was:

> Most successful cyber attacks begin with information gathering rather than exploitation.

Attackers typically spend significant time learning about their target before attempting to compromise systems. Understanding technologies, users, exposed services, domains, and organizational structures often makes attacks easier and more effective.

---

# Authorization and Ethical Considerations

Before performing any reconnaissance, scanning, enumeration, or vulnerability assessment activity, proper authorization must be obtained.

Important rule:

```text
Never perform scanning or reconnaissance against systems
you do not own or have explicit written permission to test.
```

Cybersecurity professionals operate under legal and ethical boundaries.

Activities such as:

* Port scanning
* Vulnerability scanning
* Enumeration
* Penetration testing

must always be authorized.

---

# Fundamental Security Concepts

Understanding cybersecurity begins with understanding five core concepts:

1. Asset
2. Vulnerability
3. Threat
4. Exploit
5. Risk

---

# Asset

An asset is anything valuable that an organization wants to protect.

Assets may be:

## Physical Assets

* Servers
* Laptops
* Networking devices
* Storage systems

## Digital Assets

* Databases
* Customer information
* Source code
* Credentials
* Cloud resources

## Business Assets

* Brand reputation
* Intellectual property
* Financial records

### Example

```text
Customer database containing credit card information
```

is a critical asset.

---

# Vulnerability

A vulnerability is a weakness that can be exploited.

Vulnerabilities may exist in:

* Software
* Hardware
* Configurations
* Processes
* Human behavior

### Examples

```text
Weak password
Open S3 bucket
Outdated software
Misconfigured firewall
```

A vulnerability does not cause damage by itself.

It simply creates an opportunity for an attacker.

---

# Threat

A threat is anything capable of exploiting a vulnerability.

Examples include:

* Hackers
* Malware
* Ransomware
* Insider threats
* Nation-state attackers

### Example

Suppose:

```text
Front door left unlocked
```

This is a vulnerability.

A thief nearby becomes:

```text
Threat
```

because they can exploit that weakness.

---

# Exploit

An exploit is the method used to take advantage of a vulnerability.

Examples:

```text
SQL Injection Payload
Remote Code Execution Exploit
Buffer Overflow Exploit
```

An exploit bridges the gap between:

```text
Vulnerability
        ↓
Compromise
```

---

# Payload

A payload is the code executed after successful exploitation.

Examples:

```text
Reverse Shell
Keylogger
Backdoor
Ransomware
Trojan
```

The payload performs the attacker's intended action.

---

# Risk

Risk is determined by:

```text
Risk = Likelihood × Impact
```

Questions asked:

* How likely is exploitation?
* What would happen if exploited?

High likelihood + High impact = High risk

---

# House Analogy

The instructor used a useful analogy:

## House

Asset:

```text
House and valuables
```

Vulnerability:

```text
Door left open
```

Threat:

```text
Thief nearby
```

Exploit:

```text
Lock picking tools
```

Payload:

```text
Stealing valuables
```

Risk:

```text
Probability of theft and resulting damage
```

This analogy helps distinguish between commonly confused terms.

---

# Attack Surface

Attack Surface refers to all possible entry points available to an attacker.

Every exposed service increases the attack surface.

Examples:

* Websites
* Login pages
* APIs
* Mobile applications
* Open ports
* Cloud services
* VPN portals

---

## Why Attack Surface Matters

A larger attack surface means:

```text
More opportunities
More weaknesses
More potential attack paths
```

Organizations attempt to reduce attack surface by:

* Closing unused ports
* Removing unnecessary services
* Applying least privilege
* Hardening systems

---

# Vulnerability Identification

Once vulnerabilities are discovered, they are documented and tracked.

Three major systems are used:

1. CVE
2. NVD
3. CVSS

---

# CVE (Common Vulnerabilities and Exposures)

CVE provides a unique identifier for publicly known vulnerabilities.

Format:

```text
CVE-YYYY-NNNNN
```

Example:

```text
CVE-2021-44228
```

(Log4Shell)

---

## Structure of CVE

Example:

```text
CVE-2021-44228
```

### CVE

Indicates vulnerability database identifier.

### 2021

Year assigned.

### 44228

Unique vulnerability number.

---

## Purpose of CVE

Without CVEs:

Different vendors may use different names.

With CVEs:

Everyone references the same vulnerability.

Example:

```text
CVE-2021-44228
```

immediately identifies Log4Shell globally.

---

# NVD (National Vulnerability Database)

NVD is maintained by NIST.

Website:

```text
https://nvd.nist.gov
```

NVD builds upon CVEs.

---

## CVE vs NVD

### CVE

Provides:

```text
Identifier only
```

Example:

```text
CVE-2021-44228
```

---

### NVD

Provides:

```text
Detailed description
Affected versions
Severity information
References
Mitigation information
```

Think:

```text
CVE = Name
NVD = Full Report
```

---

# CVSS (Common Vulnerability Scoring System)

CVSS assigns numerical severity scores.

Range:

```text
0.0 – 10.0
```

---

## Severity Ratings

| Score    | Severity |
| -------- | -------- |
| 0.0      | None     |
| 0.1–3.9  | Low      |
| 4.0–6.9  | Medium   |
| 7.0–8.9  | High     |
| 9.0–10.0 | Critical |

---

# Why CVSS Exists

Two vulnerabilities may both be labeled:

```text
High
```

But one may be significantly worse.

Example:

| Vulnerability             | Score |
| ------------------------- | ----- |
| Log4Shell                 | 10.0  |
| Another High Severity Bug | 7.8   |

Both are high.

However:

```text
10.0 > 7.8
```

Therefore Log4Shell is more dangerous.

---

# CVSS Metrics

The instructor explained five major factors influencing CVSS scoring.

---

## 1. Attack Vector

Can exploitation occur:

```text
Over the network?
```

or

```text
Requires physical access?
```

Network attacks receive higher scores.

---

## 2. Attack Complexity

How difficult is exploitation?

Questions:

```text
Special conditions needed?
Advanced skills required?
```

Simpler attacks receive higher scores.

---

## 3. Privileges Required

Must attacker authenticate first?

If:

```text
No authentication needed
```

severity increases.

---

## 4. User Interaction

Must victim do something?

Examples:

```text
Click a link
Open a file
Visit a website
```

If user interaction is required:

Severity decreases.

If not required:

Severity increases.

---

## 5. CIA Triad Impact

### Confidentiality

Can data be stolen?

### Integrity

Can data be modified?

### Availability

Can services be disrupted?

The greater the impact on CIA:

The higher the CVSS score.

---

# Log4Shell Example

Log4Shell received:

```text
CVSS 10.0
```

because:

* Remote exploitation
* No authentication
* Minimal user interaction
* Full compromise potential

This made it one of the most severe vulnerabilities ever disclosed.

---

# OWASP

OWASP stands for:

```text
Open Worldwide Application Security Project
```

OWASP is a nonprofit organization focused on improving software security.

It provides:

* Security guidelines
* Tools
* Research
* Best practices

---

# Why OWASP Matters

OWASP Top 10 identifies the most critical web application security risks.

It serves as a reference for:

* Developers
* Security Engineers
* Auditors
* Penetration Testers

---

# OWASP Top 10 (2021)

## A01 – Broken Access Control

Users gain access to resources they should not access.

Example:

```text
user=101
```

changed to:

```text
user=102
```

reveals another user's information.

---

## A02 – Cryptographic Failures

Sensitive data not properly protected.

Examples:

* Weak encryption
* Plaintext passwords
* HTTP instead of HTTPS

---

## A03 – Injection

User input becomes executable commands.

Examples:

* SQL Injection
* Command Injection
* LDAP Injection

Example:

```sql
' OR '1'='1
```

---

## A04 – Insecure Design

Security flaws introduced during design.

Examples:

* Missing rate limiting
* Weak workflows
* Poor authentication design

---

## A05 – Security Misconfiguration

Improper security settings.

Examples:

* Default credentials
* Public admin panels
* Open cloud storage

---

## A06 – Vulnerable Components

Using outdated software.

Examples:

* Old Apache versions
* Unpatched libraries

---

## A07 – Identification and Authentication Failures

Weak authentication mechanisms.

Examples:

* Weak passwords
* Missing MFA
* Session management flaws

---

## A08 – Software and Data Integrity Failures

Trusting unverified updates or code.

Examples:

* Supply chain attacks
* Malicious package updates

---

## A09 – Security Logging and Monitoring Failures

Organizations fail to detect attacks.

Examples:

* Missing logs
* No monitoring
* Delayed incident response

---

## A10 – Server Side Request Forgery (SSRF)

Server is tricked into making requests on behalf of an attacker.

Example:

```text
User supplies:
http://internal-server/admin
```

Server fetches it.

Attacker gains indirect access.

---

# SSRF Explained

Server Side Request Forgery occurs when:

1. User supplies URL.
2. Server trusts URL.
3. Server fetches resource.
4. Internal systems become accessible.
5. Attacker gains information.

Common targets:

* Internal APIs
* Cloud metadata services
* Administrative interfaces

---

# Key Takeaways

* Vulnerabilities create opportunities.
* Threats exploit vulnerabilities.
* Exploits leverage vulnerabilities.
* Payloads execute attacker objectives.
* CVE identifies vulnerabilities.
* NVD documents vulnerabilities.
* CVSS measures severity.
* OWASP Top 10 highlights critical application security risks.
* Reducing attack surface reduces risk.

---


# Reconnaissance, Information Gathering & Enumeration

---

# Reconnaissance – The Foundation of Every Cyber Attack

Reconnaissance (Recon) is the process of gathering information about a target before attempting exploitation.

In military operations, armies do not attack blindly. They first study:

* Enemy locations
* Defenses
* Terrain
* Resources

Similarly, attackers first study:

* Domains
* Servers
* Technologies
* Employees
* Cloud infrastructure
* Email addresses
* Network exposure

before launching an attack.

This phase often determines whether an attack succeeds or fails.

---

# Why Reconnaissance Matters

The instructor emphasized an important reality:

> The better the reconnaissance, the less hacking is required.

Consider two scenarios.

## Without Reconnaissance

Attacker sends:

```text
Dear User,
Click Here.
```

Most users ignore it.

---

## With Reconnaissance

Attacker learns:

* Employee name
* Department
* Technologies used
* Current projects

Then sends:

```text
Hello Rahul,

Please review the updated Kubernetes migration document before tomorrow's meeting.

Regards,
Infrastructure Team
```

This looks legitimate.

The attack becomes much more effective.

---

# Reconnaissance Goals

Recon attempts to answer:

```text
Who is the target?
What technologies do they use?
Who works there?
What services are exposed?
What are the potential attack paths?
```

---

# Cyber Kill Chain

The Cyber Kill Chain describes the stages of a cyber attack.

---

## Stage 1 – Reconnaissance

Gather information.

Examples:

* WHOIS
* Shodan
* LinkedIn
* DNS Enumeration

---

## Stage 2 – Weaponization

Create attack payload.

Examples:

* Malware
* Ransomware
* Malicious documents

---

## Stage 3 – Delivery

Deliver payload.

Examples:

* Email
* USB
* Website

---

## Stage 4 – Exploitation

Trigger vulnerability.

Examples:

* Opening infected file
* Visiting malicious website

---

## Stage 5 – Installation

Install malware.

Examples:

* Backdoor
* Trojan
* RAT

---

## Stage 6 – Command and Control (C2)

Compromised machine communicates with attacker.

Purpose:

* Execute commands
* Upload malware
* Download stolen data

---

## Stage 7 – Actions on Objectives

Final objective.

Examples:

* Data theft
* Espionage
* Ransomware
* Destruction

---

# Information Gathering

Information gathering is the process of collecting intelligence about a target.

Information may include:

* Domain names
* Email addresses
* Technologies
* Employee information
* Infrastructure

Information gathering can be:

1. Passive
2. Active

---

# Passive Reconnaissance

Passive reconnaissance gathers information without directly interacting with the target.

No packets are sent.

No logs are generated.

Target remains unaware.

---

# Characteristics

Advantages:

```text
Stealthy
Hard to detect
Low risk
```

Disadvantages:

```text
Limited information
May contain outdated information
```

---

# Passive Recon Sources

## Search Engines

Examples:

```text
Google
Bing
DuckDuckGo
```

---

## Social Media

Examples:

```text
LinkedIn
Twitter/X
Facebook
Instagram
```

---

## WHOIS

Provides:

```text
Domain information
Registrar
Creation date
Name servers
```

---

## Certificate Transparency

Provides:

```text
SSL certificate information
Subdomains
```

---

## GitHub

May expose:

```text
API Keys
Passwords
Cloud credentials
Source code
```

---

## Job Postings

Reveal:

```text
AWS
Azure
Docker
Kubernetes
Cisco
Splunk
```

technology stacks.

---

# Active Reconnaissance

Active reconnaissance directly interacts with the target.

The target can detect activity.

Logs may be generated.

Alerts may trigger.

---

# Characteristics

Advantages:

```text
Accurate
Real-time information
```

Disadvantages:

```text
Detectable
Potentially noisy
```

---

# Examples

```text
Ping Sweeps
Port Scanning
Banner Grabbing
DNS Enumeration
SMTP Enumeration
SNMP Enumeration
Vulnerability Scanning
```

---

# Passive vs Active Recon

| Passive Recon      | Active Recon       |
| ------------------ | ------------------ |
| No interaction     | Direct interaction |
| Hard to detect     | Easier to detect   |
| Public information | Target interaction |
| Lower risk         | Higher risk        |
| Less accurate      | More accurate      |

---

# OSINT (Open Source Intelligence)

OSINT refers to intelligence gathered from publicly available sources.

The key concept:

```text
No hacking required.
```

Only public information is used.

---

# Why OSINT Matters

OSINT can reveal:

```text
Employees
Technologies
Email addresses
Subdomains
Cloud providers
Infrastructure
```

without touching the target.

---

# Common OSINT Sources

## LinkedIn

May reveal:

```text
Employee names
Departments
Technologies
Managers
```

Example:

```text
Senior AWS Engineer
```

reveals AWS usage.

---

## Company Website

May reveal:

```text
Email formats
Locations
Partners
Phone numbers
```

---

## Job Postings

Example:

```text
Must know:
AWS
Cisco ASA
Splunk
Kubernetes
```

reveals infrastructure.

---

## GitHub

Potential exposure:

```text
Secrets
API keys
Source code
Configurations
```

---

# Scanning vs Enumeration

This is one of the most important concepts from the session.

Students often confuse the two.

---

# Scanning

Scanning answers:

```text
What exists?
```

Purpose:

* Discover hosts
* Discover ports
* Discover services

Example:

```bash
nmap target.com
```

Output:

```text
22 open
80 open
443 open
```

We know doors exist.

We do not know what is behind them.

---

# Building Analogy

Scanning is like walking around a building and identifying:

```text
Front Door
Back Door
Windows
Emergency Exit
```

without entering.

---

# Enumeration

Enumeration answers:

```text
What exactly is running?
```

Purpose:

* Service versions
* Usernames
* Shares
* Configurations
* DNS records

Example:

```bash
nmap -sV target.com
```

Output:

```text
Apache 2.4.41
OpenSSH 8.2
```

Now we know what is behind the door.

---

# Why Enumeration Matters

Enumeration transforms discovery into intelligence.

Example:

```text
Apache 2.4.41
```

attacker searches:

```text
Apache 2.4.41 CVE
```

and finds vulnerabilities.

---

# Relationship

```text
Reconnaissance
      ↓
Scanning
      ↓
Enumeration
      ↓
Vulnerability Analysis
      ↓
Exploitation
```

---

# Banner Grabbing

Many services reveal information immediately after connection.

Example banner:

```text
Apache/2.4.41
```

This reveals:

```text
Software
Version
Potential vulnerabilities
```

---

# Why Attackers Love Banner Grabbing

Because it allows:

```text
Version identification
Vulnerability research
Technology fingerprinting
```

without exploitation.

---

# Defense

Hide unnecessary version information.

Instead of:

```text
Apache/2.4.41
```

show:

```text
Apache
```

---

# DNS Enumeration

DNS is the Internet's phonebook.

Converts:

```text
google.com
```

to:

```text
IP Address
```

---

# DNS Records

## A Record

Maps:

```text
Domain → IPv4
```

---

## AAAA Record

Maps:

```text
Domain → IPv6
```

---

## MX Record

Mail server information.

Example:

```text
mail.google.com
```

---

## NS Record

Authoritative DNS servers.

---

## TXT Record

Contains:

```text
SPF
DKIM
DMARC
Verification records
```

---

## CNAME

Alias record.

---

## PTR

Reverse lookup:

```text
IP → Domain
```

---

## SOA

Start of Authority.

Administrative zone information.

---

# Why DNS Enumeration Matters

May reveal:

```text
vpn.company.com
mail.company.com
api.company.com
dev.company.com
```

These become future targets.

---

# SMTP Enumeration

SMTP:

```text
Simple Mail Transfer Protocol
```

Uses:

```text
Port 25
```

---

# Purpose

Determine:

```text
Valid users
Mail infrastructure
```

---

# Common Commands

Older mail servers supported:

```text
VRFY
EXPN
RCPT TO
```

---

# Risk

If attacker discovers:

```text
admin@company.com
finance@company.com
```

then:

```text
Password attacks
Phishing
BEC attacks
```

become easier.

---

# SNMP Enumeration

SNMP:

```text
Simple Network Management Protocol
```

Uses:

```text
UDP 161
```

---

# Devices Using SNMP

```text
Routers
Switches
Printers
Firewalls
Servers
```

---

# Information Exposed

Potentially reveals:

```text
Hostname
Operating System
Installed Software
Interfaces
Processes
Accounts
Network Information
```

---

# Community Strings

Default values:

```text
public
private
```

These act like passwords.

If unchanged:

Attackers may gain access to device information.

---

# SNMP Versions

## SNMPv1

No encryption.

---

## SNMPv2c

Improved performance.

Still no encryption.

---

## SNMPv3

Provides:

```text
Authentication
Encryption
Access Control
```

Recommended version.

---

# Why SNMP Is Dangerous

Misconfigured SNMP can reveal an entire network layout without exploitation.

Attackers can learn:

```text
Network topology
Devices
Software versions
Configurations
```

which greatly assists later attacks.

---

# Key Takeaways

* Reconnaissance is the foundation of cyber attacks.
* Passive reconnaissance uses public information.
* Active reconnaissance directly interacts with targets.
* OSINT provides intelligence without hacking.
* Scanning identifies targets.
* Enumeration extracts detailed information.
* Banner grabbing reveals software details.
* DNS, SMTP, and SNMP can leak valuable information.
* Enumeration often provides the information required for exploitation.

---

#  OSINT, WHOIS, Shodan & Google Dorking

---

# Open Source Intelligence (OSINT)

## Introduction

OSINT (Open Source Intelligence) refers to the collection, analysis, and correlation of information from publicly available sources.

Unlike traditional hacking techniques, OSINT does not require exploitation of systems.

The information already exists in public domains.

The challenge lies in:

* Finding it
* Correlating it
* Understanding its significance
* Converting information into intelligence

---

# Why OSINT Matters

Before launching an attack, attackers seek answers to questions such as:

```text
Who is the target?
What technologies do they use?
Who works there?
What cloud providers are used?
Which services are exposed?
What email format does the company use?
```

OSINT often provides these answers without touching the target's infrastructure.

---

# Advantages of OSINT

## For Attackers

Used for:

* Reconnaissance
* Social Engineering
* Phishing
* Infrastructure Mapping
* Technology Identification

---

## For Defenders

Used for:

* Threat Intelligence
* Exposure Assessment
* Asset Discovery
* Brand Monitoring
* Data Leak Detection

---

# OSINT Framework

Website:

```text
https://osintframework.com
```

OSINT Framework is one of the most widely used OSINT resources.

It organizes hundreds of intelligence gathering tools into categories such as:

* Domains
* Usernames
* Social Media
* Images
* Phone Numbers
* Email Addresses
* Geolocation
* Cryptocurrency

Think of it as:

> A directory of OSINT tools.

---

# WHOIS

## What is WHOIS?

WHOIS is a public database containing domain registration information.

It acts similarly to a vehicle registration database but for internet domains.

---

# Purpose of WHOIS

WHOIS allows anyone to obtain information regarding:

* Domain Ownership
* Registration Date
* Expiration Date
* Registrar Information
* Name Servers
* Domain Status

---

# Practical Demonstration

Command:

```bash
whois google.com
```

---

# Understanding WHOIS Output

## Domain Name

Example:

```text
Domain Name: GOOGLE.COM
```

The domain being queried.

---

## Registry Domain ID

Unique identifier assigned by the registry.

Similar to:

```text
Aadhaar Number for a Domain
```

---

## Registrar

Example:

```text
MarkMonitor Inc.
```

The company through which the domain was registered.

Common Registrars:

* GoDaddy
* Namecheap
* MarkMonitor
* Google Domains

---

## Creation Date

Example:

```text
1997-09-15
```

The date when the domain was first registered.

---

### Why Important?

Fraudulent domains often have recent registration dates.

Example:

```text
microsoft-security-support.com
```

Created:

```text
Yesterday
```

This would be highly suspicious.

---

## Updated Date

The last time significant modifications were made to registration information.

---

## Expiry Date

Example:

```text
2028-09-14
```

Indicates when the domain registration expires.

---

## Name Servers

Example:

```text
ns1.google.com
ns2.google.com
ns3.google.com
ns4.google.com
```

Responsible for translating:

```text
google.com
```

into:

```text
IP Address
```

---

## Domain Status

Common values:

```text
clientDeleteProhibited
clientTransferProhibited
clientUpdateProhibited
```

These protect domains from:

* Deletion
* Unauthorized transfer
* Unauthorized modification

---

# Why Attackers Use WHOIS

WHOIS provides valuable intelligence such as:

```text
Domain Age
Registrar
DNS Infrastructure
Ownership Information
```

This helps attackers understand the target's infrastructure.

---

# Certificate Transparency Logs

## What are CT Logs?

Certificate Transparency (CT) logs publicly record every SSL/TLS certificate issued on the internet.

Purpose:

```text
Transparency
Accountability
Fraud Detection
```

---

# Popular Resource

Website:

```text
https://crt.sh
```

---

# Why CT Logs Matter

Suppose an organization owns:

```text
company.com
```

Certificates may reveal:

```text
vpn.company.com
mail.company.com
dev.company.com
api.company.com
staging.company.com
```

Even if these subdomains are not publicly advertised.

---

# Example Search

Search:

```text
%.google.com
```

on crt.sh

Potentially reveals:

```text
mail.google.com
docs.google.com
support.google.com
```

and many others.

---

# Why Attackers Love CT Logs

They reveal:

* Hidden Infrastructure
* Development Environments
* VPN Gateways
* Administrative Systems

without touching the target.

---

# Job Posting Intelligence

Most people see job advertisements as recruitment information.

Attackers see them as infrastructure documentation.

---

# Example Job Advertisement

```text
Required Skills:

AWS
Kubernetes
Cisco ASA
Splunk
```

---

# Information Revealed

The organization likely uses:

```text
AWS Cloud
Containerized Infrastructure
Cisco Firewalls
Splunk SIEM
```

---

# Why This Matters

Attackers can focus their research on:

```text
AWS Misconfigurations
Kubernetes Weaknesses
Cisco Vulnerabilities
```

instead of guessing.

---

# Social Media Intelligence

Social media is one of the richest OSINT sources available.

---

# Information Commonly Revealed

Employees frequently disclose:

```text
Projects
Job Roles
Technologies
Locations
Managers
Departments
```

often unintentionally.

---

# LinkedIn Intelligence

Example Profile:

```text
Cloud Security Engineer
AWS Specialist
Kubernetes Administrator
```

Reveals:

```text
Cloud Platform
Container Platform
Security Focus
```

---

# Why LinkedIn Matters

LinkedIn may reveal:

```text
Employee Names
Reporting Structure
Departments
Technology Stack
```

This information is highly useful for spear phishing attacks.

---

# Example

Attacker learns:

```text
Rahul Sharma
Cloud Engineer
Works on AWS
```

Phishing email becomes:

```text
AWS IAM Policy Review Required
```

instead of:

```text
Click Here
```

The attack becomes much more believable.

---

# Wayback Machine

## What is the Wayback Machine?

Website:

```text
https://archive.org
```

Stores historical snapshots of websites.

---

# Why It Matters

Organizations often remove pages.

However, archived versions may still contain:

```text
Admin Panels
Backup Directories
Old APIs
Internal Documentation
```

---

# Example

Current Website:

```text
company.com
```

appears secure.

Archived Version reveals:

```text
/admin
/backup
/dev
/test
```

These paths may still exist.

---

# Intelligence Obtained

The Wayback Machine can reveal:

* Historical Website Structure
* Old Technologies
* Forgotten Endpoints
* Previous Configurations

---

# Shodan

## What is Shodan?

Shodan is often called:

```text
Google for Internet Connected Devices
```

---

# Difference Between Google and Shodan

Google indexes:

```text
Web Pages
```

Shodan indexes:

```text
Servers
Routers
Firewalls
Cameras
IoT Devices
Printers
```

---

# Information Revealed

Shodan may expose:

```text
IP Address
Open Ports
Service Versions
Operating Systems
Location
Organization
```

---

# Example Searches

```text
Apache
Cisco ASA
Webcam
RDP
```

---

# Why Attackers Use Shodan

Organizations sometimes accidentally expose:

```text
Databases
Remote Desktop Services
Cameras
Management Interfaces
```

to the public internet.

Shodan finds these exposures automatically.

---

# Google Dorking

## What is Google Dorking?

Google Dorking uses advanced search operators to discover publicly accessible information indexed by Google.

The instructor described it as:

> OSINT using a search bar.

---

# Why It Works

Google indexes:

* Web Pages
* PDFs
* Word Documents
* Excel Files
* PowerPoint Files
* Directory Listings

Sometimes organizations accidentally expose sensitive information.

---

# site:

Example:

```text
site:amrita.edu
```

Searches only within:

```text
amrita.edu
```

---

# filetype:

Example:

```text
filetype:pdf site:amrita.edu
```

Searches only PDF documents.

---

# Common File Types

```text
pdf
doc
docx
ppt
pptx
xlsx
csv
```

---

# intitle:"index of"

Searches for open directory listings.

Example:

```text
intitle:"index of"
```

May reveal:

```text
/backup
/uploads
/documents
```

---

# Why Dangerous?

Directory listings may expose:

```text
Database Backups
ZIP Archives
Configuration Files
Logs
```

---

# inurl:admin

Searches URLs containing:

```text
admin
```

Example:

```text
inurl:admin
```

Potential results:

```text
/admin
/admin-login
/adminpanel
```

---

# site:example.com -www

Used to identify subdomains.

Example:

```text
site:google.com -www
```

May reveal:

```text
docs.google.com
mail.google.com
support.google.com
```

---

# Google Hacking Database (GHDB)

Maintained by OWASP.

Contains:

* Known Dorks
* Security Search Queries
* OSINT Search Patterns

Used by:

* Security Researchers
* Penetration Testers
* Bug Bounty Hunters

---

# Security Through Obscurity

Important Lesson:

```text
Never assume nobody knows the URL.
```

Example:

```text
company.com/secret_admin_12345
```

is not secure simply because it is hard to guess.

Google may index it.

Attackers may discover it.

Proper security requires:

* Authentication
* Authorization
* Access Controls

not secrecy alone.

---

# Complete Passive Recon Workflow

```text
WHOIS
    ↓
Certificate Transparency
    ↓
Job Postings
    ↓
LinkedIn
    ↓
Social Media
    ↓
Wayback Machine
    ↓
Shodan
    ↓
Google Dorking
    ↓
Target Profile Creation
```

---

# Key Takeaways

* OSINT collects intelligence from public sources.
* WHOIS reveals domain registration information.
* Certificate Transparency logs reveal subdomains.
* Job advertisements reveal technologies.
* Social media reveals employees and infrastructure.
* Wayback Machine reveals historical website information.
* Shodan discovers internet-exposed systems.
* Google Dorking finds indexed sensitive information.
* OSINT enables highly targeted reconnaissance and phishing campaigns.

---

# Social Engineering & Human-Centric Attacks

---

# Social Engineering

## Introduction

Social Engineering is the art of manipulating people into performing actions or revealing confidential information that benefits an attacker.

Unlike traditional cyberattacks that target software vulnerabilities, social engineering targets:

```text
Human Psychology
Human Behavior
Human Emotions
Human Trust
```

The attacker is not hacking the computer.

The attacker is hacking the person.

---

# Why Social Engineering Works

Modern organizations invest heavily in:

* Firewalls
* Antivirus Solutions
* Intrusion Detection Systems
* SIEM Platforms
* Endpoint Protection

However, the strongest security technology can still be bypassed if a user voluntarily provides access.

The instructor emphasized:

> Humans are often the easiest target.

---

# Relationship Between OSINT and Social Engineering

Reconnaissance makes social engineering believable.

Without reconnaissance:

```text
Dear User,
Click Here.
```

Most people ignore it.

---

With reconnaissance:

```text
Hi Rahul,

The AWS IAM review document discussed during yesterday's cloud migration meeting requires your approval.

Regards,
Infrastructure Team
```

This appears legitimate.

Why?

Because the attacker already knows:

* Employee name
* Department
* Current project
* Technologies used

OSINT makes deception more convincing.

---

# Objectives of Social Engineering

Attackers commonly attempt to obtain:

```text
Credentials
Banking Information
OTP Codes
Internal Documents
System Access
Sensitive Data
```

---

# Why Humans Become Targets

Humans naturally possess traits such as:

```text
Trust
Curiosity
Fear
Urgency
Helpfulness
Greed
```

Attackers exploit these traits.

---

# Principles of Influence

Social engineering attacks are often built upon psychological principles.

The session discussed six major principles.

---

# 1. Authority

## Definition

People tend to obey individuals who appear to have authority.

Examples:

```text
CEO
Manager
Government Official
Police Officer
IT Administrator
```

---

## Attack Example

An email claims:

```text
From: CEO

Transfer funds immediately.
```

Employees often comply because the request appears to originate from authority.

---

## Why It Works

Humans are conditioned to obey authority figures.

This behavior exists in:

* Schools
* Workplaces
* Governments

---

## Defense

Always verify requests independently.

Do not assume authority equals legitimacy.

---

# 2. Urgency / Scarcity

## Definition

Attackers create pressure so victims act quickly.

---

## Examples

```text
Account expires in 1 hour.
Immediate action required.
Last chance to claim reward.
```

---

## Why It Works

Urgency reduces critical thinking.

Victims focus on solving the problem rather than verifying legitimacy.

---

## Defense

Pause and verify.

Legitimate organizations rarely require immediate action without verification.

---

# 3. Social Proof

## Definition

People are influenced by the actions of others.

---

## Examples

```text
All employees have completed this survey.
Everyone in your department has updated their password.
```

---

## Why It Works

Humans naturally follow group behavior.

Victims think:

```text
If everyone else did it,
it must be safe.
```

---

## Defense

Verify information independently.

Do not assume safety because others appear to participate.

---

# 4. Liking

## Definition

People trust people they like.

---

## Techniques Used

Attackers build rapport through:

```text
Compliments
Shared Interests
Friendly Conversations
Professional Networking
```

---

## Example

An attacker connects on LinkedIn and gradually builds trust before requesting information.

---

## Defense

Trust should be based on verification rather than friendliness.

---

# 5. Reciprocity

## Definition

Humans feel obligated to return favors.

---

## Example

Attacker helps an employee solve a small problem.

Later requests:

```text
Can you quickly share this document?
```

The employee feels indebted.

---

## Defense

Security policies must never be bypassed because someone was helpful.

---

# 6. Commitment

## Definition

People prefer to remain consistent with previous actions.

---

## Example

Attacker asks:

```text
Can you confirm your employee ID?
```

Victim agrees.

Then:

```text
Can you confirm your email?
```

Victim agrees.

Finally:

```text
Can you verify your reset code?
```

Victim may continue cooperating.

---

## Defense

Evaluate every request independently.

---

# The Phishing Family

Phishing is a category of attacks rather than a single attack.

All phishing attacks aim to trick victims into revealing information or performing actions.

---

# 1. Phishing

## Definition

Mass attack sent to a large number of users.

---

## Example

```text
Your bank account has been suspended.
Click here.
```

---

## Characteristics

```text
Generic
Broad Audience
Low Personalization
```

---

# 2. Spear Phishing

## Definition

Targeted phishing attack against a specific individual or organization.

---

## Example

```text
Hi Udhaya,

Please review the updated CDAC assignment.
```

---

## Characteristics

```text
Highly Personalized
Uses Reconnaissance
Higher Success Rate
```

---

# 3. Whaling

## Definition

Phishing attack targeting high-value individuals.

---

## Targets

```text
CEO
CFO
Director
Senior Management
```

---

## Goal

Obtain:

```text
Financial Access
Sensitive Information
Administrative Privileges
```

---

# 4. Business Email Compromise (BEC)

## Definition

Attacker impersonates:

```text
Executive
Vendor
Partner
```

to commit financial fraud.

---

## Example

```text
Transfer ₹25 Lakhs immediately.
```

appears to come from the CFO.

---

## Impact

BEC attacks cause billions of dollars in losses globally.

---

# 5. Vishing

## Definition

Voice Phishing.

Conducted through telephone calls.

---

## Example

```text
This is your bank.
Please share your OTP.
```

---

# Goal

Steal:

```text
OTP
Credentials
Financial Information
```

---

# 6. Smishing

## Definition

SMS-based phishing.

---

## Example

```text
Parcel delivery failed.
Click here.
```

---

# 7. Clone Phishing

## Definition

Attacker copies a legitimate email.

The attachment or link is replaced with a malicious one.

---

## Why Dangerous?

Victims may already trust the original email.

---

# 8. Angler Phishing

## Definition

Attackers impersonate customer support accounts on social media.

---

## Example

Victim posts:

```text
My banking app is not working.
```

Fake support account responds.

Victim unknowingly shares information.

---

# Anatomy of a Phishing Message

Most phishing messages contain five common components.

---

# 1. Spoofed Sender

Fake sender identity.

Example:

```text
support@paypaI.com
```

where:

```text
I ≠ l
```

---

# 2. Pretext

The story used to justify the message.

Examples:

```text
Security Alert
Invoice Attached
Password Expired
```

---

# 3. Emotional Trigger

Examples:

```text
Fear
Urgency
Authority
Curiosity
```

---

# 4. Call to Action

Requests action.

Examples:

```text
Click Here
Open Attachment
Verify Account
```

---

# 5. Payload

Final objective.

Examples:

```text
Credential Theft
Malware
Ransomware
Remote Access
```

---

# Golden Rule

The instructor highlighted:

> Verify through another communication channel.

Example:

If an email claims to be from your manager:

```text
Call your manager.
Message your manager.
Verify independently.
```

---

# Beyond Email Attacks

Not all social engineering occurs through email.

Several other attack types exist.

---

# Pretexting

## Definition

Creating a believable identity or scenario to obtain information.

---

## Examples

Pretending to be:

```text
IT Support
HR Department
Police Officer
Bank Employee
```

---

## Goal

Gather:

```text
Credentials
Internal Information
Sensitive Data
```

---

# Baiting

## Definition

Using curiosity or rewards to lure victims.

---

## Examples

```text
Free Software
Free Movie Download
Gift Card
USB Drive
```

---

## Classic Example

USB labeled:

```text
Salary_2026.xlsx
```

left in a parking lot.

Victim inserts it.

Malware executes.

---

# Quid Pro Quo

## Definition

"Something for something."

Attacker offers a service in exchange for access.

---

## Example

```text
Free Technical Support
```

in exchange for remote access.

---

# Tailgating

## Definition

Physical access attack.

Attacker follows an authorized employee into a restricted area.

---

## Example

```text
Can you hold the door?
```

Employee grants access.

Attacker enters secure area.

---

# Dumpster Diving

## Definition

Searching discarded materials for information.

---

## Examples

Recovering:

```text
Employee Directories
Network Diagrams
Passwords
Printed Reports
```

from trash bins.

---

# Watering Hole Attack

## Definition

Attacker compromises a website frequently visited by the target group.

---

## Process

1. Identify target community.
2. Identify trusted websites.
3. Compromise website.
4. Wait for victims to visit.
5. Deliver malware.

---

## Why Called Watering Hole?

Animals gather around water sources.

Predators wait nearby.

Similarly:

Attackers wait where victims naturally gather.

---

# Social Engineering Attack Flow

```text
Reconnaissance
      ↓
OSINT
      ↓
Target Profiling
      ↓
Trust Building
      ↓
Manipulation
      ↓
Information Disclosure
      ↓
System Compromise
```

---

# Key Takeaways

* Social engineering targets people rather than technology.
* Reconnaissance makes social engineering more effective.
* Authority, urgency, and trust are common manipulation techniques.
* Phishing exists in many forms.
* Most phishing attacks contain predictable components.
* Verification through independent channels is one of the strongest defenses.
* Human awareness remains one of the most important cybersecurity controls.

---

# Practical Demonstrations: Nmap, Gobuster & Recon Workflow

---

# Practical Reconnaissance Tools

After understanding vulnerabilities, reconnaissance, OSINT, enumeration, and social engineering concepts, the session moved into practical demonstrations using industry-standard tools.

The primary tools demonstrated were:

```text
Nmap
Gobuster
WHOIS
```

These tools are extensively used during:

* Penetration Testing
* Vulnerability Assessments
* Red Team Operations
* Security Audits
* Bug Bounty Programs

---

# Nmap (Network Mapper)

## Introduction

Nmap is one of the most widely used network reconnaissance and enumeration tools in cybersecurity.

Website:

```text
https://nmap.org
```

Nmap is used to:

* Discover hosts
* Discover open ports
* Identify services
* Identify service versions
* Perform OS detection
* Perform network mapping

---

# Why Nmap Matters

Suppose an attacker discovers:

```text
target.com
```

This alone provides little information.

Nmap helps answer:

```text
Is the system alive?
Which ports are open?
What services are running?
Which versions are running?
```

This information is often the foundation of future attacks.

---

# Host Discovery

## Objective

Determine whether a target is alive.

---

## Command Demonstrated

```bash
nmap -sn google.com
```

---

## Understanding the Command

### nmap

Invokes the Network Mapper tool.

---

### -sn

Means:

```text
Ping Scan
No Port Scan
```

Purpose:

```text
Check if host is alive.
```

---

# Sample Output

```text
Nmap scan report for google.com
Host is up.
```

---

# What We Learn

We learn:

```text
Target Exists
Target Responds
Target Reachable
```

We do NOT learn:

```text
Open Ports
Services
Versions
```

---

# Real World Analogy

Imagine standing outside a building.

Host Discovery answers:

```text
Is anyone inside?
```

without entering.

---

# Reverse DNS (rDNS)

The demonstration also showed:

```text
rDNS Record
```

Reverse DNS converts:

```text
IP Address
```

into:

```text
Domain Name
```

Example:

```text
192.x.x.x
```

↓

```text
google.com
```

---

# Port Scanning

## Objective

Identify which ports are open.

---

## Command Demonstrated

```bash
nmap google.com
```

---

# What Happens?

Nmap:

1. Confirms host is alive.
2. Scans common ports.
3. Reports open services.

---

# Example Output

```text
21/tcp open ftp
80/tcp open http
443/tcp open https
2000/tcp open cisco-sccp
```

---

# Understanding Ports

A port is a logical communication endpoint.

Think:

```text
IP Address = Building
Port = Room Number
```

---

# Common Ports

| Port | Service |
| ---- | ------- |
| 21   | FTP     |
| 22   | SSH     |
| 25   | SMTP    |
| 53   | DNS     |
| 80   | HTTP    |
| 110  | POP3    |
| 143  | IMAP    |
| 443  | HTTPS   |
| 3306 | MySQL   |

---

# Why Open Ports Matter

Each open port represents:

```text
Potential Functionality
Potential Exposure
Potential Attack Surface
```

Attackers often begin by identifying open ports.

---

# Service Detection

## Objective

Determine exactly what software is running.

---

## Command Demonstrated

```bash
nmap -sV google.com
```

---

# Understanding -sV

```text
Service Version Detection
```

Nmap attempts to identify:

```text
Software
Version
Protocol
```

---

# Example Output

```text
80/tcp open http gws
443/tcp open ssl/http gws
```

---

# What is GWS?

```text
Google Web Server
```

Nmap identified Google's web server software.

---

# Why Version Detection Matters

Suppose Nmap reveals:

```text
Apache 2.4.41
```

Attacker searches:

```text
Apache 2.4.41 CVE
```

Potentially discovering:

```text
Known Vulnerabilities
Public Exploits
Security Advisories
```

---

# Unrecognized Services

The demonstration showed:

```text
2 services unrecognized despite returning data
```

Meaning:

* Nmap received responses.
* Responses did not match known fingerprints.

Nmap provides:

```text
Service Fingerprints
```

for manual analysis.

---

# Practical Recon Workflow Using Nmap

```text
Target Domain
      ↓
Host Discovery
      ↓
Port Scan
      ↓
Service Detection
      ↓
Version Identification
      ↓
Vulnerability Research
```

---

# Gobuster

## Introduction

Gobuster is a content discovery and enumeration tool.

Used to discover:

```text
Directories
Files
Subdomains
Virtual Hosts
Cloud Storage Buckets
```

---

# Why Gobuster Matters

Websites often contain hidden resources.

Examples:

```text
/admin
/backup
/dev
/uploads
```

These may not be linked publicly.

Gobuster helps discover them.

---

# Gobuster Modes

The instructor discussed several modes.

---

## Directory Enumeration (dir)

Purpose:

```text
Find Hidden Directories
Find Hidden Files
```

---

## Example Command

```bash
gobuster dir -u http://target.com -w wordlist.txt
```

---

# Parameters

### -u

Target URL

Example:

```text
http://target.com
```

---

### -w

Wordlist

Example:

```text
common.txt
```

Contains thousands of guesses.

---

# What Gobuster Does

Suppose wordlist contains:

```text
admin
backup
test
uploads
```

Gobuster tries:

```text
target.com/admin
target.com/backup
target.com/test
target.com/uploads
```

---

# Example Results

```text
/admin
/uploads
/backup
```

Discovered successfully.

---

# Why Hidden Directories Matter

They may expose:

```text
Administrative Panels
Debug Pages
Backups
Development Systems
```

---

# DNS Enumeration

## Objective

Discover subdomains.

---

## Command Demonstrated

```bash
gobuster dns -d amazon.com -w common.txt
```

---

# Important Observation

The instructor initially tried:

```bash
gobuster dns -d www.amazon.com
```

which produced an error.

Reason:

Gobuster DNS expects:

```text
Root Domain
```

not:

```text
Subdomain
```

---

# Correct Usage

```bash
gobuster dns -d amazon.com
```

---

# What Happens?

Gobuster tests:

```text
mail.amazon.com
vpn.amazon.com
api.amazon.com
dev.amazon.com
```

and checks if they exist.

---

# Why Subdomains Matter

Organizations frequently expose:

```text
Development Servers
VPN Gateways
Testing Environments
```

through subdomains.

Examples:

```text
vpn.company.com
dev.company.com
mail.company.com
```

---

# DNS Enumeration vs Directory Enumeration

## DNS Enumeration

Discovers:

```text
mail.company.com
vpn.company.com
api.company.com
```

Subdomains.

---

## Directory Enumeration

Discovers:

```text
company.com/admin
company.com/uploads
company.com/login
```

Paths inside a website.

---

# Complete Enumeration Workflow

```text
Root Domain
      ↓
DNS Enumeration
      ↓
Subdomain Discovery
      ↓
Host Discovery
      ↓
Port Scanning
      ↓
Service Detection
      ↓
Directory Enumeration
      ↓
Vulnerability Analysis
```

---

# Practical Recon Pipeline Learned in Session 5

The session gradually built a complete attacker workflow.

---

## Phase 1 – Passive Recon

Using:

```text
WHOIS
CT Logs
Social Media
LinkedIn
Job Postings
Wayback Machine
Shodan
Google Dorking
```

Goal:

```text
Build Target Profile
```

---

## Phase 2 – Active Recon

Using:

```text
Nmap
Gobuster
DNS Queries
Enumeration
```

Goal:

```text
Validate Information
Identify Attack Surface
```

---

## Phase 3 – Analysis

Using:

```text
CVE
NVD
CVSS
```

Goal:

```text
Find Weaknesses
```

---

## Phase 4 – Exploitation Planning

Using gathered intelligence.

Examples:

```text
Phishing
Credential Attacks
Vulnerability Exploitation
```

---

# Complete Reconnaissance Workflow

```text
WHOIS
    ↓
Certificate Transparency
    ↓
Social Media
    ↓
Job Postings
    ↓
Wayback Machine
    ↓
Shodan
    ↓
Google Dorking
    ↓
Target Profiling
    ↓
Host Discovery
    ↓
Port Scanning
    ↓
Service Detection
    ↓
DNS Enumeration
    ↓
Directory Enumeration
    ↓
Vulnerability Research
    ↓
Attack Planning
```

---

# Interview Questions

## What is the difference between Scanning and Enumeration?

Scanning identifies:

```text
What exists?
```

Enumeration identifies:

```text
What exactly is running?
```

---

## What is the difference between Passive and Active Recon?

Passive:

```text
No interaction with target.
```

Active:

```text
Direct interaction with target.
```

---

## Why is Reconnaissance Important?

Reconnaissance reduces uncertainty and provides intelligence that makes attacks more effective.

---

## Why is OSINT Powerful?

OSINT reveals valuable information without touching the target.

---

## Why is Service Detection Important?

Because software versions help identify known vulnerabilities.

---

## What is Gobuster Used For?

Gobuster performs:

```text
Directory Enumeration
DNS Enumeration
Subdomain Discovery
```

---

## What is Nmap Used For?

Nmap performs:

```text
Host Discovery
Port Scanning
Service Detection
Network Mapping
```

---
Key Takeaways

* Reconnaissance is the first stage of most cyber attacks.
* OSINT can reveal significant intelligence without interacting with the target.
* Passive recon is stealthy but limited.
* Active recon is accurate but detectable.
* Enumeration provides deeper intelligence than scanning.
* WHOIS, CT Logs, Shodan, and Google Dorking are powerful OSINT resources.
* Social engineering remains one of the most effective attack techniques.
* Nmap is the industry-standard reconnaissance tool.
* Gobuster is widely used for content and DNS discovery.
* Reconnaissance often determines the success of later attack phases.

---

# End of Session 5

**Topics Covered:**

✅ Vulnerabilities
✅ CVE, NVD, CVSS
✅ OWASP Top 10
✅ SSRF
✅ Attack Surface
✅ Reconnaissance
✅ OSINT
✅ Passive Reconnaissance
✅ Active Reconnaissance
✅ Scanning vs Enumeration
✅ Banner Grabbing
✅ DNS Enumeration
✅ SMTP Enumeration
✅ SNMP Enumeration
✅ WHOIS
✅ Certificate Transparency
✅ Job Posting Intelligence
✅ Social Media Intelligence
✅ Wayback Machine
✅ Shodan
✅ Google Dorking
✅ Social Engineering
✅ Principles of Influence
✅ Phishing Family
✅ Anatomy of Phishing
✅ Pretexting
✅ Baiting
✅ Quid Pro Quo
✅ Tailgating
✅ Dumpster Diving
✅ Watering Hole Attack
✅ Nmap Host Discovery
✅ Nmap Port Scanning
✅ Nmap Service Detection
✅ Gobuster Directory Enumeration
✅ Gobuster DNS Enumeration

---
