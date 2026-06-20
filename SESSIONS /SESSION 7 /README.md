
# Session 7 – Footprinting and Reconnaissance

## Part 1 – Topics 1 to 4

**Date:** 18 June 2026
**Course:** CDAC Industry Exposure Program – Cybersecurity

---

# 1. Footprinting Fundamentals

## Definition

Footprinting is the process of collecting information about a target system, network, organization, or individual before attempting any security assessment or attack.

It is the first phase of:

* Penetration Testing
* Vulnerability Assessment
* Ethical Hacking
* Cyber Attacks

The PPT states:

> This step acts as a preparatory phase for the attacker, who needs to gather as much information as possible to easily find ways to intrude into the target network.

The instructor emphasized:

> If your initial information is wrong, everything afterwards becomes garbage.

Therefore:

```text
Garbage In → Garbage Out
```

Good reconnaissance leads to successful penetration testing.

---

## Why Footprinting Is Important

Suppose you want to attack or assess:

```text
example.com
```

Without footprinting you know nothing.

After footprinting you may know:

* Domain names
* Subdomains
* IP addresses
* Employees
* Email addresses
* Web technologies
* Firewalls
* VPN gateways
* Open-source documents
* Breached credentials
* Public repositories
* Server locations

All these become entry points.

---

## Role in Penetration Testing

Footprinting is equivalent to military reconnaissance.

Before a war, armies first collect:

* Terrain information
* Enemy strength
* Supply routes

Similarly, cyber attackers first collect intelligence.

---

## Information Gathering vs Footprinting

Both terms are often used interchangeably.

```text
Footprinting = Information Gathering
```

Goal:

```text
Collect maximum information
↓
Reduce uncertainty
↓
Find weaknesses
```

---

# 2. Types of Footprinting

The PPT divides footprinting into two categories.

---

# Passive Footprinting

## Definition

Information gathering without interacting directly with the target.

Target does not know you are collecting information.

---

### Examples

Searching:

* Google
* LinkedIn
* Facebook
* Medium
* GitHub
* Job portals
* News articles

---

### Example

Finding employees on LinkedIn:

```text
site:linkedin.com "Microsoft" Security Engineer
```

No packets are sent to Microsoft's network.

Hence:

```text
Invisible to target
```

---

### Sources Used

Social media:

* LinkedIn
* Twitter
* Facebook

Search engines:

* Google
* Bing

Public databases:

* WHOIS
* DNS records

Breach databases:

* HaveIBeenPwned

GitHub repositories

Press releases

Annual reports

Government records

---

## Advantages

* Safe
* Stealthy
* Legal
* No IDS alerts
* No firewall logs

---

## Disadvantages

Information may be outdated.

Cannot discover internal services.

---

# Active Footprinting

## Definition

Information gathering involving direct interaction with the target.

Target systems receive packets.

---

Examples:

### Ping

```bash
ping target.com
```

---

### DNS Query

```bash
nslookup target.com
```

---

### Traceroute

```bash
traceroute target.com
```

---

### Nmap

```bash
nmap target.com
```

---

### Banner Grabbing

```bash
telnet IP port
```

---

Target may detect:

* Your IP address
* Logs
* Firewall events
* IDS alerts

---

## Advantages

More accurate.

Real-time information.

Discovers:

* Ports
* Services
* Operating systems

---

## Disadvantages

Can be detected.

---

## Comparison

| Feature            | Passive          | Active     |
| ------------------ | ---------------- | ---------- |
| Direct interaction | No               | Yes        |
| Detection          | Difficult        | Possible   |
| Stealth            | High             | Low        |
| Accuracy           | Medium           | High       |
| Legal risk         | Low              | Moderate   |
| Examples           | Google, LinkedIn | Ping, Nmap |

---

# 3. Information Obtained During Footprinting

According to the PPT, information falls into three categories.

---

# A. Organization Information

This describes the company itself.

Examples:

## Employee Details

* Names
* LinkedIn profiles
* Designations
* Departments
* Emails

---

## Telephone Numbers

* Customer care numbers
* Support numbers
* Corporate contacts

---

## Branch Locations

* Head office
* Regional offices
* Data centers
* Manufacturing plants

---

## Background Information

* Company history
* Acquisitions
* Business partners
* Revenue
* Competitors

---

## Technologies Used

* WordPress
* Angular
* React
* AWS
* Azure
* Fortinet
* Cisco
* Palo Alto

---

## Public Documents

* Press releases
* PDF documents
* Annual reports
* Whitepapers
* Brochures

These reveal infrastructure details.

---

# B. Network Information

Information about the network itself.

---

## Domain Names

Example:

```text
google.com
```

---

## Subdomains

```text
mail.google.com
accounts.google.com
docs.google.com
```

Different subdomains may host different services.

---

## Network Blocks

Example:

```text
142.250.0.0/16
```

Shows IP ranges owned by the organization.

---

## Topology

* Routers
* Firewalls
* ISP
* Connectivity

---

## Reachable IP Addresses

* Servers
* VPN gateways
* Mail servers
* DNS servers

---

## WHOIS Records

Contain:

* Owner information
* Registrar details
* Creation date
* Expiry date
* Name servers

---

## DNS Records

Examples:

* A Record
* MX Record
* TXT Record
* NS Record
* PTR Record

---

# C. System Information

The PPT specifically lists:

---

## Web Server Operating System

Examples:

* Linux
* Ubuntu
* Windows Server
* CentOS
* Apache
* Nginx

---

## Server Locations

* Country
* City
* Cloud Provider
* Region

---

## Public Email Addresses

Example:

```text
admin@example.com
support@example.com
ceo@example.com
```

Useful for phishing and social engineering.

---

## Usernames and Passwords

May appear in:

* GitHub
* Pastebin
* Breach databases
* Public leaks

---

# 4. Footprinting Threats

The information collected can be abused.

---

## Social Engineering

Knowing employee names helps attackers create believable phishing emails.

Example:

```text
Hi Rahul,

IT Department requests password verification.
```

Victim trusts the message because the attacker already knows:

* Name
* Department
* Role

---

## System Attacks

Knowing:

```text
Apache 2.4.49
```

May reveal known vulnerabilities.

---

## Network Attacks

Knowing:

```text
VPN Gateway IP
```

Allows targeted attacks.

---

## Information Leakage

Sensitive documents accidentally published online may reveal:

* Passwords
* API keys
* Configurations

---

## Privacy Loss

Employees may expose:

* Phone numbers
* Addresses
* Birthdays

---

## Corporate Espionage

Competitors may learn:

* Technologies
* Vendors
* Projects
* Architecture

---

## Business Loss

Consequences:

* Data breaches
* Financial losses
* Reputation damage

---

# Instructor's Main Message

The most important phase of penetration testing is:

```text
Footprinting + Reconnaissance
```

Because:

```text
Bad information
↓
Wrong assumptions
↓
Wrong vulnerabilities
↓
Failed penetration
```

The quality of the entire pentest depends on how good the information gathering phase is.

---

# Key Takeaways

* Footprinting is the first phase of ethical hacking.
* It aims to gather maximum information about the target.
* Passive footprinting does not directly interact with the target.
* Active footprinting involves direct interaction.
* Information collected may include organization details, network information, and system information.
* Attackers use footprinting to identify possible entry points.
* Accurate reconnaissance determines the success of later stages of penetration testing.

# Session 7 – Footprinting and Reconnaissance

## Part 2 – Topics 5 to 10

**Date:** 18 June 2026
**Course:** CDAC Industry Exposure Program – Cybersecurity

---

# 5. Footprinting Methodology

Footprinting is not random information collection.

A professional penetration tester follows a systematic process.

```text
Target
    ↓
Collect Public Information
    ↓
Analyze
    ↓
Correlate Findings
    ↓
Identify Attack Surface
```

The instructor emphasized:

> The more information you collect, the narrower your attack becomes.

---

## Goal

Transform:

```text
Unknown Target
```

into

```text
Known Infrastructure
```

by collecting:

* Domains
* IP ranges
* Employees
* Emails
* Technologies
* Servers
* Documents
* Social media information

---

## Information Sources

### Human Sources

* Employees
* LinkedIn
* Social Media

---

### Technical Sources

* WHOIS
* DNS
* Google
* Shodan
* GitHub

---

### Public Documents

* PDFs
* PPTs
* Annual reports
* Whitepapers

---

### Breach Databases

* HaveIBeenPwned
* Pastebin
* Breach forums

---

# Typical Flow

```text
Company Name
        ↓
Domain
        ↓
Subdomains
        ↓
Email Addresses
        ↓
Employees
        ↓
Technologies
        ↓
Attack Surface
```

---

# 6. Search Engine Footprinting

Search engines contain enormous amounts of publicly accessible information.

Most organizations unknowingly expose:

* PDFs
* Employee lists
* Login pages
* Internal portals
* Configuration files

The attacker uses search engines to discover these.

---

## Search Engines Used

### Google

Most common.

---

### Bing

Alternative source.

---

### Yahoo

Provides indexed pages.

---

### DuckDuckGo

Privacy-oriented search engine.

---

### Baidu

Useful for Chinese domains.

---

### Yandex

Useful for Russian infrastructure.

---

# Why Search Engines Matter

Search engines have already crawled and indexed websites.

Therefore, attackers don't need to scan immediately.

They simply search.

---

Example:

Searching

```text
company annual report pdf
```

may reveal:

* Employee names
* Technologies
* Email addresses

without sending any packets to the target.

This is passive reconnaissance.

---

# 7. Google Dorking

Google Dorking is the process of using advanced search operators to locate sensitive information.

Google is effectively a huge database.

The attacker asks:

```text
Can Google show me hidden information?
```

---

Example:

Instead of

```text
Microsoft
```

the attacker searches:

```text
site:microsoft.com filetype:pdf
```

and retrieves only PDF documents.

---

## Why Google Dorking Works

Search engines index:

* Files
* Web pages
* Login portals
* Cameras
* Directories
* Configurations

Improperly exposed resources become searchable.

---

## Information Found Using Dorks

* Password files
* Admin pages
* Database dumps
* Configuration files
* Backups
* Cameras
* Internal documents

---

Google Dorking itself is not illegal.

Unauthorized access to discovered systems is illegal.

---

# 8. Important Google Operators

---

## site:

Restricts search to a domain.

Example:

```text
site:amazon.com
```

Searches only Amazon.

---

Example:

```text
site:linkedin.com cybersecurity engineer
```

Useful for employee discovery.

---

## filetype:

Search specific file types.

Example:

```text
filetype:pdf
```

Returns PDF documents.

---

Examples:

```text
filetype:xlsx
filetype:docx
filetype:ppt
```

---

## intitle:

Searches page titles.

Example:

```text
intitle:"login"
```

Returns pages containing login.

---

Example:

```text
intitle:"admin"
```

May reveal admin portals.

---

## inurl:

Search inside URLs.

Example:

```text
inurl:admin
```

Finds:

```text
/admin
/adminlogin
/adminpanel
```

---

## cache:

Displays cached pages.

Example:

```text
cache:example.com
```

Useful if the page has been removed.

---

## related:

Finds similar websites.

Example:

```text
related:amazon.com
```

---

## define:

Provides definitions.

Example:

```text
define:malware
```

---

## link:

Shows pages linking to a target.

Example:

```text
link:example.com
```

---

# Combining Operators

Example:

```text
site:company.com filetype:pdf
```

Only PDF documents from that company.

---

Example:

```text
site:company.com intitle:login
```

Searches login pages.

---

Example:

```text
site:company.com inurl:admin
```

Searches admin interfaces.

---

# 9. Google Hacking Database (GHDB)

The Google Hacking Database contains pre-built Google Dorks.

Maintained originally by:

```text
Exploit Database
```

---

Purpose:

Instead of creating dorks manually, researchers use existing queries.

---

Categories include:

### Files containing passwords

Examples:

```text
password.txt
config.php
backup.sql
```

---

### Login Portals

Searches:

```text
admin
administrator
cpanel
```

---

### Directory Listings

Exposed folders.

Example:

```text
Index of /
```

---

### Vulnerable Devices

Routers

Printers

IP cameras

SCADA systems

---

### Database Files

SQL dumps

CSV files

Excel sheets

---

### Sensitive Documents

PDFs

DOCX

PPTs

---

## Example

Search:

```text
intitle:"index of" backup
```

May reveal publicly exposed backups.

---

## Purpose of GHDB

Security researchers use GHDB to:

* Find exposures
* Assess risks
* Educate organizations

---

# 10. VPN Footprinting Through Google Dorks

Many organizations expose VPN portals publicly.

Examples:

---

## Cisco VPN

Search:

```text
intitle:"Cisco Systems VPN"
```

---

## Fortinet VPN

Search:

```text
intitle:"Fortinet"
```

---

## Pulse Secure VPN

Search:

```text
inurl:"/dana-na/"
```

---

## Palo Alto VPN

Search:

```text
inurl:"global-protect"
```

---

## Citrix Gateways

Search:

```text
inurl:"citrix"
```

---

# Why Attackers Look for VPNs

VPN servers are Internet-facing.

They often become initial entry points.

Attackers may:

1. Identify VPN portals.

2. Determine vendor.

3. Look for known vulnerabilities.

4. Attempt credential attacks.

---

# Example Workflow

```text
Company Name
        ↓
Google Dork
        ↓
VPN Portal Found
        ↓
Vendor Identified
        ↓
Version Enumeration
        ↓
Known CVEs Checked
```

---

# Instructor's Main Message

Search engines are one of the strongest reconnaissance tools.

A large amount of information can be obtained without touching the target network.

```text
Google
+
Open Source Information
=
Powerful Passive Reconnaissance
```

---

# Key Takeaways

* Footprinting follows a systematic methodology.
* Search engines are powerful OSINT tools.
* Google Dorking uses advanced operators.
* Operators like site:, filetype:, intitle:, and inurl: refine searches.
* GHDB contains ready-made dorks.
* VPN portals are commonly discovered using passive reconnaissance.
* Search engines provide enormous intelligence without generating network traffic.
