Reconnaissance, Footprinting & Enumeration

> Industry‑Standard, Deep‑Dive GitHub README
Audience: Cybersecurity / Penetration Testing Interns (Beginner → Intermediate)
Purpose: This document is designed so that when an organization or mentor says "Perform reconnaissance or enumeration", you can execute the task independently, confidently, and professionally — without step‑by‑step classroom guidance.




---

📌 Scope & Ethics

Perform recon only on authorized targets (labs, written permission, training environments).

Reconnaissance ≠ exploitation. This phase focuses on information gathering and attack surface mapping.

This methodology follows real‑world penetration testing workflows used in professional engagements.



---

🧠 Core Reconnaissance Philosophy

Always answer these three questions:

1. What assets exist? (domains, IPs, subdomains, services)


2. What is exposed? (ports, directories, parameters, versions)


3. What is potentially vulnerable? (misconfigurations, outdated services, weak entry points)



Reconnaissance quality directly determines exploitation success.


---

🗺️ High‑Level Workflow

Target Definition
      ↓
Passive Reconnaissance
      ↓
Active Reconnaissance
      ↓
Enumeration (Deep Inspection)
      ↓
Analysis & Attack Surface Mapping
      ↓
Documentation & Reporting

Never skip steps.


---

1️⃣ Passive Reconnaissance (No Direct Target Interaction)

1.1 Domain & Ownership Intelligence

Objective: Identify ownership, infrastructure hints, and administrative metadata.

whois example.com

Analyze:

Registrar and organization name

Name servers

Contact emails (useful for OSINT)

IP ranges or CIDR blocks



---

1.2 DNS Intelligence Gathering

nslookup example.com
dig example.com any

Collect and document:

A / AAAA records (IPv4 / IPv6)

MX records (mail servers)

TXT records (SPF, DKIM, DMARC, verification tokens)


Misconfigured DNS often leads to takeover vulnerabilities.


---

1.3 Subdomain Enumeration (Passive)

Why it matters: Development, staging, and legacy subdomains frequently lack proper security controls.

subfinder -d example.com
assetfinder example.com

Flag high‑value targets:

dev.example.com

staging.example.com

test.example.com

admin.example.com



---

1.4 Technology Fingerprinting

whatweb example.com

Identify:

Web server (Apache, Nginx, IIS)

CMS (WordPress, Joomla, Drupal)

Frameworks (Laravel, Django, Express)

Analytics, WAFs, third‑party services


Technology mapping guides vulnerability selection.


---

1.5 Search Engine & OSINT Reconnaissance

Common queries:

site:example.com
site:example.com inurl:login
site:example.com inurl:admin
site:example.com filetype:pdf
intitle:"index of"

Look for:

Exposed admin panels

Backup files

Internal documents

Directory listings



---

2️⃣ Active Reconnaissance (Minimal Interaction)

2.1 Host Availability Check

ping example.com

ICMP blocked ≠ host down. Continue regardless.


---

2.2 Port Scanning (Initial)

nmap -Pn example.com

Fast scan:

nmap -T4 -F example.com

Document open ports only.


---

2.3 Service & Version Enumeration

nmap -sV example.com

Why this matters:

Version numbers enable CVE correlation

Legacy services often lack patches



---

3️⃣ Enumeration (Critical Phase 🔥)

3.1 Aggressive Enumeration Scan

nmap -A example.com

Includes:

OS fingerprinting

Default NSE scripts

Service detail expansion



---

3.2 Web Directory & File Enumeration

Using Dirb

dirb http://example.com

Using Gobuster

gobuster dir -u http://example.com -w /usr/share/wordlists/dirb/common.txt

Focus on:

/admin

/login

/dashboard

/backup

/uploads

/config



---

3.3 HTTP Header Enumeration

curl -I http://example.com

Inspect:

Server disclosure

Missing security headers

Cookie flags (HttpOnly, Secure)



---

3.4 Parameter Discovery (Manual)

Example patterns:

example.com/index.php?id=1
example.com/search?q=test

Classify parameters:

GET parameters

POST parameters


These become injection candidates later.


---

4️⃣ Analysis & Attack Surface Mapping

Ask critical questions:

Which services should not be public?

Which directories expose sensitive functionality?

Are there outdated or uncommon services?

Where is user input accepted?


This phase differentiates professionals from tool‑runners.


---

5️⃣ Documentation & Reporting (Industry Standard)

5.1 Reconnaissance Report Template

Target Overview
---------------
Domain:
IP Address:
Scope:

Passive Reconnaissance
---------------------
Subdomains:
Technologies Identified:
DNS Findings:

Active Reconnaissance
---------------------
Open Ports:
Services & Versions:

Enumeration Findings
-------------------
Directories Discovered:
Login Interfaces:
Parameters Identified:

Potential Attack Surface
------------------------
(SQL Injection, XSS, Auth Issues, Misconfiguration, etc.)

Clear documentation = professional credibility.


---

6️⃣ Common Internship Instructions → Your Actions

Mentor Instruction	What You Execute

"Do recon"	Sections 1 & 2
"Enumerate the target"	Section 3
"Give findings"	Section 5



---

7️⃣ Legal Practice Environments

bWAPP

DVWA

OWASP Juice Shop

TryHackMe

Hack The Box (Academy / Labs)



---

8️⃣ Time‑Efficient Daily Practice (Ramadan‑Friendly)

Recon & enumeration: 30–40 minutes

Documentation: 15–20 minutes

Consistency > duration



---

✅ Final Note

Mastering reconnaissance and enumeration ensures:

Faster vulnerability discovery

Strong technical interviews

Professional internship performance


This README is portfolio‑ready and industry‑aligned.

➡️ Next upgrades available:

OWASP Top 10 mapping from recon output

NSDA Level‑4 exam‑focused recon checklist

Real‑world penetration testing report sample
