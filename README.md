# 🔍 Reconnaissance, Footprinting & Enumeration
---

## 📌 Table of Contents
1. Introduction & Scope
2. Reconnaissance Mindset
3. Overall Methodology
4. Passive Reconnaissance (Deep)
5. Active Reconnaissance (Deep)
6. Enumeration (Very Deep)
7. Analysis & Attack Surface Mapping
8. Documentation & Reporting
9. Mentor Instructions → Exact Actions
10. Legal Practice Targets
11. Time-Efficient Daily Workflow

---

## 1. Introduction & Scope

Reconnaissance and Enumeration form the foundation of penetration testing.

A weak recon phase results in missed vulnerabilities.
A strong recon phase makes exploitation straightforward.

This document explains:
- What to run
- Why to run it
- How it works
- How to analyze results
- How findings lead to exploitation later

Suitable for:
- Cybersecurity internships
- Bug bounty foundations
- Penetration testing certifications
- Professional portfolios

---

## 2. Reconnaissance Mindset (Critical)

Always think like a professional tester:

- Recon is information gathering, not exploitation
- Quality > Quantity
- Every output must answer: "How can this be abused later?"

Core Questions:
1. What systems exist?
2. How do they communicate?
3. Where does user input enter the system?

---

## 3. Overall Methodology

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

## 4. Passive Reconnaissance (Deep)
(No direct interaction with target infrastructure)

---

### 4.1 WHOIS Enumeration

Command:
whois example.com

Analyze:
- Organization name
- Registrar
- Name servers
- Admin / abuse emails
- IP ranges or CIDR blocks

Why it matters:
- Large IP ranges = more assets
- Exposed emails = OSINT & phishing vectors

---

### 4.2 DNS Intelligence (nslookup & dig)

nslookup:
nslookup example.com

dig:
dig example.com any

Look for:
- A / AAAA records
- MX records
- TXT records (SPF, DKIM, DMARC, tokens)

Why it matters:
- DNS misconfig = subdomain takeover
- Weak mail config = spoofing

---

### 4.3 Subdomain Enumeration (Passive)

Commands:
subfinder -d example.com
assetfinder example.com

High-value subdomains:
- dev.example.com
- test.example.com
- staging.example.com
- admin.example.com

---

### 4.4 Technology Fingerprinting

Command:
whatweb example.com

Analyze:
- Web server (Apache, Nginx, IIS)
- CMS (WordPress, Drupal)
- Frameworks
- WAF / CDN

---

### 4.5 Search Engine & OSINT Recon

Google Dorks:
site:example.com
site:example.com inurl:login
site:example.com inurl:admin
site:example.com filetype:pdf
intitle:"index of"

Look for:
- Login portals
- Backup files
- Internal docs
- Directory listing

---

## 5. Active Reconnaissance (Deep)
(Limited & controlled interaction)

---

### 5.1 Host Discovery

ping example.com

Note:
ICMP blocked ≠ host down

---

### 5.2 Port Scanning

Initial scan:
nmap -Pn example.com

Fast scan:
nmap -T4 -F example.com

Why it matters:
Each open port = entry point

---

### 5.3 Service & Version Detection

Command:
nmap -sV example.com

Analyze:
- Service name
- Version number

Why it matters:
Versions enable CVE mapping

---

## 6. Enumeration (Very Deep)

---

### 6.1 Aggressive Enumeration

Command:
nmap -A example.com

Includes:
- OS detection
- NSE scripts
- Extended service details

---

### 6.2 Web Directory & File Enumeration

Dirb:
dirb http://example.com

Gobuster:
gobuster dir -u http://example.com -w /usr/share/wordlists/dirb/common.txt

Finds:
- Admin panels
- Backup files
- Upload points

---

### 6.3 HTTP Header & Cookie Analysis

Command:
curl -I http://example.com

Analyze:
- Server disclosure
- Missing security headers
- Cookie flags (Secure, HttpOnly, SameSite)

---

### 6.4 Parameter Discovery

Examples:
example.com/page.php?id=1
example.com/search?q=test

Why parameters matter:
- Main injection points
- Used for SQLi, XSS, Command Injection

---

## 7. Analysis & Attack Surface Mapping

Ask:
- Which services should not be public?
- Which inputs accept user data?
- Which components are outdated?

This phase separates professionals from tool-runners.

---

## 8. Documentation & Reporting

Recon Report Template:

Target Overview:
- Domain:
- IP Address:
- Scope:

Passive Recon:
- Subdomains
- DNS records
- Technologies

Active Recon:
- Open ports
- Services & versions

Enumeration:
- Directories
- Parameters
- Header issues

Potential Attack Surface:
- Injection
- Authentication
- Misconfiguration

---

## 9. Mentor Instructions → Exact Actions

Mentor says: Do recon → You execute sections 4 & 5  
Mentor says: Enumerate → You execute section 6  
Mentor says: Submit report → You follow section 8  

---

## 10. Legal Practice Targets

- bWAPP
- DVWA
- OWASP Juice Shop
- TryHackMe
- Hack The Box Academy

---

## 11. Time-Efficient Daily Workflow

- Recon & Enumeration: 40 minutes
- Documentation: 20 minutes
- Review & Notes: 10 minutes

---

## Final Statement

This README represents a real-world reconnaissance and enumeration methodology suitable for internships, certifications, and professional penetration testing portfolios.

Master recon first — exploitation becomes logical, not guesswork.
