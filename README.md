Reconnaissance, Footprinting & Enumeration

> Industry‑Standard Deep Reconnaissance Playbook
---

Table of Contents

1. Introduction & Scope


2. Reconnaissance Mindset


3. Overall Methodology


4. Passive Reconnaissance (Deep)

WHOIS

DNS Intelligence (nslookup, dig)

Subdomain Enumeration

Technology Fingerprinting

Search Engine & OSINT



5. Active Reconnaissance (Deep)

Host Discovery

Port Scanning

Service & Version Detection



6. Enumeration (Very Deep)

Nmap Advanced Usage

Web Enumeration

Directory & File Discovery

Header & Cookie Analysis

Parameter Discovery



7. Analysis & Attack Surface Mapping


8. Documentation & Reporting (Industry Standard)


9. Mentor Instructions → Your Exact Actions


10. Legal Practice Targets


11. Time‑Efficient Daily Workflow




---

1. Introduction & Scope

Reconnaissance and enumeration form the foundation of penetration testing.
A weak recon phase results in missed vulnerabilities; a strong recon phase makes exploitation straightforward.

This document explains what to run, why to run it, how it works, and how to interpret results.


---

2. Reconnaissance Mindset (Critical)

Always think like this:

Recon is information gathering, not exploitation

Quality > quantity

Every output must answer: How can this be abused later?


Core questions:

1. What systems exist?


2. How do they communicate?


3. Where does user input enter the system?




---

3. Overall Methodology

Target Definition
  ↓
Passive Reconnaissance
  ↓
Active Reconnaissance
  ↓
Enumeration
  ↓
Analysis
  ↓
Documentation

Never jump directly to exploitation.


---

4. Passive Reconnaissance (Deep)

> No direct interaction with the target infrastructure




---

4.1 WHOIS Enumeration

Why WHOIS is used

Identifies ownership and administrative control

Reveals registrar, organization, and sometimes internal email addresses

Helps understand target size and infrastructure


Command

whois example.com

What to analyze

Organization name

Name servers

Abuse / admin emails

IP ranges or CIDR blocks


Why it matters

Large IP ranges → multiple assets

Exposed emails → OSINT & phishing potential



---

4.2 DNS Intelligence (nslookup & dig)

Why DNS enumeration is important

DNS records often leak:

Internal services

Mail infrastructure

Verification tokens

Misconfigurations


nslookup (basic & quick)

nslookup example.com

Use when you need:

Quick A record resolution

Simple MX lookup


dig (advanced & detailed)

dig example.com any

What to look for

A / AAAA records → IP mapping

MX records → mail servers

TXT records → SPF, DKIM, DMARC, API keys, verification strings


Why it matters

Misconfigured DNS → subdomain takeover, email spoofing


---

4.3 Subdomain Enumeration (Passive)

Why subdomains are critical

Often hosted separately

Frequently less monitored

Dev/test environments are common targets


Commands

subfinder -d example.com
assetfinder example.com

High‑value subdomains

dev.example.com

test.example.com

staging.example.com

admin.example.com



---

4.4 Technology Fingerprinting

Purpose

Identify software stack

Map potential vulnerabilities


Command

whatweb example.com

Analyze

Web server (Apache, Nginx, IIS)

CMS (WordPress, Drupal)

Frameworks (Laravel, Django)

Security controls (WAF, CDN)



---

4.5 Search Engine & OSINT Recon

Why this works

Search engines index data developers forget to protect.

Common Queries

site:example.com
site:example.com inurl:login
site:example.com inurl:admin
site:example.com filetype:pdf
intitle:"index of"

Look for

Login portals

Backup files

Internal documentation

Directory listing exposure



---

5. Active Reconnaissance (Deep)

> Limited, controlled interaction with the target




---

5.1 Host Discovery

ping example.com

Note

ICMP blocking is common — absence of reply ≠ host down


---

5.2 Port Scanning

Initial scan

nmap -Pn example.com

Fast scan (top ports)

nmap -T4 -F example.com

Why port scanning matters

Each open port = potential entry point



---

5.3 Service & Version Detection

nmap -sV example.com

Analyze

Service name

Version number


Why it matters

Versions allow CVE mapping and exploit research


---

6. Enumeration (Very Deep)

6.1 Aggressive Enumeration

nmap -A example.com

Includes:

OS detection

Default NSE scripts

Extended service information



---

6.2 Web Directory & File Enumeration

Dirb

dirb http://example.com

Gobuster

gobuster dir -u http://example.com -w /usr/share/wordlists/dirb/common.txt

Why this matters

Hidden directories often expose:

Admin panels

Backups

Upload points



---

6.3 HTTP Header & Cookie Analysis

curl -I http://example.com

Analyze:

Server disclosure

Missing security headers

Cookie flags (Secure, HttpOnly)



---

6.4 Parameter Discovery

Examples

example.com/page.php?id=1
example.com/search?q=test

Why parameters matter

Primary injection points

Used later for SQLi, XSS, command injection



---

7. Analysis & Attack Surface Mapping

Ask:

Which services should not be public?

Which inputs accept user data?

Which components are outdated?


This phase separates professionals from tool‑runners.


---

8. Documentation & Reporting

Recon Report Template

Target Overview
Domain:
IP Address:
Scope:

Passive Recon Findings
- Subdomains:
- DNS Records:
- Technologies:

Active Recon Findings
- Open Ports:
- Services & Versions:

Enumeration Findings
- Directories:
- Parameters:
- Headers Issues:

Potential Attack Surface
- Injection
- Authentication
- Misconfiguration


---

9. Mentor Instructions → Your Action

Mentor Says	You Execute

Do recon	Sections 4 & 5
Enumerate	Section 6
Submit report	Section 8



---

10. Legal Practice Targets

bWAPP

DVWA

OWASP Juice Shop

TryHackMe

Hack The Box (Academy)



---

11. Time‑Efficient Daily Workflow

Recon & enumeration: 40 minutes

Documentation: 20 minutes

Review & notes: 10 minutes



---

Final Statement

This README represents a real‑world reconnaissance and enumeration methodology suitable for internships, certifications, and professional portfolios.
