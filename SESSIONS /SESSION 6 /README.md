
# Session 6 – Network Attacks, ARP Poisoning, DoS/DDoS and Web Security Foundations

**Date:** 16 June 2026
**Duration:** 2:00 PM – 5:00 PM
**Course:** CDAC Industry Exposure Program – Cybersecurity
**Session:** 6

---

# Overview

Session 6 focused on foundational network security concepts and practical attack demonstrations using Kali Linux and Metasploitable. The session began with the principle:

> You cannot attack what you do not understand.

The instructor explained that before learning attacks such as Man-in-the-Middle, ARP poisoning, ARP spoofing, DoS, DDoS, packet sniffing, or web request manipulation, it is necessary to understand how normal network communication works.

The session covered:

* Network layers
* MAC addresses
* IP addresses
* Switches
* ARP
* ARP cache
* ARP scanning
* Man-in-the-Middle attacks
* HTTPS and TLS protection
* ARP poisoning
* IP forwarding
* Kali and Metasploitable demonstration
* DoS and DDoS attacks
* Volumetric and protocol-based attacks
* DDoS defenses
* HTTP request and response basics
* Intercepting proxy concept
* Burp Suite introduction

The session connected low-level network attacks with web security fundamentals, showing how attackers first understand the network path and then move toward intercepting, modifying, or replaying traffic.

---

# Ethical Note

The techniques discussed in this session, including ARP scanning, ARP poisoning, MITM, DoS/DDoS concepts, and intercepting traffic, must only be performed in a legal lab environment or on systems where written authorization has been obtained.

In the session, the practical work was done using a controlled lab setup involving Kali Linux and Metasploitable virtual machines.

---

# Section 1 – Networking Foundations

## Why Networking Foundations Matter

Cybersecurity attacks do not happen in isolation. Every attack depends on normal system behavior.

For example:

* ARP poisoning abuses normal ARP behavior.
* MITM abuses traffic forwarding.
* DNS spoofing abuses name resolution.
* SYN flood abuses the TCP handshake.
* Burp Suite abuses the fact that the browser sends controllable HTTP requests.

Therefore, before learning attacks, we must understand how devices normally communicate.

---

# Network Layers

The instructor introduced the idea of layered communication.

A network is divided into layers so that each layer handles a specific responsibility.

For this session, the important layers were:

```text
Application Layer
Transport Layer
Network Layer
Data Link Layer
Physical Layer
```

Each layer depends on the layer below it.

This is a key security idea:

```text
Each layer trusts the one below it.
```

If a lower layer is manipulated, the upper layers may continue trusting the wrong information.

---

## Application Layer

The Application Layer is where user-facing services operate.

Examples:

```text
HTTP
HTTPS
DNS
SMTP
FTP
SSH
```

This is the layer where users interact with websites, email, files, and applications.

### Examples

When a user opens:

```text
https://google.com
```

the browser is using application-layer protocols.

When a user sends an email, the system may use:

```text
SMTP
```

When a user types a domain name, the system uses:

```text
DNS
```

to resolve the domain name into an IP address.

---

## Important Application Layer Protocols

### HTTP

HTTP stands for:

```text
HyperText Transfer Protocol
```

It is used for web browsing.

Example:

```text
http://example.com
```

Default port:

```text
80
```

HTTP is not encrypted. If login credentials are sent using plain HTTP, they can be intercepted and read.

---

### HTTPS

HTTPS stands for:

```text
HyperText Transfer Protocol Secure
```

It is HTTP protected using TLS encryption.

Example:

```text
https://example.com
```

Default port:

```text
443
```

HTTPS protects:

* Usernames
* Passwords
* Cookies
* Form data
* Session tokens

from being read by attackers sitting in the middle.

---

### DNS

DNS stands for:

```text
Domain Name System
```

It converts human-readable domain names into IP addresses.

Example:

```text
google.com
        ↓
142.250.x.x
```

DNS is often called the internet's phone book.

---

### SMTP

SMTP stands for:

```text
Simple Mail Transfer Protocol
```

It is used for sending emails.

Common ports:

```text
25
465
587
```

SMTP is important in cybersecurity because email-based attacks such as phishing, spoofing, and business email compromise often involve mail infrastructure.

---

# Transport Layer

The Transport Layer manages communication between applications running on different systems.

The two most important transport protocols are:

```text
TCP
UDP
```

---

## TCP

TCP stands for:

```text
Transmission Control Protocol
```

TCP is reliable and connection-oriented.

It ensures:

* Data is delivered
* Data is ordered
* Lost packets are retransmitted
* Communication is acknowledged

Examples of services using TCP:

* HTTP
* HTTPS
* SSH
* FTP
* SMTP

---

## TCP Three-Way Handshake

Before TCP communication begins, a connection is established using a three-way handshake.

```text
Client                  Server
  | ---- SYN ----------> |
  | <--- SYN-ACK ------- |
  | ---- ACK ----------> |
```

### Step 1 – SYN

The client says:

```text
I want to start a connection.
```

### Step 2 – SYN-ACK

The server replies:

```text
I received your request and I am ready.
```

### Step 3 – ACK

The client confirms:

```text
Connection established.
```

This handshake becomes important later when learning about SYN flood attacks.

---

## UDP

UDP stands for:

```text
User Datagram Protocol
```

UDP is fast but unreliable.

It does not establish a connection before sending data.

It does not guarantee delivery.

Used for:

* DNS
* Streaming
* Gaming
* Voice/video calls

UDP is often used in DDoS attacks because it is lightweight and can generate large volumes of traffic.

---

## Ports

A port identifies a specific service running on a machine.

Think of it like this:

```text
IP Address = Building Address
Port       = Room Number
```

Common ports:

| Port | Service |
| ---- | ------- |
| 21   | FTP     |
| 22   | SSH     |
| 25   | SMTP    |
| 53   | DNS     |
| 80   | HTTP    |
| 443  | HTTPS   |
| 3306 | MySQL   |

Example:

```text
192.168.1.10:80
```

means:

```text
Host 192.168.1.10
Service on port 80
HTTP web service
```

---

# Network Layer

The Network Layer handles routing between networks.

The main concept here is:

```text
IP Address
```

---

## IP Address

IP stands for:

```text
Internet Protocol
```

An IP address identifies a device logically on a network.

Examples:

```text
192.168.1.10
10.0.2.15
8.8.8.8
```

An IP address is used by routers to move packets from one network to another.

---

## Router

A router connects different networks.

Example:

```text
Home Network
     ↓
Router
     ↓
Internet
```

Routers use IP addresses to decide where packets should go next.

---

# Data Link Layer

The Data Link Layer handles local network communication.

Important concepts:

```text
MAC Address
Switch
ARP
```

This layer is extremely important for this session because ARP spoofing and ARP poisoning work at Layer 2.

---

# MAC Address

MAC stands for:

```text
Media Access Control
```

A MAC address is a physical address assigned to a network interface card.

Example:

```text
08:00:27:95:b9:e6
```

A MAC address is used for communication inside a local network.

---

## Characteristics of MAC Address

A MAC address is:

* Layer 2 address
* Physical address
* Used inside a LAN
* Used by switches
* Usually assigned to the network card
* Represented in hexadecimal

Example:

```text
00:1A:2B:3C:4D:5E
```

A MAC address contains 48 bits and is usually written as six hexadecimal pairs.

---

# IP Address vs MAC Address

A very important concept from the session:

```text
Do not confuse IP address and MAC address.
```

They serve different purposes.

| MAC Address                | IP Address                 |
| -------------------------- | -------------------------- |
| Layer 2                    | Layer 3                    |
| Physical address           | Logical address            |
| Used locally               | Used across networks       |
| Used by switches           | Used by routers            |
| Does not cross routers     | Can travel across networks |
| Example: 08:00:27:95:b9:e6 | Example: 10.0.2.15         |

---

## Simple Analogy

```text
MAC Address = Physical seat number
IP Address  = Postal address
```

A MAC address identifies the physical interface within a local network.

An IP address identifies where the device is located logically in the network.

---

# Example

Suppose Kali Linux has:

```text
IP Address  : 10.0.2.15
MAC Address : 08:00:27:95:b9:e6
```

The IP address helps route packets.

The MAC address helps deliver frames locally through the switch.

---

# Switches

A switch connects devices inside a LAN.

Examples of devices connected to a switch:

* Laptop
* Printer
* Server
* Router
* Camera
* Desktop

A switch works at Layer 2 and uses MAC addresses.

---

# Hub vs Switch

## Hub

A hub is an older network device.

It sends traffic to everyone.

Example:

```text
A sends data to B
Hub sends it to B, C, D, E
```

This means every device receives the traffic.

Because of this, passive sniffing was easy on old hub-based networks.

---

## Switch

A switch is smarter.

It learns which MAC address is connected to which port.

Then it forwards traffic only to the correct destination port.

Example:

```text
A sends data to B
Switch sends it only to B's port
```

This improves performance and privacy.

---

# MAC Address Table / CAM Table

A switch stores MAC-to-port mappings in a table.

This table is called:

```text
MAC Address Table
```

or

```text
CAM Table
```

Example:

| MAC Address       | Switch Port |
| ----------------- | ----------- |
| AA:AA:AA:AA:AA:AA | Port 1      |
| BB:BB:BB:BB:BB:BB | Port 2      |
| CC:CC:CC:CC:CC:CC | Port 3      |

When traffic comes in, the switch checks the destination MAC and forwards the frame only to the correct port.

---

# Why You Cannot Simply Sniff a Switched LAN

The instructor explained a key idea:

> On a switched network, other people's traffic does not automatically reach your machine.

If Victim talks to Router:

```text
Victim → Switch → Router
```

the attacker connected to another switch port does not receive that traffic.

So simply opening Wireshark on the attacker's machine will not show all network traffic.

This is why attackers need attacks like:

* ARP spoofing
* ARP poisoning
* MITM
* MAC flooding

to force traffic to pass through them.

---

# Broadcast Traffic

One exception exists: broadcast traffic.

Broadcast MAC address:

```text
FF:FF:FF:FF:FF:FF
```

This means:

```text
Send to everyone on the LAN.
```

ARP requests use broadcast.

This is one of the reasons ARP becomes important for attacks.

---

# ARP – Address Resolution Protocol

ARP stands for:

```text
Address Resolution Protocol
```

ARP solves a basic problem:

```text
I know the IP address.
But I need the MAC address.
```

A device may know that the gateway is:

```text
10.0.2.1
```

But to send a frame inside the LAN, it needs the gateway's MAC address.

ARP performs:

```text
IP Address → MAC Address
```

conversion.

---

# Why ARP Is Needed

Switches do not forward frames using IP addresses.

They forward frames using MAC addresses.

Therefore, before a device can send data locally, it must know the destination MAC address.

Example:

```text
Destination IP  : 10.0.2.1
Destination MAC : Unknown
```

ARP is used to discover the MAC.

---

# ARP Request

If a system wants to know the MAC address for an IP, it sends an ARP request.

Example:

```text
Who has 10.0.2.1?
Tell 10.0.2.15
```

This request is broadcast.

Every device on the local network receives it.

---

# ARP Reply

Only the device that owns that IP address replies.

Example:

```text
10.0.2.1 is at 52:55:0a:00:02:01
```

This reply is normally unicast back to the requester.

---

# ARP Cache

After receiving the reply, the system stores the mapping in the ARP cache.

Example:

```text
10.0.2.1 → 52:55:0a:00:02:01
```

This avoids asking again for every packet.

---

## Viewing ARP Cache

Linux:

```bash
arp -a
```

or

```bash
ip neigh
```

Windows:

```cmd
arp -a
```

Example output:

```text
10.0.2.1 at 52:55:0a:00:02:01 [ether] on eth0
```

---

# Why ARP Cache Exists

Without ARP cache:

```text
Every packet would require a new ARP request.
```

That would be inefficient.

With ARP cache:

```text
Ask once.
Store result.
Reuse mapping.
```

---

# The Root Flaw of ARP

The most important weakness:

```text
ARP believes whatever it is told.
```

ARP was created when local networks were considered trusted.

Because of that, ARP has:

* No authentication
* No digital signature
* No certificate
* No verification
* No proof of ownership

If a system receives an ARP reply, it may accept it and update its cache.

---

# Gratuitous ARP

A gratuitous ARP is an ARP reply sent even when nobody asked for it.

Example:

```text
10.0.2.1 is at AA:AA:AA:AA:AA:AA
```

If a victim accepts this reply, its ARP cache may be updated even though it never requested that information.

This is a key reason ARP poisoning works.

---

# Normal ARP Example

Router:

```text
IP  : 10.0.2.1
MAC : 52:55:0a:00:02:01
```

Victim asks:

```text
Who has 10.0.2.1?
```

Router replies:

```text
10.0.2.1 is at 52:55:0a:00:02:01
```

Victim stores:

```text
10.0.2.1 → 52:55:0a:00:02:01
```

This is correct.

---

# Malicious ARP Example

Attacker has MAC:

```text
08:00:27:95:b9:e6
```

Attacker sends fake ARP reply:

```text
10.0.2.1 is at 08:00:27:95:b9:e6
```

Victim accepts it and updates:

```text
10.0.2.1 → 08:00:27:95:b9:e6
```

Now the victim believes the attacker's MAC address belongs to the router.

This is ARP poisoning.

---

# Why ARP Attacks Are Powerful

Once the victim believes the attacker is the router, traffic flows like this:

```text
Victim → Attacker → Router → Internet
```

instead of:

```text
Victim → Router → Internet
```

This creates a Man-in-the-Middle position.

---

# Section 1 Key Takeaways

* Networks operate in layers.
* Each layer depends on the layer below it.
* MAC addresses are Layer 2 physical addresses.
* IP addresses are Layer 3 logical addresses.
* Switches forward frames using MAC addresses.
* Switches prevent passive sniffing by forwarding traffic only to the correct port.
* ARP converts IP addresses into MAC addresses.
* ARP requests are broadcast.
* ARP replies are usually unicast.
* ARP cache stores IP-to-MAC mappings.
* ARP has no authentication.
* ARP poisoning abuses this lack of authentication.
* Understanding MAC, IP, switches, and ARP is necessary before understanding MITM attacks.

---
# Section 2 – ARP Scanning and Host Discovery

Before launching attacks, an attacker must first answer:

```text
Who is on the network?
```

This phase is called:

```text
Reconnaissance
```

or

```text
Host Discovery
```

The goal is to identify:

* Active hosts
* IP addresses
* MAC addresses
* Routers
* Servers
* Printers
* Cameras
* IoT devices

---

# ARP Scanning

ARP scanning is a Layer 2 host discovery technique.

It works by sending ARP requests to every address inside a subnet.

Example:

```text
Who has 192.168.1.1?
Who has 192.168.1.2?
Who has 192.168.1.3?
...
```

Any active device replies with its MAC address.

---

# Why ARP Scan Is More Reliable Than Ping

ICMP ping can be blocked.

Example:

```text
Firewall blocks ICMP
```

The host appears offline.

However, devices still need ARP to communicate.

Therefore:

```text
ARP Scan
```

can discover hosts that ignore ping requests.

---

# Important Limitation

ARP only works inside the local network.

ARP packets do not cross routers.

Example:

```text
192.168.1.0/24
```

cannot ARP-scan:

```text
10.10.10.0/24
```

because routers do not forward ARP broadcasts.

---

# arp-scan Tool

Common command:

```bash
sudo arp-scan --localnet
```

Purpose:

* Discover active hosts
* Obtain MAC addresses
* Identify vendors

Example output:

```text
192.168.1.1
52:55:0a:00:02:01

192.168.1.3
08:00:27:00:5d:6a
```

---

# OUI and Vendor Identification

The first part of a MAC address identifies the manufacturer.

Called:

```text
Organizationally Unique Identifier (OUI)
```

Example:

```text
08:00:27
```

belongs to:

```text
Oracle VirtualBox
```

Attackers can infer device types simply from MAC addresses.

---

# Nmap Host Discovery

Command:

```bash
nmap -sn 192.168.1.0/24
```

Purpose:

```text
Host Discovery Only
No Port Scan
```

On local networks, Nmap often internally uses ARP.

---

# Netdiscover

Command:

```bash
sudo netdiscover -p
```

Purpose:

Passive discovery.

Instead of sending packets, Netdiscover listens to existing traffic.

Advantages:

* Stealthy
* Difficult to detect
* Generates no scan traffic

Disadvantages:

* Slower
* Depends on existing traffic

---

# Active vs Passive Discovery

## Active

Examples:

```text
arp-scan
nmap -sn
```

Characteristics:

* Sends packets
* Fast
* Detectable

---

## Passive

Example:

```text
netdiscover
```

Characteristics:

* Sends nothing
* Very stealthy
* Slower

---

# Detecting ARP Scans

Blue teams monitor:

```text
Many sequential ARP requests
```

Example:

```text
Who has .1?
Who has .2?
Who has .3?
...
```

generated within a few seconds.

This pattern is abnormal.

---

# Detection Tools

## Snort

IDS capable of detecting:

* ARP sweeps
* ARP floods
* Suspicious broadcasts

---

## Suricata

Provides:

* Packet inspection
* Protocol analysis
* Alert generation

---

## ARPWatch

Tracks:

```text
IP ↔ MAC
```

relationships.

Generates alerts when mappings suddenly change.

Useful for detecting:

* ARP spoofing
* MITM preparation

---

# Defenses

## VLAN Segmentation

Separate networks:

```text
HR VLAN
Finance VLAN
IT VLAN
```

Reducing broadcast domains limits attack surface.

---

## Switch Port Security

Allow only known MAC addresses.

Unknown devices trigger:

* Alerts
* Port shutdown

---

# Section 3 – Man-in-the-Middle (MITM)

## Definition

A MITM attack occurs when an attacker secretly positions themselves between two communicating devices.

Normal:

```text
Victim → Router → Internet
```

MITM:

```text
Victim → Attacker → Router → Internet
```

The attacker becomes invisible.

---

# Capabilities of MITM

## Sniff

Read traffic.

Examples:

* HTTP credentials
* DNS requests
* Cookies

---

## Alter

Modify traffic.

Examples:

* Replace downloads
* Modify forms
* Inject ads

---

## Inject / Redirect

Send users elsewhere.

Example:

```text
bank.com
```

redirected to:

```text
fake-bank.com
```

---

# Ways To Become The Middle

## ARP Poisoning

Manipulate ARP cache.

---

## DNS Spoofing

Manipulate name resolution.

---

## Rogue Access Point

Create fake Wi-Fi.

Example:

```text
Airport_Free_WiFi
```

Victim connects to attacker.

---

## SSL Stripping

Downgrade:

```text
HTTPS
```

to

```text
HTTP
```

making traffic readable.

---

# HTTPS and TLS

HTTPS means:

```text
HTTP + TLS
```

TLS provides:

## Confidentiality

Encryption protects data.

---

## Integrity

Prevents modification.

---

## Authentication

Verifies server identity.

---

# What Attackers Can Still See

Even with HTTPS they can observe:

* Source IP
* Destination IP
* Timing
* Traffic size

But cannot easily see:

* Passwords
* Forms
* Messages

---

# HSTS

HTTP Strict Transport Security.

Purpose:

Force browsers to always use HTTPS.

Protects against:

```text
SSL Stripping
```

---

# Certificate Warnings

Browser warning:

```text
Connection is not private
```

indicates:

```text
Cannot verify server identity
```

Ignoring warnings may allow MITM attacks.

---

# Section 4 – ARP Poisoning

ARP poisoning exploits the fact that:

```text
ARP trusts everyone.
```

---

# Goal

Normal:

```text
Victim → Router
```

After poisoning:

```text
Victim → Attacker → Router
```

---

# First Lie

Attacker tells victim:

```text
Gateway IP
=
Attacker MAC
```

Example:

```text
10.0.2.1 is at AA:AA:AA:AA
```

Victim updates cache.

---

# Second Lie

Attacker tells router:

```text
Victim IP
=
Attacker MAC
```

Router updates cache.

---

# Result

Both systems send traffic through attacker.

---

# Why Fake ARP Replies Must Be Repeated

ARP cache entries expire.

Real devices may correct mappings.

Attackers continuously send forged replies to maintain poisoning.

---

# IP Forwarding

Without forwarding:

```text
Victim → Attacker → X
```

Internet breaks.

Victim notices immediately.

---

Enable forwarding:

```bash
echo 1 | sudo tee /proc/sys/net/ipv4/ip_forward
```

Linux behaves like a router.

---

# Tools

## Ettercap

Supports:

* ARP poisoning
* Sniffing
* DNS spoofing

---

## Bettercap

Modern framework supporting:

* MITM
* Sniffing
* Proxying
* Credential capture

---

## arpspoof

Simple ARP spoofing tool.

---

## Wireshark

Packet analysis tool.

Useful for:

* Observing protocols
* Detecting ARP attacks
* Troubleshooting

---

# Session Hijacking

Cookies identify users.

Example:

```text
sessionid=ABC123
```

Stealing the cookie may allow impersonation without knowing passwords.

---

# Practical Demonstration

Kali Linux:

```text
10.0.2.15
08:00:27:95:b9:e6
```

Metasploitable:

```text
10.0.2.3
08:00:27:00:5d:6a
```

---

Host discovery:

```bash
sudo arp-scan --localnet
```

View ARP cache:

```bash
arp -a
```

Check connectivity:

```bash
ping google.com
```

Enable forwarding:

```bash
echo 1 | sudo tee /proc/sys/net/ipv4/ip_forward
```

These steps prepare the environment for ARP poisoning and MITM attacks.

---

# Part 2 Key Takeaways

* ARP scanning is reliable host discovery.
* Passive reconnaissance is stealthier.
* MITM enables sniffing, altering, and redirecting traffic.
* HTTPS and TLS protect confidentiality and integrity.
* ARP poisoning exploits ARP's lack of authentication.
* IP forwarding is necessary to avoid breaking connectivity.
* Tools such as Ettercap, Bettercap, arpspoof, and Wireshark support MITM operations.
* Cookies and session tokens are valuable targets.

# Section 5 – Denial of Service (DoS) and Distributed Denial of Service (DDoS)

---

# Introduction

Unlike previous attacks which targeted:

* Confidentiality
* Integrity

DoS and DDoS attacks primarily target:

```text
Availability
```

The objective is not to steal data or modify information.

Instead, the attacker attempts to make the service:

* Slow
* Unresponsive
* Completely unavailable

---

# CIA Triad Review

The three pillars of information security are:

## Confidentiality

Protect information from unauthorized disclosure.

Examples:

* Encryption
* Access control

---

## Integrity

Protect information from unauthorized modification.

Examples:

* Hashing
* Digital signatures

---

## Availability

Ensure resources remain accessible to legitimate users.

Examples:

* High availability
* Redundancy
* Load balancing

---

DoS attacks target:

```text
Availability
```

---

# Denial of Service (DoS)

A DoS attack uses a single attacking machine.

```text
Attacker
    ↓
Target Server
```

One system overwhelms the victim.

Examples:

* Sending excessive packets
* Flooding requests
* Exhausting server resources

---

# Distributed Denial of Service (DDoS)

DDoS uses multiple machines simultaneously.

```text
Bot 1
Bot 2
Bot 3
Bot 4
 ↓
Target
```

Thousands of compromised devices attack together.

This collection is called:

```text
Botnet
```

---

# Why DDoS Is Dangerous

DoS:

```text
Single source
Easy to block
```

DDoS:

```text
Thousands of sources
Hard to distinguish from real users
```

---

# Botnets

Attackers compromise devices such as:

* Cameras
* Routers
* IoT devices
* Servers

These become:

```text
Zombie Machines
```

which obey commands from the attacker.

Examples:

* Mirai Botnet
* IoT botnets

---

# Volumetric Attacks

Goal:

```text
Saturate the Pipe
```

Consume bandwidth so legitimate traffic cannot reach the target.

---

# UDP Flood

Large amounts of UDP packets are sent.

```text
Attacker
↓↓↓↓↓↓↓↓↓↓
Target
```

Effects:

* Consumes bandwidth
* Increases CPU usage

---

# ICMP Flood

Massive ping traffic.

```text
Attacker
↓↓↓↓↓↓↓↓↓↓
Target
```

Consumes:

* Network bandwidth
* Processing resources

---

# Measuring Attack Size

Measured in:

```text
Mbps
Gbps
Tbps
```

Examples:

```text
1 Gbps = 1000 Mbps
1 Tbps = 1000 Gbps
```

Modern attacks may exceed several Tbps.

---

# Reflection Attacks

Instead of attacking directly:

```text
Attacker → Victim
```

the attacker uses third-party servers.

Attacker spoofs the victim's IP address.

```text
Attacker
      ↓
Public Server
      ↓
Victim
```

The public server unknowingly attacks the victim.

---

# Amplification Attacks

A small request creates a huge response.

Example:

Request:

```text
15 bytes
```

Response:

```text
750 KB
```

This multiplies attack power.

---

# Common Amplification Services

## DNS Amplification

Small DNS queries create large responses.

---

## NTP Amplification

Abuses old Network Time Protocol servers.

---

## Memcached Amplification

Very powerful amplification mechanism.

Amplification factor:

```text
50,000×
```

---

# GitHub DDoS Attack (2018)

Attack size:

```text
1.35 Tbps
```

Technique:

```text
Memcached Amplification
```

This became one of the largest DDoS attacks recorded.

---

# Protocol Attacks

Unlike volumetric attacks, protocol attacks exploit weaknesses in protocols.

Example:

```text
TCP
```

---

# SYN Flood Attack

TCP normally uses a three-way handshake.

```text
Client        Server

SYN -------->
     <------ SYN-ACK

ACK -------->
```

Connection established.

---

# Attack Process

Attacker sends:

```text
SYN
```

Server replies:

```text
SYN-ACK
```

Attacker never sends:

```text
ACK
```

The server waits.

---

# Half-Open Connections

State:

```text
SYN
SYN-ACK
```

without:

```text
ACK
```

is called:

```text
Half-Open Connection
```

---

# Why SYN Flood Works

Thousands of half-open connections accumulate.

Eventually:

```text
Connection Table Full
```

Legitimate users cannot connect.

Availability is lost.

---

# Defenses Against SYN Flood

## SYN Cookies

Server delays allocating resources until ACK arrives.

Protects against half-open connections.

---

## Rate Limiting

Limit requests per source.

---

## Firewalls

Detect abnormal SYN rates.

---

## IDS/IPS

Examples:

* Snort
* Suricata

---

## Load Balancers

Distribute connections.

---

# DDoS Defenses

---

## Rate Limiting

Restrict excessive requests.

Example:

```text
100 requests/minute allowed
```

---

## Anycast

Multiple geographically distributed servers.

Traffic is spread globally.

---

## CDN

Content Delivery Networks distribute traffic.

Examples:

* Cloudflare
* Akamai

---

## Scrubbing Centers

Traffic enters:

```text
Scrubbing Center
```

Malicious packets are removed.

Only clean traffic reaches the target.

---

## Blackhole Routing

Last resort.

ISP drops all traffic.

```text
Attack traffic → Dropped
Legitimate traffic → Dropped
```

Service becomes unavailable but attack impact stops.

---

# Incident Response

Organizations maintain:

* Emergency contacts
* Playbooks
* ISP contacts
* DDoS providers

to quickly react to attacks.

---

# Section B – HTTP Fundamentals

Everything on the web follows:

```text
Request → Response
```

---

# HTTP Request

Browser sends:

```text
Request
```

to the server.

Components:

## Method

Examples:

```http
GET
POST
PUT
DELETE
```

---

## URL

Example:

```text
https://example.com/login
```

---

## Headers

Metadata.

Examples:

```http
Cookie
Authorization
User-Agent
Content-Type
```

---

## Body

Contains data.

Example:

```text
username=admin
password=test123
```

---

# HTTP Response

Contains:

## Status Code

Examples:

```http
200 OK
403 Forbidden
404 Not Found
500 Internal Server Error
```

---

## Headers

Examples:

```http
Set-Cookie
Content-Type
```

---

## Body

Contains:

* HTML
* JSON
* Images
* Files

---

# Security Principle

Most important statement:

> Everything a web application trusts arrives in a request, and the client controls the request.

Therefore:

```text
Never trust client input.
Always validate on the server.
```

---

# Intercepting Proxy

Normal:

```text
Browser → Server
```

With proxy:

```text
Browser → Proxy → Server
```

The tester can:

* Read requests
* Modify requests
* Replay requests
* Analyze responses

---

# Why It Is Legal

MITM:

```text
Intercepting someone else's traffic
```

Proxy:

```text
Intercepting your own traffic
```

Same technology.

Different ethics.

---

# Browser Restrictions Are Not Security

Client-side controls are conveniences.

Not security mechanisms.

---

# Dropdown Example

Browser:

```html
<select>
<option>User</option>
</select>
```

Proxy can change:

```text
role=admin
```

---

# Disabled Fields

Browser blocks editing.

Proxy bypasses it.

---

# JavaScript Validation

Browser says:

```text
Age 1-100
```

Proxy sends:

```text
Age=9999
```

Server must validate.

---

# Security Mindset

Developers think:

```text
User cannot send this.
```

Security professionals think:

```text
Can the server stop me?
```

---

# Burp Suite

Burp Suite acts as an intercepting proxy.

Workflow:

```text
Browser
 ↓
Burp
 ↓
Server
```

---

# Components

## Proxy

Captures requests.

---

## Repeater

Replay requests manually.

---

## Intruder

Automates repeated requests.

---

## Decoder

Performs:

* Base64
* URL encoding

---

## Comparer

Compares responses.

---

# Example Testing Flow

1. Open website.

2. Login.

3. Request intercepted.

4. Modify parameter.

5. Forward request.

6. Observe response.

7. Identify vulnerability.

---

# Common Vulnerabilities

## Parameter Tampering

Example:

```text
price=100
```

changed to:

```text
price=1
```

---

## Broken Access Control

Accessing unauthorized resources.

---

## IDOR

Example:

```text
/employee/100
```

changed to:

```text
/employee/101
```

Another user's data appears.

---

## SQL Injection

Inject SQL queries through inputs.

---

## Cross-Site Scripting

Inject malicious JavaScript.

---

# Practical Demonstration

Lab Environment:

## Kali Linux

Attacker Machine

---

## Metasploitable

Victim Machine

---

# Commands Used

View interfaces:

```bash
ifconfig
```

View ARP cache:

```bash
arp -a
```

Discover hosts:

```bash
sudo arp-scan --localnet
```

Check connectivity:

```bash
ping google.com
```

Enable forwarding:

```bash
echo 1 | sudo tee /proc/sys/net/ipv4/ip_forward
```

---
# Practical Demonstration – Kali Linux and Metasploitable Lab

The instructor demonstrated the concepts using two virtual machines:

### Kali Linux

Role:

```text
Attacker Machine
```

Purpose:

- Perform host discovery
- View ARP tables
- Enable packet forwarding
- Prepare for ARP poisoning
- Observe traffic

---

### Metasploitable

Role:

```text
Victim Machine
```

Purpose:

- Simulate a vulnerable host
- Verify connectivity
- Observe ARP cache changes

---

# Step 1 – Identify Kali Linux Network Configuration

Command:

```bash
ifconfig
```

Output:

```text
IP Address  : 10.0.2.15
MAC Address : 08:00:27:95:b9:e6
Interface   : eth0
```

This machine acts as the attacker.

Important observations:

- IP address identifies Kali logically.
- MAC address identifies Kali physically.
- Both values are required during ARP poisoning.

---

# Step 2 – Identify Metasploitable Network Configuration

Command:

```bash
ifconfig
```

Output:

```text
IP Address  : 10.0.2.3
MAC Address : 08:00:27:00:5d:6a
Interface   : eth0
```

This machine acts as the victim.

---

# Step 3 – Discover Hosts Using ARP Scan

Command:

```bash
sudo arp-scan --localnet
```

Purpose:

Perform Layer 2 host discovery.

Output:

```text
10.0.2.1
MAC: 52:55:0a:00:02:01

10.0.2.2
MAC: 08:00:27:56:90:7c

10.0.2.3
MAC: 08:00:27:00:5d:6a
```

---

# Interpretation of Results

## Gateway

```text
IP  : 10.0.2.1
MAC : 52:55:0a:00:02:01
```

Represents the router/default gateway.

---

## Another Host

```text
IP  : 10.0.2.2
MAC : 08:00:27:56:90:7c
```

Likely another VM or VirtualBox component.

---

## Metasploitable Victim

```text
IP  : 10.0.2.3
MAC : 08:00:27:00:5d:6a
```

Matches the victim machine.

---

# Why ARP Scan Was Used

ARP scan is preferred because:

- Every active host must answer ARP.
- ICMP may be blocked.
- It reveals both IP and MAC addresses.

This information is essential before ARP poisoning.

---

# Step 4 – Examine Kali ARP Cache

Command:

```bash
arp -a
```

Output:

```text
10.0.2.1 → 52:55:0a:00:02:01
10.0.2.2 → 08:00:27:56:90:7c
10.0.2.3 → 08:00:27:00:5d:6a
```

Purpose:

View IP-to-MAC mappings already learned by Kali.

---

# Step 5 – Verify Internet Connectivity from Victim

On Metasploitable:

Command:

```bash
ping google.com
```

Output:

```text
3 packets transmitted
3 packets received
0% packet loss
```

Meaning:

```text
Victim → Gateway → Internet
```

communication is functioning correctly.

Before performing MITM attacks, connectivity must be verified.

---

# Step 6 – Inspect Victim ARP Cache

On Metasploitable:

Command:

```bash
arp -a
```

Output:

```text
10.0.2.1 at 52:55:0a:00:02:01
```

Interpretation:

Victim correctly believes:

```text
Gateway IP
10.0.2.1

belongs to

52:55:0a:00:02:01
```

This serves as the baseline before poisoning.

---

# Step 7 – Enable IP Forwarding on Kali

Command:

```bash
echo 1 | sudo tee /proc/sys/net/ipv4/ip_forward
```

Output:

```text
1
```

Meaning:

```text
IP Forwarding Enabled
```

Linux now behaves like a router.

---

# Why IP Forwarding Is Necessary

Without forwarding:

```text
Victim
 ↓
Kali
 X

Internet Stops
```

Victim immediately notices.

With forwarding:

```text
Victim
 ↓
Kali
 ↓
Gateway
 ↓
Internet
```

Traffic continues normally.

This is essential for maintaining a stealthy MITM attack.

---

# Complete Attack Preparation Flow

Step 1

Identify attacker:

```text
Kali
10.0.2.15
08:00:27:95:b9:e6
```

↓

Step 2

Identify victim:

```text
Metasploitable
10.0.2.3
08:00:27:00:5d:6a
```

↓

Step 3

Identify gateway:

```text
10.0.2.1
52:55:0a:00:02:01
```

↓

Step 4

Perform ARP scan

↓

Step 5

Verify connectivity

↓

Step 6

Inspect ARP caches

↓

Step 7

Enable IP forwarding

↓

Step 8

Ready for ARP poisoning and MITM

---

# Observed Memory Issue

Metasploitable displayed:

```text
Out of memory:
Kill process xxxx (jsvc)
```

This is unrelated to ARP poisoning.

Reason:

Metasploitable was running with low memory.

Linux OOM Killer terminated processes to reclaim memory.

This behavior is common in low-RAM virtual machines.

# Session Summary

Session 6 connected networking and web security. Beginning with MAC addresses and ARP, the session moved into host discovery, MITM attacks, ARP poisoning, practical demonstrations using Kali and Metasploitable, DoS and DDoS concepts, and finally introduced HTTP and Burp Suite. The session established the foundation necessary for later topics such as SQL Injection, IDOR, XSS, authentication flaws, and web application penetration testing.

---
