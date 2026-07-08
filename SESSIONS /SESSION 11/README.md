# Session 11 – Defensive Security and the Security Operations Centre (SOC)
## Part 1 – Introduction to Defensive Security

**Course:** C-DAC Kolkata – Cybersecurity Industry Exposure Program  
**Module:** Module 6 – Defensive Security & the Security Operations Centre  
**Duration:** 2 Hours (Theory)  
**Platform Demonstrated:** Wazuh SIEM/XDR

---

# Overview

Until this point in the course, every practical exercise was performed from the **attacker's perspective**.

Students learned how to:

- Perform reconnaissance
- Scan networks
- Enumerate services
- Conduct ARP poisoning
- Perform Man-in-the-Middle attacks
- Capture packets
- Exploit vulnerable services
- Gain shell access

However, a real organization spends most of its effort **defending** systems rather than attacking them.

This session introduces the opposite perspective:

> **If someone performs those attacks against your organization, how do you detect them?**

This question forms the foundation of **Defensive Security**.

---

# The Shift from Red Team to Blue Team

Cybersecurity can broadly be divided into two perspectives.

## Offensive Security (Red Team)

The Red Team simulates attackers.

Their responsibilities include:

- Discovering vulnerabilities
- Exploiting weaknesses
- Testing security controls
- Demonstrating attack paths
- Validating security posture

The goal is **not destruction**, but to identify weaknesses before real attackers do.

---

## Defensive Security (Blue Team)

The Blue Team protects organizational assets.

Responsibilities include:

- Monitoring systems
- Detecting attacks
- Investigating suspicious activity
- Responding to incidents
- Restoring normal operations
- Improving future defenses

Unlike the Red Team, whose work is often project-based, the Blue Team operates continuously.

---

# Why Learn Offensive Security First?

The instructor emphasized an important principle:

> **You cannot defend what you do not understand.**

Consider a firewall administrator.

If they do not understand:

- Port scanning
- SQL Injection
- ARP Spoofing
- Password attacks
- Privilege escalation

they cannot effectively detect or stop those attacks.

Understanding the attacker's mindset enables defenders to:

- Recognize attack patterns
- Anticipate attacker behavior
- Build effective detections
- Reduce response time

---

# The Cybersecurity Journey

The course progression follows a logical path.

```text
Understand Networks

↓

Learn Attacks

↓

Perform Attacks

↓

Understand Detection

↓

Monitor Systems

↓

Respond to Incidents

↓

Improve Security
```

This mirrors how many cybersecurity professionals build expertise.

---

# The Philosophy of Defensive Security

Historically, organizations believed that security meant preventing every attack.

The traditional mindset was:

```text
Build Strong Walls

↓

Prevent Every Intrusion
```

This approach assumed that perfect prevention was achievable.

Modern cybersecurity has shown that this assumption is unrealistic.

---

# The "Assume Breach" Philosophy

Modern defensive security operates on a different assumption:

> **Every organization should assume that attackers will eventually breach its defenses.**

This concept is known as **Assume Breach**.

Rather than asking:

> "How do we stop every attack?"

organizations ask:

> "How quickly can we detect and contain an attack after it occurs?"

This shift fundamentally changed cybersecurity operations.

---

# Preventive Security

Preventive security aims to stop attacks before they succeed.

Examples include:

- Firewalls
- Access control
- Multi-Factor Authentication (MFA)
- Patch management
- Secure configurations
- Network segmentation
- Endpoint protection

These controls reduce the likelihood of compromise.

However, no preventive control is perfect.

---

# Detective Security

Detective security focuses on identifying malicious activity after or during an attack.

Examples include:

- Security Information and Event Management (SIEM)
- Intrusion Detection Systems (IDS)
- Log monitoring
- Endpoint Detection and Response (EDR)
- File Integrity Monitoring (FIM)
- Threat intelligence correlation

The objective is early detection.

---

# Responsive Security

Once an attack has been detected, the organization must respond.

Response activities include:

- Isolating compromised systems
- Blocking malicious IP addresses
- Disabling compromised accounts
- Collecting forensic evidence
- Removing malware
- Restoring services
- Updating detection rules

Response minimizes damage and restores business operations.

---

# Comparing Security Approaches

| Preventive Security | Detective Security | Responsive Security |
|---------------------|--------------------|---------------------|
| Stops attacks | Detects attacks | Handles attacks |
| Firewall | SIEM | Incident Response |
| MFA | IDS | Host Isolation |
| Patching | Log Analysis | Malware Removal |
| Hardening | Threat Detection | Recovery |

Effective cybersecurity requires all three approaches working together.

---

# Why Perfect Prevention Is Impossible

Modern environments are extremely complex.

Organizations manage:

- Thousands of endpoints
- Cloud infrastructure
- Mobile devices
- Remote employees
- Third-party integrations
- Web applications
- APIs

Each component introduces potential attack surfaces.

As environments grow, achieving perfect prevention becomes impossible.

---

# The Importance of Detection Speed

An attack that remains undetected for weeks can result in:

- Credential theft
- Data exfiltration
- Ransomware deployment
- Lateral movement
- Persistence mechanisms
- Financial loss
- Reputational damage

The period between compromise and detection is known as **Dwell Time**.

Reducing dwell time is one of the primary objectives of modern defensive security.

---

# From Attacks to Detection

Throughout earlier sessions, students generated attack activity such as:

- Port scans
- Failed logins
- ARP spoofing
- Service exploitation

Each of these actions leaves evidence.

Examples include:

- Authentication logs
- Network logs
- Firewall logs
- Web server logs
- Process creation logs
- System event logs

The Blue Team analyzes these records to identify malicious activity.

---

# Key Terminology

### Red Team

Simulates attackers to identify security weaknesses.

---

### Blue Team

Defends systems by monitoring, detecting, and responding to attacks.

---

### Purple Team

A collaborative approach where Red and Blue Teams work together to improve organizational security.

Purple Teaming focuses on:

- Validating detections
- Improving monitoring
- Refining response procedures

---

# Learning Objectives

After completing this session, students should be able to:

- Explain the goals of defensive security.
- Describe the difference between preventive, detective, and responsive security.
- Explain why modern organizations assume breaches will occur.
- Understand the relationship between offensive and defensive security.
- Recognize the importance of rapid detection and response.
- Describe the role of a Blue Team within an organization.

---

# Interview Questions

## Why is offensive security taught before defensive security?

Understanding attacker techniques enables defenders to recognize, detect, and respond to attacks more effectively.

---

## What is the "Assume Breach" philosophy?

It is the security principle that organizations should assume attackers will eventually bypass preventive controls and therefore prioritize rapid detection and response.

---

## What is the difference between preventive and detective security?

Preventive security aims to stop attacks before they occur, while detective security focuses on identifying attacks that have already begun or succeeded.

---

## What is a Purple Team?

A collaborative practice in which Red Team and Blue Team members work together to improve detection capabilities and overall security posture.

---

# Key Takeaways

- Modern cybersecurity extends beyond prevention; it emphasizes rapid detection and effective response.
- Offensive knowledge strengthens defensive capabilities.
- Perfect prevention is unrealistic in complex environments.
- The "Assume Breach" philosophy underpins modern defensive security.
- Blue Teams continuously monitor systems, while Purple Teams ensure that offensive findings improve defensive controls.

# Session 11 – Defensive Security and the Security Operations Centre (SOC)
## Part 2 – Security Operations Centre (SOC)

**Course:** C-DAC Kolkata – Cybersecurity Industry Exposure Program  
**Module:** Defensive Security and SOC Operations

---

# Introduction to the Security Operations Centre (SOC)

Once an organization understands that cyber attacks are inevitable, the next question becomes:

> **Who monitors the organization's systems every minute of every day?**

The answer is the **Security Operations Centre (SOC).**

A Security Operations Centre is the central command center responsible for continuously monitoring, detecting, investigating, analyzing, and responding to cybersecurity incidents.

Unlike penetration testing, which is usually performed periodically, SOC operations run **24 hours a day, 7 days a week, 365 days a year.**

Its primary objective is:

> Detect attacks as early as possible and minimize their impact.

---

# What is a Security Operations Centre?

A Security Operations Centre (SOC) is a dedicated team of cybersecurity professionals supported by specialized tools that continuously monitor an organization's IT infrastructure.

The SOC monitors:

- Servers
- Workstations
- Laptops
- Firewalls
- Routers
- Switches
- Active Directory
- Cloud Infrastructure
- Applications
- Databases
- Endpoint Devices
- Network Traffic

Every event generated by these systems is analyzed for signs of malicious activity.

---

# Why Organizations Need a SOC

Modern enterprises generate enormous amounts of activity every second.

Examples include:

- Millions of authentication requests
- Thousands of DNS queries
- Web application requests
- Email traffic
- VPN connections
- File modifications
- Process executions
- Network communications

It is impossible for humans to manually monitor all of this activity.

A SOC automates collection, correlation, and analysis while analysts investigate suspicious behavior.

---

# Objectives of a SOC

The main objectives of a Security Operations Centre include:

- Continuous monitoring
- Threat detection
- Incident investigation
- Incident response
- Threat hunting
- Malware analysis
- Digital forensics
- Vulnerability management
- Security reporting
- Continuous improvement

---

# Core Functions of a SOC

A mature SOC performs multiple interconnected functions.

```text
Collect Logs

↓

Normalize Data

↓

Correlate Events

↓

Generate Alerts

↓

Investigate Alerts

↓

Respond to Incidents

↓

Recover Systems

↓

Improve Detection Rules
```

This process repeats continuously.

---

# SOC Architecture

A simplified SOC architecture is shown below.

```text
                    Users
                      │
                      ▼
        ------------------------------
        | Servers  Firewalls  PCs    |
        | Routers  Switches  Cloud   |
        ------------------------------
                      │
                 Generate Logs
                      │
                      ▼
              SIEM Platform
                      │
      Correlation • Rules • Analytics
                      │
                      ▼
              Security Analysts
                      │
                      ▼
           Incident Response Team
                      │
                      ▼
              Business Recovery
```

The SIEM platform acts as the central nervous system of the SOC.

---

# Components of a SOC

A SOC generally consists of three major components:

## People

Security professionals responsible for monitoring and responding.

Examples:

- SOC Analysts
- Threat Hunters
- Incident Responders
- Malware Analysts
- Forensic Investigators

---

## Processes

Standardized procedures describing:

- Alert handling
- Escalation
- Investigation
- Incident response
- Documentation
- Reporting

Processes ensure consistency.

---

## Technology

Technology provides visibility into organizational activity.

Examples include:

- SIEM
- EDR
- IDS
- IPS
- SOAR
- Threat Intelligence Platforms
- Endpoint Monitoring
- Network Monitoring
- Ticketing Systems

---

# SOC Operating Model

A SOC follows a continuous monitoring cycle.

```text
Monitor

↓

Detect

↓

Investigate

↓

Contain

↓

Recover

↓

Improve
```

This cycle repeats continuously throughout the day.

---

# SOC Analyst Roles

SOC teams are generally organized into multiple tiers.

Each tier performs increasingly complex tasks.

---

# Tier 1 SOC Analyst

Often called the first line of defense.

Responsibilities include:

- Monitor dashboards
- Review alerts
- Verify suspicious activity
- Filter false positives
- Escalate confirmed incidents

Tier 1 analysts answer questions such as:

- Is this alert legitimate?
- Should it be investigated further?

---

# Tier 2 SOC Analyst

Tier 2 analysts perform deeper investigations.

Responsibilities include:

- Incident investigation
- Malware analysis
- Threat correlation
- Root cause analysis
- Containment recommendations

They determine:

- How the attack occurred
- Which systems are affected
- What actions are required

---

# Tier 3 SOC Analyst

Tier 3 analysts possess advanced expertise.

Responsibilities include:

- Threat hunting
- Advanced malware analysis
- Detection engineering
- SIEM rule creation
- Threat intelligence
- Tool development

Tier 3 analysts proactively search for attackers that automated systems may have missed.

---

# SOC Manager

The SOC Manager oversees operations.

Responsibilities include:

- Team coordination
- Resource planning
- Incident escalation
- Performance metrics
- Reporting
- Compliance

The manager ensures that the SOC operates efficiently.

---

# Security Teams

Organizations often use different security teams with different responsibilities.

---

## Red Team

Primary objective:

Attack systems to identify weaknesses.

Activities:

- Penetration Testing
- Exploitation
- Social Engineering
- Adversary Simulation

---

## Blue Team

Primary objective:

Protect organizational infrastructure.

Activities:

- Monitoring
- Detection
- Investigation
- Incident Response
- Threat Hunting

---

## Purple Team

The Purple Team combines Red and Blue Team expertise.

Purpose:

Improve organizational defenses by validating detection capabilities.

Instead of competing,

Red and Blue Teams collaborate.

---

# Red Team vs Blue Team vs Purple Team

| Red Team | Blue Team | Purple Team |
|-----------|-----------|-------------|
| Attack | Defend | Collaborate |
| Simulate Threats | Detect Threats | Improve Detection |
| Offensive | Defensive | Optimization |
| Finds Weaknesses | Monitors Systems | Shares Knowledge |

---

# SOC Terminology

Understanding SOC terminology is essential.

---

## Log

A log is a recorded activity generated by a system.

Examples:

```text
User Login

File Created

Application Started

Firewall Allowed Connection

DNS Query
```

Logs are raw records.

---

## Event

An event is any observable action occurring within a system.

Every event may or may not represent suspicious behavior.

Example:

```text
User logged in
```

is an event.

---

## Alert

An alert is generated when predefined rules identify potentially suspicious activity.

Example:

```text
10 Failed Login Attempts

↓

Alert Generated
```

Not every alert indicates an attack.

---

## Incident

An incident is a confirmed security event requiring investigation and response.

Example:

```text
Confirmed Malware Infection

↓

Security Incident
```

---

# Relationship Between Logs, Events, Alerts and Incidents

The instructor emphasized understanding this progression.

```text
Logs

↓

Events

↓

Correlation

↓

Alert

↓

Investigation

↓

Incident

↓

Response
```

This workflow forms the backbone of every SOC.

---

# Example Workflow

Suppose a user enters the wrong password.

System records:

```text
Failed Login
```

One failed login:

```text
Log
```

Ten failed logins:

```text
Event Pattern
```

Correlation rule triggers:

```text
Alert
```

Analyst investigates.

If confirmed to be brute force:

```text
Incident
```

The SOC now begins containment.

---

# Challenges Faced by SOCs

Modern SOCs face several operational challenges.

Examples include:

- Alert fatigue
- False positives
- Skill shortages
- Large log volumes
- Complex environments
- Cloud infrastructure
- Remote workforce
- Advanced persistent threats (APTs)

These challenges require automation and continuous tuning.

---

# Metrics Used in a SOC

Organizations evaluate SOC performance using several metrics.

Examples include:

### MTTD

Mean Time To Detect

Average time required to detect an attack.

Lower values indicate faster detection.

---

### MTTR

Mean Time To Respond

Average time required to contain and respond to an incident.

Lower values indicate more efficient incident response.

---

# Learning Objectives

After completing this section, students should be able to:

- Define a Security Operations Centre.
- Explain the purpose of continuous monitoring.
- Describe the roles of Tier 1, Tier 2, and Tier 3 analysts.
- Differentiate between Red, Blue, and Purple Teams.
- Explain the progression from Log → Event → Alert → Incident.
- Understand the operational workflow of a SOC.

---

# Interview Questions

## What is a Security Operations Centre?

A Security Operations Centre is a centralized facility responsible for continuously monitoring, detecting, investigating, and responding to cybersecurity threats across an organization's infrastructure.

---

## What is the primary responsibility of a Tier 1 SOC Analyst?

A Tier 1 analyst monitors alerts, performs initial triage, filters false positives, and escalates confirmed suspicious activity.

---

## What is the difference between an Alert and an Incident?

An alert is an indication of potentially suspicious activity generated by monitoring systems.

An incident is a verified security event that requires investigation and response.

---

## What is the role of a Purple Team?

A Purple Team facilitates collaboration between offensive (Red Team) and defensive (Blue Team) personnel to improve detection capabilities and strengthen organizational security.

---

## Why is continuous monitoring important?

Continuous monitoring enables organizations to detect attacks quickly, reduce attacker dwell time, and respond before significant damage occurs.

---

# Key Takeaways

- A Security Operations Centre (SOC) serves as the organization's cybersecurity command center.
- SOC operations are continuous and focus on monitoring, detection, investigation, and response.
- Tiered analyst roles enable efficient handling of alerts and incidents.
- Logs are transformed into events, correlated into alerts, and investigated as incidents.
- Collaboration between Red, Blue, and Purple Teams improves overall security posture.
- Metrics such as MTTD and MTTR help organizations measure SOC effectiveness.

# Session 11 – Defensive Security and the Security Operations Centre (SOC)
## Part 3 – Security Information and Event Management (SIEM)

**Course:** C-DAC Kolkata – Cybersecurity Industry Exposure Program  
**Module:** Defensive Security & Security Operations Centre (SOC)

---

# Introduction to SIEM

As organizations expanded their IT infrastructure, they began generating enormous amounts of security logs every second.

Examples include:

- User logins
- Failed login attempts
- File access
- Firewall traffic
- DNS queries
- Web requests
- Database transactions
- Endpoint activity
- Antivirus detections

A medium-sized organization may generate **millions of log entries every day**.

Reading these logs manually is impossible.

This problem led to the development of **Security Information and Event Management (SIEM)** platforms.

---

# What is SIEM?

SIEM stands for:

```text
Security Information and Event Management
```

A SIEM is a centralized security platform that:

- Collects logs
- Stores logs
- Normalizes logs
- Correlates events
- Detects suspicious activity
- Generates alerts
- Assists incident investigation
- Provides dashboards and reports

Rather than viewing logs separately from each device, a SIEM brings everything together into a single platform.

---

# Why Organizations Need SIEM

Imagine an organization with:

- 2,000 Employees
- 800 Servers
- 5,000 Endpoints
- 40 Firewalls
- 100 Network Switches
- Cloud Infrastructure
- VPN Gateways
- Active Directory
- Email Servers

Every component continuously generates logs.

Without SIEM:

```text
Server Logs

Firewall Logs

Router Logs

Application Logs

Database Logs

↓

Different Locations

↓

Manual Investigation
```

Investigation becomes extremely slow.

With SIEM:

```text
All Logs

↓

Central Collection

↓

Correlation

↓

Detection

↓

Alert

↓

Investigation
```

---

# Meaning of SIEM

The acronym consists of two parts.

## Security Information

Refers to:

- Collecting
- Storing
- Searching
- Reporting

security-related information.

This includes historical logs used for:

- Compliance
- Auditing
- Forensics

---

## Security Event Management

Focuses on:

- Real-time monitoring
- Event correlation
- Threat detection
- Alert generation
- Incident response

This enables analysts to detect attacks as they occur.

---

# Evolution of Log Management

Historically:

```text
Each Server

↓

Separate Log File

↓

Administrator Reads Logs
```

Problems:

- Difficult to correlate
- Time consuming
- No centralized visibility

Modern architecture:

```text
Servers

Firewalls

Endpoints

Cloud

↓

Central SIEM

↓

Correlation

↓

Alerts

↓

SOC Analyst
```

---

# SIEM Architecture

A simplified SIEM architecture is shown below.

```text
                Data Sources
------------------------------------------------

Servers

Firewalls

Endpoints

Routers

Switches

Cloud

Applications

Databases

------------------------------------------------

          │
          ▼

Log Collection

          │
          ▼

Log Normalization

          │
          ▼

Correlation Engine

          │
          ▼

Alert Generation

          │
          ▼

SOC Dashboard

          │
          ▼

Security Analysts
```

---

# Data Sources

A SIEM collects information from many different systems.

Examples include:

## Operating Systems

- Windows
- Linux
- macOS

---

## Network Devices

- Routers
- Switches
- Firewalls

---

## Security Devices

- IDS
- IPS
- Antivirus
- EDR
- Proxy Servers

---

## Cloud Platforms

- AWS
- Azure
- Google Cloud

---

## Applications

- Apache
- Nginx
- IIS
- SQL Server
- Oracle
- Active Directory

---

# Log Collection

The first stage of SIEM operation is collecting logs.

Logs may be gathered using:

- Agents
- Syslog
- APIs
- File Monitoring
- Cloud Connectors

The objective is to centralize all security-relevant information.

---

# Log Normalization

Different devices produce logs in different formats.

Example:

Firewall:

```text
ALLOW TCP 80
```

Linux:

```text
Accepted password for user
```

Windows:

```text
Event ID 4624
```

A SIEM converts these diverse formats into a standardized structure.

This process is called **Normalization**.

Without normalization, meaningful correlation would be impossible.

---

# Parsing

Parsing extracts useful information from raw logs.

Example:

Raw Log:

```text
User admin logged in from 192.168.1.5
```

Parser extracts:

```text
Username

IP Address

Timestamp

Action
```

This structured information can then be analyzed.

---

# Correlation

Correlation is one of the most important SIEM features.

Instead of analyzing individual logs independently, the SIEM combines multiple related events.

Example:

```text
10 Failed Logins

+

Successful Login

+

New Administrator Created

↓

Possible Brute Force Attack
```

This relationship cannot be identified by examining a single log entry.

---

# Correlation Rules

A correlation rule defines suspicious patterns.

Example:

```text
Condition:

5 Failed Logins

within

2 Minutes

↓

Generate Alert
```

Rules are continuously evaluated against incoming events.

---

# Example Correlation Scenario

Suppose the following events occur:

09:00

```text
Failed Login
```

09:01

```text
Failed Login
```

09:02

```text
Failed Login
```

09:03

```text
Successful Login
```

09:04

```text
Privilege Escalation
```

Individually,

these events may appear harmless.

Together,

they strongly suggest account compromise.

The SIEM detects this pattern and generates an alert.

---

# Alert Generation

When correlation rules are satisfied,

the SIEM generates an alert.

An alert typically contains:

- Timestamp
- Severity
- Source IP
- Destination
- Username
- Rule Triggered
- Description
- MITRE Mapping (if configured)

Alerts are reviewed by SOC analysts.

---

# Dashboards

SIEM dashboards provide real-time visibility into organizational security.

Typical dashboards display:

- Active alerts
- Top attacked hosts
- Authentication failures
- Malware detections
- Geographic attack origins
- Network activity
- User activity
- Threat trends

Dashboards allow analysts to prioritize investigations quickly.

---

# Searching Logs

One of the strengths of a SIEM is rapid log searching.

Example:

Search for:

```text
username = admin
```

or

```text
source.ip = 192.168.1.25
```

Analysts can investigate historical events within seconds.

---

# Reporting

SIEM platforms generate reports for:

- Compliance
- Auditing
- Incident response
- Management
- Security metrics

Examples include:

- Weekly attack summary
- Failed login statistics
- Top malware detections
- User authentication report

---

# Six Core Functions of SIEM

A modern SIEM performs six primary functions.

```text
Collect

↓

Normalize

↓

Store

↓

Correlate

↓

Alert

↓

Visualize
```

These functions work together to provide centralized security monitoring.

---

# SIEM vs Traditional Log Management

| Traditional Log Management | SIEM |
|----------------------------|------|
| Stores logs | Stores logs |
| Manual analysis | Automated analysis |
| No correlation | Event correlation |
| No real-time alerts | Real-time alerts |
| Basic reporting | Advanced dashboards |
| Limited detection | Threat detection |

---

# SIEM vs SOAR

Students often confuse SIEM with SOAR.

## SIEM

Focuses on:

- Collecting
- Detecting
- Alerting

---

## SOAR

Stands for:

```text
Security Orchestration, Automation and Response
```

Focuses on:

- Automating incident response
- Executing playbooks
- Reducing manual effort

Example:

SIEM detects malware.

SOAR automatically:

- Isolates endpoint
- Blocks IP
- Creates ticket
- Notifies analysts

---

# SIEM vs XDR

Another commonly confused technology is XDR.

## XDR

Extended Detection and Response.

Unlike traditional SIEM,

XDR integrates telemetry from:

- Endpoints
- Email
- Network
- Identity
- Cloud

and provides advanced detection and response capabilities.

---

# Popular SIEM Platforms

Examples include:

- Wazuh
- Splunk Enterprise Security
- IBM QRadar
- Microsoft Sentinel
- Elastic Security
- ArcSight
- LogRhythm
- AlienVault OSSIM

The practical portion of this session focuses on **Wazuh**.

---

# Benefits of SIEM

Organizations use SIEM because it provides:

- Centralized visibility
- Faster investigations
- Threat detection
- Regulatory compliance
- Incident response support
- Long-term log storage
- Threat hunting capability

---

# Limitations of SIEM

Although powerful, SIEM is not perfect.

Challenges include:

- Large storage requirements
- Complex rule tuning
- False positives
- False negatives
- Skilled analysts required
- High deployment cost (for some platforms)

Proper tuning significantly improves effectiveness.

---

# Learning Objectives

After completing this section, students should be able to:

- Define SIEM.
- Explain why centralized log collection is necessary.
- Describe the SIEM architecture.
- Explain log normalization and parsing.
- Understand event correlation.
- Differentiate SIEM, SOAR, and XDR.
- Describe the six core functions of a SIEM.

---

# Interview Questions

## What is SIEM?

Security Information and Event Management is a centralized platform used to collect, normalize, correlate, analyze, and visualize security logs to detect and investigate threats.

---

## Why is log normalization important?

Different devices produce logs in different formats. Normalization converts them into a standardized structure so they can be correlated and analyzed consistently.

---

## What is event correlation?

Event correlation combines multiple related events to identify suspicious patterns that would not be apparent when examining individual logs separately.

---

## What is the difference between SIEM and SOAR?

SIEM focuses on log collection, analysis, and alert generation, whereas SOAR automates investigation and incident response using predefined playbooks.

---

## Why is SIEM important for a SOC?

A SOC relies on SIEM to centralize security visibility, detect threats in real time, generate alerts, support investigations, and improve incident response.

---

# Key Takeaways

- SIEM centralizes security logs from multiple data sources.
- Log normalization and parsing transform diverse log formats into structured data.
- Event correlation enables detection of complex attack patterns.
- Dashboards and reports provide real-time visibility into organizational security.
- SIEM serves as the analytical core of a Security Operations Centre.
- Wazuh, Splunk, QRadar, Microsoft Sentinel, and Elastic Security are widely used SIEM platforms.
- SIEM detects threats, while SOAR automates response and XDR extends detection across multiple security domains.

# Session 11 – Defensive Security and the Security Operations Centre (SOC)
## Part 4 – Wazuh Architecture and Components

**Course:** C-DAC Kolkata – Cybersecurity Industry Exposure Program  
**Module:** Wazuh SIEM / XDR Architecture

---

# Introduction to Wazuh

After understanding the purpose of a SIEM, the next topic introduced in the session is **Wazuh**.

Wazuh is an open-source security platform that combines several security capabilities into a single solution.

It provides:

- Security Monitoring
- Log Analysis
- Threat Detection
- File Integrity Monitoring (FIM)
- Vulnerability Detection
- Security Configuration Assessment (SCA)
- Incident Response
- Endpoint Detection and Response (EDR)
- Compliance Monitoring

Unlike traditional antivirus software, Wazuh continuously collects security events from endpoints and analyzes them centrally.

---

# Why Wazuh?

Modern organizations need a security platform that is:

- Open Source
- Scalable
- Centralized
- Flexible
- Easy to integrate
- Cost effective

Wazuh satisfies these requirements while supporting:

- Windows
- Linux
- macOS
- Docker
- Kubernetes
- Cloud Platforms
- Virtual Machines

This makes it suitable for both small organizations and large enterprises.

---

# Wazuh as a SIEM and XDR Platform

Although Wazuh is commonly introduced as a SIEM, it also includes features commonly associated with XDR (Extended Detection and Response).

Wazuh provides:

- Centralized log collection
- Endpoint monitoring
- Threat detection
- Active response
- File integrity monitoring
- Vulnerability assessment

This combination enables organizations to monitor both endpoints and infrastructure from a single platform.

---

# High-Level Wazuh Architecture

The instructor introduced the overall architecture before discussing each component.

```text
             Endpoints

 Windows   Linux   macOS   Cloud

          │
          ▼

     Wazuh Agent

          │

Encrypted Communication

          │
          ▼

     Wazuh Manager

          │
          ▼

      Wazuh Indexer

          │
          ▼

     Wazuh Dashboard

          │
          ▼

      SOC Analysts
```

Each component performs a specific role within the platform.

---

# Major Components

The Wazuh architecture consists of four primary components:

- Wazuh Agent
- Wazuh Manager
- Wazuh Indexer
- Wazuh Dashboard

Understanding the interaction between these components is essential.

---

# Wazuh Agent

## What is a Wazuh Agent?

A Wazuh Agent is software installed on an endpoint that continuously monitors system activity.

The agent acts as the "eyes and ears" of the Wazuh platform.

It collects security-related information and securely sends it to the Wazuh Manager.

---

# Information Collected by the Agent

The agent monitors many aspects of the operating system.

Examples include:

### Authentication Events

- Successful logins
- Failed logins
- Account lockouts
- Password changes

---

### File Activity

- File creation
- File deletion
- File modification
- Permission changes

---

### Process Activity

- Process creation
- Process termination
- Running services

---

### System Information

- Operating system version
- Installed software
- Running applications
- Hostname
- Network interfaces

---

### Security Events

- Malware detections
- Configuration changes
- Policy violations
- Security alerts

---

# Why Install Agents?

Without an agent,

the SIEM has limited visibility into endpoint activity.

With an agent,

the SIEM receives detailed information directly from the endpoint.

```text
Without Agent

Limited Visibility

↓

Firewall Logs Only

----------------------------

With Agent

Complete Endpoint Visibility

↓

Files

Processes

Users

Authentication

System Events
```

---

# Wazuh Manager

## What is the Manager?

The Wazuh Manager is the central processing component of the platform.

It receives events from all connected agents.

Its responsibilities include:

- Log processing
- Rule evaluation
- Threat detection
- Alert generation
- Agent management

The manager acts as the "brain" of the system.

---

# Functions of the Manager

The manager performs several operations.

```text
Receive Events

↓

Decode Logs

↓

Normalize Data

↓

Apply Rules

↓

Correlate Events

↓

Generate Alerts

↓

Forward Results
```

The manager determines whether an event is benign or suspicious.

---

# Agent Registration

Before communication begins,

an endpoint must register with the manager.

General workflow:

```text
Install Agent

↓

Register Agent

↓

Authentication

↓

Secure Connection

↓

Begin Monitoring
```

Only authorized agents should communicate with the manager.

---

# Secure Communication

Communication between agents and the manager is encrypted.

This protects:

- Log data
- Credentials
- Authentication information

Encryption prevents attackers from modifying or reading transmitted events.

---

# Wazuh Indexer

## Purpose

The Indexer stores processed security events.

Think of the Indexer as the database of the Wazuh platform.

Responsibilities include:

- Storing alerts
- Indexing logs
- Fast searching
- Historical analysis

Without indexing,

searching millions of logs would be extremely slow.

---

# Why Indexing?

Suppose an analyst searches for:

```text
Failed Login

Past 30 Days
```

Instead of scanning every log sequentially,

the index allows rapid retrieval.

Benefits:

- Faster searches
- Better scalability
- Improved reporting

---

# Wazuh Dashboard

The Dashboard is the graphical interface used by SOC analysts.

It provides:

- Alert visualization
- Search functionality
- Dashboards
- Reports
- Rule management
- Agent status
- Security metrics

The dashboard converts technical log data into meaningful visualizations.

---

# Dashboard Features

Typical dashboard widgets include:

- Alert count
- Active agents
- Failed logins
- Malware detections
- Top attacked systems
- File modifications
- Compliance status
- MITRE ATT&CK mappings

This helps analysts understand organizational security at a glance.

---

# End-to-End Data Flow

The complete Wazuh workflow is:

```text
Endpoint Activity

↓

Agent Collects Data

↓

Encrypted Transmission

↓

Manager Processes Events

↓

Rules Applied

↓

Alerts Generated

↓

Indexer Stores Results

↓

Dashboard Displays Alerts

↓

SOC Analyst Investigates
```

Every event follows this pipeline.

---

# Wazuh Rules

Rules determine whether an event should generate an alert.

Example:

```text
5 Failed Login Attempts

↓

Rule Triggered

↓

Generate Alert
```

Rules contain:

- Conditions
- Severity
- Description
- MITRE Mapping
- Response Actions

Rule tuning is critical to reducing false positives.

---

# Decoders

Different devices generate logs in different formats.

Decoders interpret these formats.

Example:

Raw Log:

```text
Jul 08 sshd Failed password for admin
```

Decoder extracts:

```text
Timestamp

Service

Username

Action
```

Decoded data is easier to analyze.

---

# Alerts

When rules match decoded events,

alerts are generated.

An alert typically contains:

- Rule ID
- Severity
- Timestamp
- Hostname
- Source IP
- Description
- MITRE Technique

Alerts become visible in the Dashboard.

---

# Severity Levels

Wazuh assigns severity levels to alerts.

Lower levels indicate informational events.

Higher levels indicate potentially dangerous activity.

Example progression:

```text
Level 3

Information

↓

Level 7

Suspicious Activity

↓

Level 12

High Risk

↓

Level 15

Critical Security Incident
```

Analysts prioritize investigations based on severity.

---

# Scalability

Wazuh supports environments ranging from:

Small Business

↓

Medium Enterprise

↓

Large Enterprise

↓

Cloud Infrastructure

↓

Hybrid Networks

Multiple managers and indexers can be deployed to improve scalability and availability.

---

# Advantages of Wazuh

Advantages include:

- Open source
- Active community
- Cross-platform support
- SIEM capabilities
- XDR functionality
- File Integrity Monitoring
- Vulnerability Detection
- Compliance Monitoring
- MITRE ATT&CK integration
- Active Response

---

# Limitations

Like any security platform,

Wazuh has limitations.

Examples include:

- Requires proper configuration
- Rule tuning needed
- Storage requirements increase with log volume
- Analysts must understand alerts
- False positives may occur if rules are not optimized

---

# Learning Objectives

After completing this section, students should be able to:

- Explain the purpose of Wazuh.
- Identify the four primary Wazuh components.
- Describe the responsibilities of the Agent, Manager, Indexer, and Dashboard.
- Explain how logs flow through the Wazuh architecture.
- Understand the roles of decoders, rules, and alerts.
- Explain why centralized endpoint monitoring is important.

---

# Interview Questions

## What is Wazuh?

Wazuh is an open-source security platform that provides SIEM and XDR capabilities, including log analysis, threat detection, file integrity monitoring, vulnerability detection, and incident response.

---

## What is the role of the Wazuh Agent?

The Wazuh Agent collects security-related information from endpoints and securely sends it to the Wazuh Manager.

---

## What is the responsibility of the Wazuh Manager?

The Manager processes incoming events, applies decoders and rules, detects suspicious activity, generates alerts, and manages connected agents.

---

## Why is the Indexer important?

The Indexer stores processed events in an optimized format, enabling fast searches, reporting, and historical analysis.

---

## What is the purpose of the Dashboard?

The Dashboard provides a graphical interface that allows SOC analysts to monitor alerts, search logs, visualize trends, manage agents, and investigate incidents.

---

## What is a Decoder in Wazuh?

A Decoder interprets raw log formats from different systems and extracts structured fields such as timestamps, usernames, services, and actions.

---

## Why are Rules important?

Rules evaluate decoded events and determine whether an alert should be generated based on predefined detection logic.

---

# Key Takeaways

- Wazuh is an open-source SIEM/XDR platform designed for centralized security monitoring.
- The architecture consists of four primary components: Agent, Manager, Indexer, and Dashboard.
- Agents collect endpoint telemetry, while the Manager processes events using decoders and rules.
- The Indexer stores searchable security data, and the Dashboard provides visualization for SOC analysts.
- Rules and decoders form the foundation of threat detection within Wazuh.
- Proper deployment and tuning enable organizations to detect, investigate, and respond to security events efficiently.

# Session 11 – Defensive Security and the Security Operations Centre (SOC)
## Part 5 – Log Analysis, Event Processing and Threat Detection in Wazuh

**Course:** C-DAC Kolkata – Cybersecurity Industry Exposure Program  
**Module:** Defensive Security & Wazuh SIEM

---

# Introduction

A Security Information and Event Management (SIEM) platform is only as effective as the logs it receives.

The instructor emphasized that:

> **"Everything that happens inside a computer leaves evidence."**

Whether a user logs in, a file is modified, malware executes, or an attacker scans a network, some form of event is generated.

These events are recorded as **logs**.

The responsibility of a SOC analyst is to transform these raw logs into actionable security intelligence.

This process involves:

```text
Log Collection

↓

Log Decoding

↓

Normalization

↓

Rule Matching

↓

Correlation

↓

Alert Generation

↓

Incident Investigation
```

---

# What is a Log?

A **log** is a chronological record of an event generated by a system, application, or network device.

Logs act as the "black box" of a computer system.

They record:

- What happened
- When it happened
- Where it happened
- Who performed the action
- Whether the action succeeded or failed

Without logs, forensic investigations would be nearly impossible.

---

# Why are Logs Important?

Logs serve multiple purposes.

## Security Monitoring

Detect attacks and suspicious behaviour.

Example:

```text
Multiple failed login attempts
```

---

## Troubleshooting

Identify application failures or configuration issues.

Example:

```text
Database connection failed
```

---

## Compliance

Meet regulatory requirements such as:

- ISO 27001
- PCI DSS
- HIPAA
- GDPR

Many regulations require retaining logs for months or years.

---

## Digital Forensics

Investigators use logs to reconstruct attack timelines.

Example:

```text
Initial Login

↓

Privilege Escalation

↓

Malware Execution

↓

Data Exfiltration
```

---

# Characteristics of a Good Log

A useful security log should include:

- Timestamp
- Username
- Hostname
- Source IP
- Destination IP
- Event Description
- Event ID
- Severity
- Status (Success / Failure)

The more context available, the easier it becomes to investigate incidents.

---

# Types of Logs

Organizations collect logs from many different sources.

---

# 1. Authentication Logs

Authentication logs record user login activity.

Examples include:

- Successful logins
- Failed logins
- Password changes
- Account lockouts
- Account creation
- Privilege changes

Example:

```text
User: admin

Action: Failed Login

Source IP: 192.168.1.10

Time: 10:15 AM
```

Authentication logs are essential for detecting brute-force attacks.

---

# 2. System Logs

System logs record operating system activity.

Examples:

- Boot events
- Shutdown events
- Driver loading
- Kernel messages
- Service startup
- System errors

These logs help detect:

- Crashes
- Unauthorized service installation
- System instability

---

# 3. Application Logs

Applications generate their own logs.

Examples:

- Apache
- Nginx
- MySQL
- PostgreSQL
- IIS
- Docker

Application logs help identify:

- SQL Injection
- Web attacks
- Application crashes
- Authentication failures

---

# 4. Firewall Logs

Firewalls record network traffic decisions.

Example:

```text
ALLOW

TCP

192.168.1.5

→

10.10.10.25

Port 443
```

or

```text
DENY

TCP

203.10.11.20

→

192.168.1.5

Port 22
```

Firewall logs help detect:

- Port scans
- Unauthorized access attempts
- Suspicious outbound traffic

---

# 5. Web Server Logs

Web servers record HTTP requests.

Typical information includes:

- Client IP
- Requested URL
- HTTP Method
- Status Code
- User Agent
- Timestamp

Example:

```text
GET /login

200 OK
```

or

```text
POST /admin.php

403 Forbidden
```

These logs are useful for detecting:

- Directory traversal
- SQL Injection
- Brute-force attacks
- Web shell activity

---

# 6. Endpoint Logs

Endpoint logs record activities on user devices.

Examples:

- File creation
- USB insertion
- Process creation
- Antivirus detection
- Registry modifications
- Software installation

Endpoint logs are central to Endpoint Detection and Response (EDR).

---

# Log Collection in Wazuh

The Wazuh Agent continuously collects logs from monitored systems.

Example flow:

```text
Windows Event Logs

↓

Linux Syslog

↓

Apache Logs

↓

Authentication Logs

↓

Wazuh Agent
```

The collected data is securely transmitted to the Wazuh Manager.

---

# Raw Logs

Initially, logs are unstructured.

Example:

```text
Jul 08 09:20 sshd Failed password for admin from 192.168.1.20
```

Although humans can interpret this message, computers require a structured format for efficient analysis.

---

# Decoders

Decoders convert raw log entries into structured data.

Example:

Raw Log:

```text
Jul 08 09:20 sshd Failed password for admin from 192.168.1.20
```

Decoded Fields:

```text
Timestamp : Jul 08 09:20

Service : sshd

Action : Failed Password

Username : admin

Source IP : 192.168.1.20
```

Decoding makes logs searchable and suitable for rule evaluation.

---

# Normalization

Different operating systems and applications generate logs in different formats.

Normalization converts these different formats into a common structure.

Example:

Linux:

```text
Accepted password
```

Windows:

```text
Event ID 4624
```

After normalization:

```text
Authentication Success
```

The SIEM can now apply the same detection rules across different operating systems.

---

# Rules

Rules define suspicious conditions.

Examples:

Rule:

```text
More than 5 failed logins

within

60 seconds
```

If the condition is met:

```text
Generate Alert
```

Rules are the intelligence layer of a SIEM.

---

# Rule Matching Process

The Wazuh Manager processes every incoming log using the following sequence:

```text
Receive Log

↓

Decode Log

↓

Normalize Data

↓

Compare Against Rules

↓

Rule Matched?

↓

Yes

↓

Generate Alert

↓

Store Alert

↓

Display on Dashboard
```

If no rule matches, the event is stored but no alert is generated.

---

# Alert Generation

When a rule matches, Wazuh generates an alert containing:

- Alert ID
- Rule ID
- Severity
- Hostname
- Timestamp
- Description
- Source IP
- MITRE ATT&CK Technique (if mapped)

These alerts appear immediately on the SOC dashboard.

---

# Alert Severity Levels

Alerts are assigned severity levels to help analysts prioritize investigations.

Typical interpretation:

| Level | Meaning |
|--------|---------|
| 0–3 | Informational |
| 4–6 | Low Risk |
| 7–9 | Medium Risk |
| 10–12 | High Risk |
| 13–15 | Critical |

Higher severity alerts require immediate attention.

---

# Example: SSH Brute Force Detection

Consider the following sequence of events:

```text
09:00

Failed Login

↓

09:01

Failed Login

↓

09:02

Failed Login

↓

09:03

Failed Login

↓

09:04

Failed Login
```

The corresponding Wazuh rule detects:

```text
Five failed logins within a short period
```

Result:

```text
High Severity Alert
```

The SOC analyst investigates to determine whether the activity is malicious or simply a user entering an incorrect password.

---

# False Positives

A **False Positive** occurs when legitimate activity is incorrectly classified as malicious.

Example:

A user repeatedly mistypes their password.

The SIEM generates a brute-force alert.

Investigation reveals:

```text
Legitimate User

↓

Forgot Password

↓

No Attack
```

Although no attack occurred, the alert was generated.

---

# False Negatives

A **False Negative** occurs when malicious activity is not detected.

Example:

An attacker successfully compromises a system, but no alert is generated.

False negatives are more dangerous than false positives because attacks remain unnoticed.

---

# Rule Tuning

SOC analysts continuously refine detection rules to:

- Reduce false positives
- Improve detection accuracy
- Minimize unnecessary alerts

This process is known as **Rule Tuning**.

Effective tuning improves analyst productivity and reduces alert fatigue.

---

# Alert Fatigue

Large organizations may generate thousands of alerts daily.

Example:

```text
20,000 Alerts

↓

Only 15 Real Incidents
```

If analysts investigate every alert manually, important incidents may be missed.

Proper rule tuning and correlation help reduce alert fatigue.

---

# Correlation Example

Suppose Wazuh receives the following events:

```text
Failed Login

↓

Failed Login

↓

Successful Login

↓

New Administrator Account Created

↓

Large File Download
```

Individually, each event may appear normal.

Together, they suggest possible account compromise.

Correlation enables Wazuh to identify this attack chain.

---

# Learning Objectives

After completing this section, students should be able to:

- Explain the importance of logs in cybersecurity.
- Identify different categories of security logs.
- Describe the Wazuh log processing pipeline.
- Explain the purpose of decoders, normalization, and rules.
- Understand how alerts are generated.
- Differentiate between false positives and false negatives.
- Explain why rule tuning is essential for SOC operations.

---

# Interview Questions

## What is a security log?

A security log is a chronological record of events generated by systems, applications, or network devices that provides evidence of system activity.

---

## Why are decoders required in Wazuh?

Decoders convert raw log entries into structured fields, allowing rules to analyze events consistently across different log formats.

---

## What is the purpose of normalization?

Normalization standardizes logs from different operating systems and applications into a common format for efficient correlation and analysis.

---

## What is a false positive?

A false positive occurs when legitimate activity is incorrectly identified as malicious.

---

## What is a false negative?

A false negative occurs when malicious activity is not detected by the security monitoring system.

---

## Why is rule tuning important?

Rule tuning reduces false positives, improves detection accuracy, minimizes alert fatigue, and enables analysts to focus on genuine security incidents.

---

# Key Takeaways

- Every action performed on a system generates logs that serve as evidence for security monitoring and investigations.
- Wazuh processes logs through decoding, normalization, rule evaluation, and alert generation.
- Different log types provide visibility into authentication, systems, applications, firewalls, and endpoints.
- Effective rule tuning and event correlation improve threat detection while reducing false positives.
- Log analysis forms the foundation of every Security Operations Centre and enables timely detection of malicious activity.

# Session 11 – Defensive Security and the Security Operations Centre (SOC)
## Part 6 – File Integrity Monitoring (FIM), Syscheck and Vulnerability Detection

**Course:** C-DAC Kolkata – Cybersecurity Industry Exposure Program  
**Module:** Wazuh SIEM / XDR

---

# Introduction

Traditional security monitoring primarily focuses on:

- Network traffic
- Authentication logs
- Firewall events
- Process execution

However, attackers often attempt to modify important system files after gaining access.

Examples include:

- Replacing system binaries
- Installing web shells
- Modifying configuration files
- Changing startup scripts
- Editing scheduled tasks
- Altering registry entries (Windows)

Many of these modifications may not immediately generate obvious alerts.

To detect such changes, Wazuh provides **File Integrity Monitoring (FIM).**

---

# What is File Integrity Monitoring (FIM)?

File Integrity Monitoring (FIM) is a security mechanism that continuously monitors files and directories for unauthorized modifications.

Instead of simply checking whether a file exists, FIM detects:

- File creation
- File deletion
- File modification
- Permission changes
- Ownership changes
- Attribute changes
- Hash changes

The objective is to determine whether critical files have been altered.

---

# Why File Integrity Monitoring is Important

Attackers rarely leave systems unchanged after compromising them.

They often modify files to:

- Maintain persistence
- Hide malicious code
- Replace legitimate applications
- Install malware
- Create administrator accounts
- Disable security software

Without file monitoring, these modifications may remain unnoticed for long periods.

---

# Security Principle

One of the core principles discussed is:

> **Critical files should never change unexpectedly.**

If they do,

the change should be investigated immediately.

---

# How FIM Works

The File Integrity Monitoring process follows these steps.

```text
Initial Scan

↓

Create Baseline

↓

Store File Metadata

↓

Monitor Files

↓

Compare Current State

↓

Detect Changes

↓

Generate Alert
```

The "baseline" is extremely important.

---

# What is a Baseline?

A baseline represents the known-good state of a system.

When Wazuh first scans a directory, it records:

- Filename
- File size
- Permissions
- Owner
- Timestamp
- Cryptographic hash

Example:

```text
/etc/passwd

Hash

SHA256:

A4D9...

Owner:

root

Permissions:

644
```

Future scans compare the current file against this baseline.

---

# What Does Wazuh Compare?

During every scan,

Wazuh compares:

- File name
- File size
- Last modification time
- Owner
- Group
- Permissions
- SHA1 Hash
- SHA256 Hash
- MD5 Hash (if enabled)

Even if only one attribute changes,

the system detects the modification.

---

# Cryptographic Hashes

Instead of comparing entire files,

Wazuh uses cryptographic hashes.

Example:

```text
File

↓

SHA256

↓

8F52A1...
```

If even one byte changes,

the resulting hash changes completely.

This makes hashes extremely reliable for integrity verification.

---

# Example

Original file:

```text
Hello World
```

SHA256:

```text
A591A6...
```

Modified file:

```text
Hello World!
```

New SHA256:

```text
DFFD60...
```

Although only one character changed,

the hash is completely different.

---

# Syscheck

The File Integrity Monitoring module in Wazuh is called:

```text
Syscheck
```

Syscheck is responsible for:

- Initial scanning
- Baseline creation
- Continuous monitoring
- Integrity verification
- Alert generation

---

# How Syscheck Works

```text
Critical Directory

↓

Scan Files

↓

Calculate Hashes

↓

Store Baseline

↓

Periodic Scan

↓

Compare Hashes

↓

Generate Alert
```

---

# Directories Commonly Monitored

Linux:

```text
/etc

/bin

/usr/bin

/boot

/root
```

Windows:

```text
C:\Windows

C:\Windows\System32

Program Files

Registry
```

Web Servers:

```text
/var/www

/var/www/html
```

These locations contain critical operating system and application files.

---

# Example Scenario

Suppose an attacker compromises a Linux web server.

They upload:

```text
shell.php
```

Location:

```text
/var/www/html/
```

Syscheck performs its next scan.

It notices:

```text
New File Detected
```

↓

Alert Generated

↓

SOC Analyst Investigates

---

# Detecting File Modification

Suppose an attacker modifies:

```text
/etc/passwd
```

Original Hash:

```text
ABC123...
```

Current Hash:

```text
XYZ789...
```

Result:

```text
Integrity Violation

↓

High Severity Alert
```

---

# Detecting File Deletion

Deletion can also indicate malicious activity.

Example:

Attacker deletes:

```text
audit.log
```

Next scan:

```text
Expected File Missing
```

↓

Alert Generated

---

# Detecting Permission Changes

Attackers often modify file permissions.

Example:

Original:

```text
644
```

Modified:

```text
777
```

Result:

```text
Permission Changed

↓

Alert
```

Unexpected permission changes should always be investigated.

---

# Detecting Ownership Changes

Changing ownership may allow attackers to maintain persistence.

Example:

Original Owner:

```text
root
```

Modified Owner:

```text
attacker
```

↓

Alert Generated

---

# Web Shell Detection

One practical example discussed is web shell detection.

A web shell is a malicious script uploaded to a compromised web server.

Examples:

```text
shell.php

cmd.php

upload.php
```

Once uploaded,

the attacker can execute commands remotely.

File Integrity Monitoring detects these unexpected files.

---

# Malware Detection

Malware often modifies:

- Executables
- DLL files
- Startup scripts
- Scheduled tasks
- Registry entries

FIM identifies these modifications before the malware becomes fully established.

---

# Insider Threat Detection

Not every attack comes from outside.

Employees may intentionally or accidentally modify sensitive files.

Example:

```text
Financial Report

↓

Unauthorized Modification

↓

FIM Alert
```

This enables organizations to detect insider threats.

---

# Compliance

Many security standards require File Integrity Monitoring.

Examples:

- PCI DSS
- HIPAA
- ISO 27001
- NIST

FIM assists organizations in meeting these compliance requirements.

---

# Vulnerability Detection in Wazuh

In addition to File Integrity Monitoring,

Wazuh also performs vulnerability detection.

Instead of monitoring files,

it analyzes:

- Installed software
- Package versions
- Operating system versions

The detected versions are compared against known vulnerability databases.

---

# Vulnerability Detection Workflow

```text
Installed Packages

↓

Collect Version Information

↓

Compare with CVE Database

↓

Known Vulnerability?

↓

Yes

↓

Generate Alert
```

---

# Example

Installed Software:

```text
Apache 2.4.49
```

Known CVE:

```text
Remote Code Execution
```

Result:

```text
Vulnerability Detected

↓

Alert
```

The SOC analyst can now recommend patching.

---

# Advantages of Vulnerability Detection

It enables organizations to:

- Discover outdated software
- Identify known CVEs
- Prioritize patching
- Reduce attack surface
- Improve compliance

---

# Difference Between FIM and Vulnerability Detection

| File Integrity Monitoring | Vulnerability Detection |
|---------------------------|-------------------------|
| Detects file changes | Detects vulnerable software |
| Compares hashes | Compares software versions |
| Focuses on integrity | Focuses on weaknesses |
| Detects unauthorized modifications | Detects missing patches |

Both modules complement each other.

---

# Investigation Workflow

When an alert is generated,

the SOC analyst should determine:

```text
Who changed the file?

↓

When was it modified?

↓

Why was it changed?

↓

Was the change authorized?

↓

Does malware exist?

↓

Should Incident Response begin?
```

---

# Best Practices

Monitor:

- Operating system files
- Configuration files
- Application directories
- Web directories
- Registry
- Startup folders

Avoid monitoring:

- Temporary files
- Browser cache
- Frequently changing log files

This reduces unnecessary alerts.

---

# Learning Objectives

After completing this section, students should be able to:

- Explain File Integrity Monitoring.
- Describe the role of Syscheck.
- Understand baseline creation.
- Explain how cryptographic hashes detect file modifications.
- Describe web shell detection using FIM.
- Differentiate File Integrity Monitoring from Vulnerability Detection.
- Explain why integrity monitoring is important for incident detection.

---

# Interview Questions

## What is File Integrity Monitoring?

File Integrity Monitoring is the continuous monitoring of files and directories to detect unauthorized creation, deletion, modification, or permission changes.

---

## What is Syscheck?

Syscheck is the Wazuh module responsible for File Integrity Monitoring.

---

## Why are cryptographic hashes used?

Hashes uniquely represent file contents. Even a one-byte modification produces a completely different hash, allowing accurate integrity verification.

---

## What is a baseline?

A baseline is the known-good state of monitored files recorded during the initial scan and used for future comparisons.

---

## How can FIM detect web shells?

When an attacker uploads an unexpected file (such as `shell.php`) into a monitored directory, Wazuh detects the new file and generates an alert.

---

## What is the difference between File Integrity Monitoring and Vulnerability Detection?

File Integrity Monitoring detects unauthorized file changes, whereas Vulnerability Detection identifies outdated software versions with known security vulnerabilities.

---

# Key Takeaways

- File Integrity Monitoring detects unauthorized changes to critical files and directories.
- Wazuh implements FIM through the **Syscheck** module.
- Baselines and cryptographic hashes enable reliable integrity verification.
- FIM helps detect malware, web shells, insider threats, and persistence mechanisms.
- Vulnerability Detection complements FIM by identifying outdated software with known CVEs.
- Together, these capabilities significantly improve an organization's ability to detect and respond to security threats.


# Session 11 – Defensive Security and the Security Operations Centre (SOC)
## Part 7 – MITRE ATT&CK Framework Integration in Wazuh

**Course:** C-DAC Kolkata – Cybersecurity Industry Exposure Program  
**Module:** Defensive Security, Threat Detection and MITRE ATT&CK

---

# Introduction

Detecting an attack is only the first step in incident response.

A SOC analyst must also answer questions such as:

- What exactly is the attacker trying to achieve?
- Which phase of the attack are we observing?
- Which technique is being used?
- Has this attack been seen before?
- What should we investigate next?

To answer these questions consistently across organizations, the cybersecurity community uses the **MITRE ATT&CK Framework**.

Modern SIEM platforms, including Wazuh, map alerts to MITRE ATT&CK techniques so analysts immediately understand where an attacker is in the attack lifecycle.

---

# What is MITRE?

MITRE is a non-profit organization that conducts research in cybersecurity, defense, healthcare, aviation, and many other domains.

One of its most important cybersecurity contributions is the **MITRE ATT&CK Framework**.

MITRE does **not** create malware.

Instead, it documents how real-world attackers behave.

---

# What is MITRE ATT&CK?

MITRE ATT&CK stands for:

```text
Adversarial Tactics, Techniques,
and Common Knowledge
```

It is a publicly available knowledge base that documents attacker behaviour observed in real-world cyber attacks.

Instead of focusing on vulnerabilities,

MITRE focuses on:

- Attacker objectives
- Attacker techniques
- Attacker procedures

---

# Purpose of MITRE ATT&CK

MITRE ATT&CK helps organizations:

- Understand attacker behaviour
- Build better detection rules
- Improve SOC investigations
- Map alerts to known attack techniques
- Perform threat hunting
- Improve Purple Team exercises

Rather than simply saying:

```text
SSH Brute Force Detected
```

the SOC can immediately map the activity to:

```text
Credential Access

↓

Brute Force

↓

MITRE Technique T1110
```

---

# ATT&CK Matrix

The ATT&CK Matrix organizes attacker behaviour into:

```text
Tactics

↓

Techniques

↓

Sub-techniques
```

Each level provides increasing detail.

---

# What is a Tactic?

A tactic describes the **goal** or **objective** of an attacker.

Examples:

- Initial Access
- Execution
- Persistence
- Privilege Escalation
- Defense Evasion
- Credential Access
- Discovery
- Lateral Movement
- Collection
- Exfiltration
- Impact

Think of tactics as answering:

> **What is the attacker trying to accomplish?**

---

# What is a Technique?

A technique describes **how** the attacker achieves a tactic.

Example:

Tactic:

```text
Credential Access
```

Technique:

```text
Brute Force
```

Another example:

Tactic:

```text
Persistence
```

Technique:

```text
Scheduled Task
```

---

# What is a Sub-Technique?

Some techniques are further divided into more specific attack methods.

Example:

Technique:

```text
Brute Force
```

Sub-techniques may include:

- Password Guessing
- Password Spraying
- Credential Stuffing

Sub-techniques provide greater analytical detail.

---

# MITRE ATT&CK Structure

```text
Tactic

↓

Technique

↓

Sub-Technique
```

Example:

```text
Credential Access

↓

Brute Force

↓

Password Guessing
```

---

# ATT&CK Tactics

The Enterprise ATT&CK Matrix currently includes tactics such as:

```text
Reconnaissance

↓

Resource Development

↓

Initial Access

↓

Execution

↓

Persistence

↓

Privilege Escalation

↓

Defense Evasion

↓

Credential Access

↓

Discovery

↓

Lateral Movement

↓

Collection

↓

Command and Control

↓

Exfiltration

↓

Impact
```

These tactics collectively describe the lifecycle of an attack.

---

# Example Attack Chain

Consider a ransomware attack.

```text
Phishing Email

↓

User Opens Attachment

↓

Malware Executes

↓

Persistence Created

↓

Credentials Stolen

↓

Administrator Privileges

↓

Lateral Movement

↓

File Encryption
```

Each step maps to one or more ATT&CK tactics and techniques.

---

# Why SOC Analysts Use MITRE

MITRE provides a common language.

Instead of saying:

```text
Something suspicious happened.
```

An analyst can state:

```text
Technique T1110

Brute Force

Credential Access
```

Every security professional understands exactly what this means.

---

# MITRE Mapping in Wazuh

One of Wazuh's strengths is automatic MITRE mapping.

When a detection rule matches,

Wazuh can associate it with:

- MITRE Tactic
- MITRE Technique
- Technique ID

This appears directly in the dashboard.

---

# Example

Suppose Wazuh detects repeated SSH login failures.

Rule triggers.

Dashboard displays:

```text
Technique

T1110

↓

Brute Force

↓

Credential Access
```

The analyst immediately understands the attacker's objective.

---

# SSH Brute Force Example

Attack:

```text
Attacker

↓

SSH Login

↓

Wrong Password

↓

Wrong Password

↓

Wrong Password

↓

Correct Password
```

Logs Generated:

```text
Authentication Failure

↓

Authentication Failure

↓

Authentication Failure

↓

Authentication Success
```

Wazuh Rule:

```text
Multiple Failed Logins

↓

Alert
```

MITRE Mapping:

```text
Credential Access

↓

Brute Force

↓

T1110
```

---

# Why Mapping Matters

Without MITRE:

```text
Alert Generated
```

With MITRE:

```text
Alert

↓

Attack Objective

↓

Technique

↓

Possible Next Steps

↓

Recommended Investigation
```

Analysts gain immediate context.

---

# Threat Hunting

MITRE ATT&CK is widely used for threat hunting.

Threat hunting differs from traditional monitoring.

Traditional monitoring:

```text
Alert

↓

Investigate
```

Threat hunting:

```text
No Alert

↓

Search for Hidden Attacker Activity
```

Analysts proactively search for attacker behaviours.

---

# Coverage Analysis

Organizations often ask:

> **Can we detect every ATT&CK technique?**

Usually,

the answer is **no**.

SOC teams therefore perform:

```text
ATT&CK Coverage Analysis
```

This identifies:

- Detectable techniques
- Missing detections
- Monitoring gaps

Improving coverage strengthens the SOC.

---

# Purple Team Exercises

Purple Teaming commonly uses MITRE ATT&CK.

Workflow:

```text
Red Team

↓

Simulate Technique

↓

Blue Team

↓

Verify Detection

↓

Improve Rule

↓

Repeat
```

The objective is continuous improvement rather than competition.

---

# ATT&CK and Incident Response

Suppose a SOC analyst observes:

```text
PowerShell Execution

↓

Credential Dumping

↓

New Service Created

↓

Remote Desktop Connection
```

Using ATT&CK,

the analyst can reconstruct the attack sequence and predict likely attacker objectives.

This improves response efficiency.

---

# MITRE IDs

Each technique has a unique identifier.

Examples:

| Technique | MITRE ID |
|------------|-----------|
| Brute Force | T1110 |
| PowerShell | T1059 |
| Command Shell | T1059.003 |
| Scheduled Task | T1053 |
| Remote Services | T1021 |
| Credential Dumping | T1003 |

These IDs are commonly referenced in SOC reports.

---

# Benefits of MITRE Integration

MITRE integration provides:

- Standard terminology
- Better investigations
- Improved reporting
- Faster analyst training
- Better rule creation
- Threat hunting support
- Purple Team collaboration

---

# Limitations

MITRE ATT&CK:

- Does not prevent attacks.
- Does not detect attacks by itself.
- Is not a vulnerability scanner.

Instead,

it provides a framework for understanding attacker behaviour.

Detection still depends on tools such as:

- Wazuh
- Splunk
- Microsoft Sentinel
- QRadar
- Elastic Security

---

# Learning Objectives

After completing this section, students should be able to:

- Explain the purpose of the MITRE ATT&CK Framework.
- Differentiate tactics, techniques, and sub-techniques.
- Describe how Wazuh maps alerts to ATT&CK techniques.
- Explain why ATT&CK is useful for SOC analysts.
- Understand how ATT&CK supports threat hunting and Purple Team exercises.

---

# Interview Questions

## What is the MITRE ATT&CK Framework?

The MITRE ATT&CK Framework is a publicly available knowledge base that documents real-world attacker behaviour using tactics, techniques, and procedures.

---

## What is the difference between a tactic and a technique?

A tactic represents the attacker's objective, while a technique describes the method used to achieve that objective.

---

## Why does Wazuh integrate with MITRE ATT&CK?

Wazuh maps alerts to ATT&CK techniques to provide analysts with standardized context about attacker behaviour, enabling faster investigation and response.

---

## What is threat hunting?

Threat hunting is the proactive search for hidden attacker activity that may not have generated automated alerts.

---

## Why is MITRE ATT&CK important for Purple Teams?

It provides a common framework that allows Red Teams and Blue Teams to validate detections, improve monitoring, and strengthen organizational security.

---

# Key Takeaways

- MITRE ATT&CK is a standardized framework for describing attacker behaviour.
- The framework organizes attacks into tactics, techniques, and sub-techniques.
- Wazuh enriches alerts by automatically mapping them to MITRE ATT&CK techniques.
- MITRE integration improves investigations, reporting, threat hunting, and Purple Team collaboration.
- Understanding ATT&CK enables SOC analysts to move beyond individual alerts and reconstruct complete attack chains.


# Session 11 – Defensive Security and the Security Operations Centre (SOC)
## Part 8 – Incident Response Lifecycle and Security Incident Handling

**Course:** C-DAC Kolkata – Cybersecurity Industry Exposure Program  
**Module:** Incident Response, Wazuh Active Response and SOC Operations

---

# Introduction

Detecting an attack is only one part of cybersecurity.

A Security Operations Centre (SOC) becomes valuable only when it can **respond quickly and effectively** after detecting suspicious activity.

This process is known as **Incident Response (IR).**

An Incident Response process provides a structured methodology for:

- Detecting attacks
- Limiting damage
- Preserving evidence
- Restoring business operations
- Preventing future incidents

Without an Incident Response process, organizations may:

- Respond too slowly
- Destroy forensic evidence
- Allow attackers to remain inside the network
- Increase financial loss
- Damage customer trust

---

# What is an Incident?

A **security incident** is any event that compromises, or has the potential to compromise, the:

- Confidentiality
- Integrity
- Availability

of information or information systems.

Examples include:

- Malware infection
- Ransomware attack
- Data breach
- Unauthorized access
- Privilege escalation
- Insider threat
- Denial-of-Service attack
- Web application compromise

Not every alert is an incident.

An incident is confirmed after investigation.

---

# Event vs Alert vs Incident

One of the most important concepts for SOC analysts is understanding the relationship between events, alerts, and incidents.

```text
Event

↓

Alert

↓

Investigation

↓

Incident

↓

Response
```

### Event

Something happened.

Example:

```text
User Login
```

---

### Alert

The SIEM believes something suspicious happened.

Example:

```text
20 Failed Login Attempts
```

---

### Incident

The analyst confirms malicious activity.

Example:

```text
Confirmed SSH Brute Force Attack
```

---

# Why Incident Response is Important

A rapid response helps organizations:

- Minimize downtime
- Reduce financial loss
- Prevent data theft
- Stop malware spread
- Preserve evidence
- Meet compliance requirements
- Improve customer trust

---

# NIST Incident Response Lifecycle

The instructor introduced the widely accepted **NIST Incident Response Lifecycle**.

It consists of six phases.

```text
Preparation

↓

Detection & Analysis

↓

Containment

↓

Eradication

↓

Recovery

↓

Lessons Learned
```

This lifecycle forms the basis of most enterprise Incident Response programs.

---

# Phase 1 – Preparation

Preparation occurs **before** an attack happens.

The organization prepares people, processes, and technology.

Examples include:

- Security policies
- Incident Response Plan
- Asset inventory
- Backup strategy
- Logging
- SIEM deployment
- Security awareness training
- Playbooks
- Communication procedures

Preparation determines how effectively an organization responds later.

---

# Preparation Checklist

Examples:

✔ Security monitoring enabled

✔ Backup available

✔ Logs collected

✔ Incident Response team identified

✔ Contact information documented

✔ Escalation process defined

✔ Detection rules configured

---

# Phase 2 – Detection and Analysis

This phase begins when suspicious activity is detected.

Possible detection sources:

- SIEM
- Antivirus
- EDR
- IDS
- Firewall
- User reports
- Threat Intelligence

SOC analysts investigate:

- Is this malicious?
- Which systems are affected?
- How serious is it?
- Is immediate containment required?

---

# Detection Workflow

```text
Logs

↓

Correlation

↓

Alert

↓

SOC Investigation

↓

Incident Confirmed
```

---

# Indicators of Compromise (IoCs)

During analysis, analysts search for **Indicators of Compromise (IoCs).**

Examples:

- Malicious IP Address
- Malicious Domain
- Suspicious Hash
- Registry Modification
- New Administrator Account
- Unknown Scheduled Task
- Web Shell
- PowerShell Abuse

IoCs provide evidence that a compromise has occurred.

---

# Indicators of Attack (IoAs)

IoCs describe evidence **after compromise.**

IoAs describe **attacker behaviour** while an attack is occurring.

Example:

```text
PowerShell

↓

Credential Dumping

↓

Privilege Escalation
```

Modern detection increasingly focuses on behavioural indicators rather than only static indicators.

---

# Phase 3 – Containment

Once an incident is confirmed,

the priority becomes preventing further damage.

Containment limits attacker movement.

Examples:

- Disconnect compromised device
- Disable compromised account
- Block malicious IP
- Stop malicious process
- Disable vulnerable service
- Isolate infected endpoint

Containment is usually divided into:

### Short-Term Containment

Immediate action to stop the attack.

---

### Long-Term Containment

Temporary fixes until permanent remediation is completed.

---

# Example

Suppose ransomware is detected.

Containment may include:

```text
Disconnect Endpoint

↓

Disable Network Access

↓

Prevent File Encryption

↓

Preserve Evidence
```

---

# Phase 4 – Eradication

Containment stops the attack.

Eradication removes the root cause.

Examples:

- Delete malware
- Remove persistence
- Patch vulnerabilities
- Remove malicious accounts
- Delete web shells
- Reset passwords

The goal is complete removal of attacker access.

---

# Phase 5 – Recovery

Recovery restores business operations.

Examples:

- Restore backups
- Reconnect systems
- Monitor recovered systems
- Validate integrity
- Resume business operations

Recovery should occur only after the organization is confident that the attacker no longer has access.

---

# Phase 6 – Lessons Learned

This is one of the most valuable phases.

Questions include:

- What happened?
- Why did it happen?
- Which controls failed?
- Which detections worked?
- Which detections failed?
- How can we improve?

Organizations update:

- Detection rules
- Playbooks
- Policies
- Training
- Monitoring

Continuous improvement is a key objective of mature SOCs.

---

# Incident Severity

Organizations often classify incidents.

Example:

| Severity | Example |
|----------|---------|
| Low | Single Failed Login |
| Medium | Malware Detected |
| High | Privilege Escalation |
| Critical | Ransomware / Data Breach |

Severity determines escalation priority.

---

# Escalation Process

Not every incident is handled by the same analyst.

Example:

```text
Tier 1

↓

Tier 2

↓

Tier 3

↓

Incident Response Team

↓

Management
```

Higher-severity incidents receive faster escalation.

---

# Documentation

Every incident should be documented.

Typical report includes:

- Timeline
- Affected systems
- Evidence
- IoCs
- MITRE ATT&CK Mapping
- Root Cause
- Containment Actions
- Recovery Steps
- Recommendations

Proper documentation supports:

- Compliance
- Audits
- Legal proceedings
- Future investigations

---

# Chain of Custody

When collecting digital evidence,

organizations must preserve its integrity.

Chain of Custody records:

- Who collected evidence
- When it was collected
- How it was stored
- Who accessed it
- When it was transferred

This is especially important if evidence may be used in legal proceedings.

---

# Automation in Incident Response

Modern SOCs increasingly automate repetitive tasks.

Examples:

- Block malicious IP
- Disable compromised account
- Isolate endpoint
- Create ticket
- Notify analyst

Automation reduces response time while allowing analysts to focus on investigation.

---

# Common Challenges

Incident Response teams often face:

- Alert fatigue
- False positives
- Limited visibility
- Insider threats
- Cloud environments
- Encryption
- Sophisticated attackers

Continuous improvement helps overcome these challenges.

---

# Learning Objectives

After completing this section, students should be able to:

- Define a security incident.
- Explain the NIST Incident Response Lifecycle.
- Differentiate events, alerts, and incidents.
- Describe containment, eradication, and recovery.
- Explain the importance of IoCs and IoAs.
- Understand incident documentation and evidence preservation.

---

# Interview Questions

## What is Incident Response?

Incident Response is a structured process used to detect, investigate, contain, eradicate, recover from, and learn from cybersecurity incidents.

---

## What is the first phase of the NIST Incident Response Lifecycle?

Preparation.

---

## What is the purpose of containment?

Containment prevents an attacker from causing additional damage while preserving evidence for investigation.

---

## What is the difference between containment and eradication?

Containment limits the attack, while eradication removes the attacker's presence and the root cause of the compromise.

---

## What is an Indicator of Compromise (IoC)?

An Indicator of Compromise is evidence suggesting that a system has been compromised, such as a malicious IP address, suspicious file hash, or unauthorized account.

---

## Why is the "Lessons Learned" phase important?

It enables organizations to improve detection rules, policies, playbooks, training, and overall security posture based on the experience gained during the incident.

---

# Key Takeaways

- Incident Response transforms threat detection into structured action.
- The NIST lifecycle consists of Preparation, Detection & Analysis, Containment, Eradication, Recovery, and Lessons Learned.
- Effective response minimizes damage while preserving forensic evidence.
- Documentation, evidence handling, and continuous improvement are essential components of a mature SOC.
- Automation and well-defined playbooks significantly improve response speed and consistency.

# Session 11 – Defensive Security and the Security Operations Centre (SOC)
## Part 9 – Wazuh Active Response, Security Automation, SOC Metrics and End-to-End Incident Scenario

**Course:** C-DAC Kolkata – Cybersecurity Industry Exposure Program  
**Module:** Wazuh Active Response & Modern SOC Operations

---

# Introduction

So far, we have studied:

- Log Collection
- SIEM
- Wazuh Architecture
- File Integrity Monitoring
- MITRE ATT&CK
- Incident Response

All of these technologies help **detect** attacks.

However, modern cyber attacks spread extremely quickly.

For example:

- Ransomware can encrypt thousands of files within minutes.
- Worms can infect hundreds of machines.
- Credential theft can immediately lead to privilege escalation.

Waiting for a human analyst to manually respond may take too long.

This introduces the concept of **Active Response**.

---

# What is Active Response?

Active Response is the automatic execution of predefined defensive actions when specific security conditions are met.

Instead of only generating an alert,

the system can automatically perform defensive operations.

Example:

```text
Attack Detected

↓

Alert Generated

↓

Automatically Block Attacker

↓

Notify Analyst
```

This significantly reduces response time.

---

# Why Active Response is Needed

Consider the following scenario.

Without automation:

```text
Attack

↓

Alert

↓

SOC Analyst Notices Alert

↓

Analyst Investigates

↓

Analyst Blocks Attacker

↓

Attack Stops
```

Time Taken:

```text
15 Minutes
```

During these 15 minutes,

the attacker may continue stealing data.

---

With Active Response:

```text
Attack

↓

Alert

↓

Automatic Block

↓

SOC Notification

↓

Analyst Reviews
```

Time Taken:

```text
2 Seconds
```

Automation minimizes attacker dwell time.

---

# Active Response Workflow

The complete workflow is:

```text
Endpoint Activity

↓

Log Generated

↓

Agent Sends Log

↓

Manager Processes Log

↓

Rule Triggered

↓

Severity Evaluated

↓

Active Response Executed

↓

SOC Analyst Notified
```

Notice that automation happens **before** the analyst begins investigation.

---

# Examples of Active Response

Depending on organizational policy,

Wazuh can automatically perform actions such as:

- Block malicious IP addresses
- Disable compromised user accounts
- Kill malicious processes
- Delete malicious files
- Stop suspicious services
- Isolate compromised endpoints
- Execute custom scripts
- Notify administrators
- Create helpdesk tickets

---

# Example 1 – SSH Brute Force Attack

Suppose an attacker repeatedly attempts to log in using SSH.

Activity:

```text
100 Failed Logins

↓

Wazuh Rule Triggered

↓

Severity = High

↓

Active Response

↓

Firewall Blocks Source IP
```

The attack stops automatically without waiting for manual intervention.

---

# Example 2 – Malware Detection

Suppose an endpoint detects ransomware.

Workflow:

```text
Malware Detected

↓

Critical Alert

↓

Endpoint Isolation

↓

SOC Notification

↓

Investigation Begins
```

The malware cannot spread to additional systems.

---

# Example 3 – File Integrity Monitoring

Suppose Syscheck detects:

```text
shell.php

uploaded into

/var/www/html
```

Active Response may:

- Quarantine the file
- Notify the SOC
- Create an incident ticket

This reduces the risk of attacker persistence.

---

# Response Scripts

Wazuh Active Response relies on scripts.

Examples include:

```text
Firewall Script

↓

Block IP
```

```text
Endpoint Script

↓

Kill Process
```

```text
Linux Script

↓

Disable User
```

Organizations can also create custom scripts tailored to their environment.

---

# Advantages of Automation

Automation provides several benefits.

### Faster Response

Human reaction:

```text
Minutes
```

Automation:

```text
Seconds
```

---

### Consistency

Automation performs the same response every time.

Human responses may vary.

---

### Reduced Analyst Workload

Analysts spend less time performing repetitive actions.

Instead,

they focus on investigation.

---

### Reduced Damage

Rapid containment reduces:

- Data loss
- Malware spread
- Business downtime

---

# Risks of Automation

Automation must be configured carefully.

Example:

Suppose a rule mistakenly identifies a legitimate administrator as malicious.

Active Response:

```text
Disable Administrator Account
```

Business operations may be disrupted.

Therefore,

organizations generally automate only well-understood response actions.

---

# Playbooks

A **Playbook** is a documented set of response steps for a specific incident.

Example:

SSH Brute Force Playbook

```text
Alert Received

↓

Verify Source IP

↓

Check Authentication Logs

↓

Block IP

↓

Reset Password

↓

Investigate User Activity

↓

Document Incident
```

Playbooks ensure consistent response across analysts.

---

# Benefits of Playbooks

Playbooks provide:

- Standardization
- Faster investigations
- Reduced mistakes
- Easier analyst training
- Compliance support

Every major SOC relies on documented playbooks.

---

# Mean Time To Detect (MTTD)

One of the most important SOC metrics is:

```text
MTTD

↓

Mean Time To Detect
```

Definition:

Average time required to detect a security incident.

Example:

Attack begins:

```text
10:00 AM
```

Detected:

```text
10:08 AM
```

MTTD:

```text
8 Minutes
```

Lower values indicate better monitoring.

---

# Mean Time To Respond (MTTR)

MTTR stands for:

```text
Mean Time To Respond
```

Definition:

Average time required to contain and respond after detection.

Example:

Incident detected:

```text
10:08 AM
```

Contained:

```text
10:15 AM
```

MTTR:

```text
7 Minutes
```

Organizations continuously attempt to reduce both MTTD and MTTR.

---

# Why MTTD and MTTR Matter

Attack Timeline:

```text
Attack Begins

↓

Detection

↓

Response

↓

Recovery
```

The longer the attacker remains undetected,

the greater the damage.

Reducing detection and response time is one of the primary objectives of a SOC.

---

# Alert Fatigue

Large organizations receive thousands of alerts every day.

Example:

```text
15,000 Alerts

↓

Only 25 Genuine Incidents
```

If analysts investigate every alert,

important attacks may be overlooked.

This problem is known as **Alert Fatigue**.

---

# Causes of Alert Fatigue

Common causes include:

- Poor detection rules
- Duplicate alerts
- False positives
- Excessive logging
- Low-priority notifications

Proper rule tuning reduces alert fatigue.

---

# Rule Tuning

Rule tuning involves improving detection logic.

Example:

Original Rule:

```text
Three Failed Logins

↓

Generate Alert
```

Too many false positives.

Improved Rule:

```text
Ten Failed Logins

AND

Successful Login

↓

Generate Alert
```

This rule is more accurate.

---

# End-to-End Incident Scenario

The instructor discussed how all concepts learned throughout the session connect together.

Scenario:

An attacker launches an SSH brute-force attack.

```text
Attacker

↓

SSH Login Attempts

↓

Linux Authentication Logs

↓

Wazuh Agent

↓

Manager

↓

Decoder

↓

Rule Evaluation

↓

MITRE Mapping

↓

High Severity Alert

↓

Active Response

↓

Firewall Blocks IP

↓

SOC Dashboard Updated

↓

Analyst Investigation

↓

Incident Report

↓

Lessons Learned
```

Notice how every component introduced in this session participates in the detection process.

---

# Complete SOC Workflow

```text
Collect Logs

↓

Normalize Logs

↓

Decode Events

↓

Apply Rules

↓

Correlate Events

↓

Generate Alerts

↓

MITRE Mapping

↓

Active Response

↓

SOC Investigation

↓

Incident Response

↓

Recovery

↓

Lessons Learned
```

This represents the complete lifecycle of modern security monitoring.

---

# Best Practices

Organizations should:

- Automate repetitive tasks.
- Keep analysts involved in critical decisions.
- Continuously tune rules.
- Maintain updated playbooks.
- Review incidents regularly.
- Measure MTTD and MTTR.
- Integrate threat intelligence.
- Perform Purple Team exercises.

---

# Learning Objectives

After completing this section, students should be able to:

- Explain Active Response.
- Describe automated incident handling.
- Explain SOC playbooks.
- Define MTTD and MTTR.
- Understand alert fatigue.
- Explain rule tuning.
- Describe an end-to-end SOC detection workflow.

---

# Interview Questions

## What is Active Response?

Active Response is the automatic execution of predefined security actions when specific detection rules are triggered.

---

## Why is Active Response important?

It reduces response time, limits attacker movement, minimizes damage, and improves overall security operations.

---

## What is a Playbook?

A playbook is a documented sequence of actions that guides analysts through the response to a specific type of security incident.

---

## What is MTTD?

Mean Time To Detect is the average time required to identify a security incident after it begins.

---

## What is MTTR?

Mean Time To Respond is the average time required to contain and respond to a detected incident.

---

## What is Alert Fatigue?

Alert fatigue occurs when analysts receive an overwhelming number of alerts, making it difficult to identify genuine security incidents.

---

## Why is Rule Tuning necessary?

Rule tuning improves detection accuracy by reducing false positives, minimizing unnecessary alerts, and helping analysts focus on real threats.

---

# Key Takeaways

- Active Response enables Wazuh to automatically execute defensive actions immediately after threat detection.
- Automation significantly reduces attacker dwell time and limits damage.
- Playbooks ensure consistent and repeatable incident handling.
- SOC performance is measured using metrics such as MTTD and MTTR.
- Rule tuning and alert prioritization are essential for reducing alert fatigue.
- A modern SOC integrates detection, automation, investigation, and continuous improvement into a single security workflow.

# Session 11 – Defensive Security and the Security Operations Centre (SOC)
## Part 10 – Complete Revision Guide, Practical Summary, Interview Preparation and Final Notes

**Course:** C-DAC Kolkata – Cybersecurity Industry Exposure Program  
**Module:** Defensive Security, SIEM, Wazuh and SOC Operations

---

# Session 11 Complete Learning Flow

The entire session can be summarized using the following flow.

```text
Modern Cyber Attacks

↓

Need for Defensive Security

↓

Security Operations Centre (SOC)

↓

SIEM

↓

Wazuh Platform

↓

Log Collection

↓

Log Analysis

↓

Threat Detection

↓

MITRE ATT&CK Mapping

↓

File Integrity Monitoring

↓

Incident Response

↓

Active Response

↓

Continuous Improvement
```

This represents the lifecycle of a modern Security Operations Centre.

---

# Complete Wazuh Data Flow

The instructor repeatedly emphasized understanding how information flows through Wazuh.

```text
User Activity

↓

Operating System

↓

Log Generated

↓

Wazuh Agent

↓

Encrypted Communication

↓

Wazuh Manager

↓

Decoder

↓

Normalization

↓

Rule Matching

↓

Correlation

↓

Alert Generation

↓

Indexer

↓

Dashboard

↓

SOC Analyst

↓

Incident Response
```

This is the single most important diagram from the session.

---

# End-to-End Attack Detection Workflow

Suppose an attacker launches an SSH brute-force attack.

The complete sequence is:

```text
Attacker

↓

SSH Login Attempts

↓

Linux Authentication Logs

↓

Wazuh Agent

↓

Manager Receives Events

↓

Decoder Extracts Fields

↓

Rule Matches

↓

MITRE ATT&CK Mapping

↓

High Severity Alert

↓

Active Response

↓

Firewall Blocks IP

↓

SOC Dashboard Updated

↓

Tier-1 Analyst Reviews

↓

Tier-2 Investigation

↓

Incident Confirmed

↓

Containment

↓

Recovery

↓

Lessons Learned
```

Notice that every topic covered during the session contributes to this workflow.

---

# Relationship Between Major Components

```text
Operating System

↓

Logs

↓

SIEM

↓

Rules

↓

Alerts

↓

SOC

↓

Incident Response
```

Everything begins with **logs**.

Without logs:

- No SIEM
- No alerts
- No investigations
- No incident response

---

# Defensive Security Mind Map

```text
Defensive Security

├── SOC

│      ├── Tier 1

│      ├── Tier 2

│      ├── Tier 3

│      └── SOC Manager

│

├── SIEM

│      ├── Log Collection

│      ├── Normalization

│      ├── Correlation

│      ├── Alerting

│      └── Dashboard

│

├── Wazuh

│      ├── Agent

│      ├── Manager

│      ├── Indexer

│      └── Dashboard

│

├── MITRE ATT&CK

│      ├── Tactics

│      ├── Techniques

│      └── Threat Hunting

│

├── Incident Response

│      ├── Detection

│      ├── Containment

│      ├── Eradication

│      ├── Recovery

│      └── Lessons Learned

│

└── Active Response

       ├── Automation

       ├── Blocking

       ├── Isolation

       └── Playbooks
```

---

# SOC Workflow

```text
Collect Logs

↓

Store Logs

↓

Decode Logs

↓

Normalize Data

↓

Correlation Rules

↓

Alert

↓

SOC Investigation

↓

Incident

↓

Response

↓

Recovery

↓

Documentation

↓

Continuous Improvement
```

---

# SIEM Workflow

```text
Data Sources

↓

Log Collection

↓

Parsing

↓

Normalization

↓

Rule Evaluation

↓

Correlation

↓

Alert Generation

↓

Dashboard

↓

Reports
```

---

# Incident Response Workflow

```text
Preparation

↓

Detection

↓

Analysis

↓

Containment

↓

Eradication

↓

Recovery

↓

Lessons Learned
```

This is based on the NIST Incident Response Lifecycle.

---

# MITRE ATT&CK Workflow

```text
Alert

↓

MITRE Mapping

↓

Tactic

↓

Technique

↓

Investigation

↓

Threat Hunting

↓

Improved Detection
```

---

# File Integrity Monitoring Workflow

```text
Baseline

↓

File Monitoring

↓

Hash Comparison

↓

Modification?

↓

Alert

↓

Investigation
```

---

# Active Response Workflow

```text
Alert

↓

Rule Triggered

↓

Active Response

↓

Firewall Block

↓

Endpoint Isolation

↓

SOC Notification
```

---

# Important Terminology

| Term | Meaning |
|------|---------|
| SOC | Security Operations Centre |
| SIEM | Security Information and Event Management |
| XDR | Extended Detection and Response |
| FIM | File Integrity Monitoring |
| EDR | Endpoint Detection and Response |
| IoC | Indicator of Compromise |
| IoA | Indicator of Attack |
| MITRE | Adversarial Tactics, Techniques and Common Knowledge |
| CVE | Common Vulnerabilities and Exposures |
| CVSS | Common Vulnerability Scoring System |
| MTTD | Mean Time To Detect |
| MTTR | Mean Time To Respond |
| SCA | Security Configuration Assessment |

---

# Wazuh Components

| Component | Responsibility |
|------------|----------------|
| Agent | Collect endpoint logs |
| Manager | Process events and apply rules |
| Decoder | Parse raw logs |
| Rule Engine | Match suspicious activity |
| Indexer | Store searchable data |
| Dashboard | Display alerts and reports |

---

# Responsibilities of a SOC Analyst

A SOC analyst should be able to:

- Monitor dashboards.
- Review alerts.
- Investigate suspicious events.
- Validate incidents.
- Collect evidence.
- Escalate incidents.
- Contain attacks.
- Document findings.
- Improve detection rules.

---

# Common Interview Questions

## What is the difference between SIEM and Wazuh?

A SIEM is a category of security platforms used for centralized log collection, correlation, and threat detection.

Wazuh is an open-source security platform that implements SIEM capabilities while also providing endpoint detection, file integrity monitoring, vulnerability detection, and active response.

---

## Why are logs important?

Logs provide historical evidence of system activity and enable security monitoring, incident investigation, digital forensics, compliance, and threat detection.

---

## What happens if logs are not collected?

Without logs:

- Security incidents cannot be investigated effectively.
- Threat detection becomes extremely limited.
- Compliance requirements may not be met.
- Digital forensic analysis becomes difficult.

---

## Why is correlation important?

Individual events often appear harmless.

Correlation combines multiple related events to identify attack patterns that would otherwise remain undetected.

---

## Why is MITRE ATT&CK important?

MITRE ATT&CK provides a standardized framework for understanding attacker behaviour, improving detection engineering, supporting threat hunting, and enhancing incident response.

---

## Why is File Integrity Monitoring useful?

It detects unauthorized modifications to important files, helping identify malware, web shells, insider threats, and persistence mechanisms.

---

## Why is Active Response important?

Active Response automatically executes predefined defensive actions, reducing attacker dwell time and minimizing damage before manual investigation begins.

---

# Common Mistakes in SOC Operations

Organizations frequently make the following mistakes:

- Collecting logs but never reviewing them.
- Generating alerts without tuning detection rules.
- Ignoring low-severity alerts that may indicate larger attack chains.
- Failing to update detection rules.
- Not documenting incidents.
- Delaying incident response.
- Lacking tested playbooks.
- Monitoring only servers while ignoring endpoints.

---

# Best Practices

A mature SOC should:

- Collect logs from all critical assets.
- Maintain synchronized system time (NTP).
- Retain logs securely.
- Regularly tune SIEM rules.
- Validate detections using Purple Team exercises.
- Perform threat hunting.
- Test incident response plans.
- Automate repetitive response actions.
- Continuously train analysts.

---

# One-Page Revision Sheet

Remember the sequence:

```text
Endpoint

↓

Logs

↓

Agent

↓

Manager

↓

Decoder

↓

Rules

↓

Correlation

↓

Alert

↓

MITRE

↓

SOC

↓

Incident Response

↓

Recovery
```

Remember the Wazuh components:

```text
Agent

↓

Manager

↓

Indexer

↓

Dashboard
```

Remember the NIST Incident Response Lifecycle:

```text
Preparation

↓

Detection & Analysis

↓

Containment

↓

Eradication

↓

Recovery

↓

Lessons Learned
```

Remember the SOC progression:

```text
Log

↓

Event

↓

Alert

↓

Incident

↓

Response
```

---

# Complete Session Summary

This session marked the transition from **Offensive Security** to **Defensive Security**.

Students learned why organizations require continuous monitoring instead of relying solely on preventive controls.

The session introduced the concept of a **Security Operations Centre (SOC)** and explained how SIEM platforms centralize security visibility by collecting, normalizing, correlating, and analyzing logs from diverse systems.

The architecture and capabilities of **Wazuh** were explored in detail, including:

- Agent
- Manager
- Indexer
- Dashboard
- Decoders
- Rules
- Alerts

Students learned how **File Integrity Monitoring (Syscheck)** detects unauthorized modifications to critical files and how vulnerability detection identifies outdated software with known CVEs.

The **MITRE ATT&CK Framework** was introduced as a standardized method for understanding attacker behaviour and mapping alerts to real-world attack techniques.

Finally, the session covered the **NIST Incident Response Lifecycle**, Wazuh Active Response, SOC automation, playbooks, performance metrics such as MTTD and MTTR, and the importance of continuous improvement through documentation and lessons learned.

---

# Final Learning Outcomes

By the end of Session 11, students should be able to:

- Explain the objectives of Defensive Security.
- Describe the role and architecture of a Security Operations Centre.
- Explain how SIEM platforms collect, process, and correlate security logs.
- Understand the architecture and operation of Wazuh.
- Explain File Integrity Monitoring and Vulnerability Detection.
- Interpret MITRE ATT&CK mappings.
- Describe the complete Incident Response Lifecycle.
- Explain Active Response and SOC automation.
- Understand the responsibilities of SOC analysts.
- Apply defensive security concepts to real-world enterprise environments.

---

# Final Note

The central message of this session is that **successful cybersecurity is not achieved solely by preventing attacks, but by building the capability to detect, investigate, respond to, and continuously learn from security incidents.** Modern organizations assume that breaches will occur and therefore invest heavily in visibility, monitoring, automation, and structured incident response. A well-designed SOC, supported by SIEM platforms such as Wazuh and guided by frameworks like MITRE ATT&CK and the NIST Incident Response Lifecycle, enables organizations to reduce attacker dwell time, minimize business impact, and continuously strengthen their security posture.

