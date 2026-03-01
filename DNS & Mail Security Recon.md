# 🧠 DNS & Mail Security Recon – FINAL CHEATSHEET

---

## 🌐 DNS Record Basics

### A Record
Purpose: Maps a domain name to an IPv4 address  
Used to identify: Web server location  

Attacker Focus:
- Direct IP access
- CDN / WAF bypass attempts
- Shared hosting detection

Example:
example.com → 93.184.216.34

---

### AAAA Record (IPv6)
Purpose: Maps a domain name to an IPv6 address  

Why it matters:
- IPv6 is often less monitored
- Firewalls may protect IPv4 but not IPv6

Attacker Focus:
- Hidden services exposed over IPv6
- Firewall misconfigurations

Example:
example.com → 2606:2800:220:1:248:1893:25c8:1946

---

### MX Record
Purpose: Defines where emails for the domain are delivered  

Attacker Focus:
- Mail server provider (Google, Microsoft, custom)
- Phishing and email spoofing potential

Example:
example.com → mail.example.com

---

### CNAME Record
Purpose: Creates an alias pointing to another domain  

Why it matters:
- Commonly used with cloud services and SaaS
- High risk of subdomain takeover if misconfigured

Attacker Focus:
- Third-party dependency mapping
- Subdomain takeover opportunities

Example:
app.example.com → example.azurewebsites.net

---

### NS Record (Name Server)
Purpose: Identifies which servers control the domain’s DNS  

Why it matters:
- Reveals DNS provider
- Helps identify DNS misconfigurations

Attacker Focus:
- Infrastructure mapping
- DNS takeover scenarios

Example:
example.com → ns1.cloudflare.com

---

### SOA Record (Start of Authority)
Purpose: Contains DNS administrative metadata  

Why it matters:
- May expose admin email
- Helps identify misconfigurations and zone control

Attacker Focus:
- OSINT enrichment
- DNS management insights

---

### TXT Record (Most Important)
Purpose: Stores text-based information for the domain  

Common Uses:
- Mail security rules (SPF, DKIM, DMARC)
- Verification tokens
- Cloud / SaaS ownership proof

---

## 📧 Mail Security Records

### SPF (Sender Policy Framework)
Purpose: Specifies which servers are allowed to send emails for the domain  

Strong SPF:
v=spf1 include:_spf.google.com -all  

Weak SPF:
v=spf1 ~all  
No SPF record

Risk if weak or missing:
- Email spoofing
- Phishing attacks

---

### DKIM (DomainKeys Identified Mail)
Purpose: Verifies that email content was not altered in transit  

Strong DKIM:
- DKIM record present
- Valid digital signature

Weak DKIM:
- DKIM missing
- Signature verification fails

Risk:
- Fake emails appear legitimate

---

### DMARC (Domain-based Message Authentication, Reporting & Conformance)
Purpose: Defines what to do if SPF or DKIM checks fail  

Policies:
p=none       → Weak  
p=quarantine → Medium  
p=reject     → Strong  

Risk if weak:
- Spoofed emails delivered
- Brand impersonation

---

## 🧱 High-Risk DNS Findings

### Internal / Hidden Subdomains
Examples:
- dev.example.com
- test.example.com
- staging.example.com
- admin.example.com

Why risky:
- Weak authentication
- Debug mode enabled
- Outdated or unfinished code

---

### Verification Tokens (TXT Records)
Examples:
- google-site-verification
- MS=msxxxx
- facebook-domain-verification

Attacker Insight:
- Identify cloud providers
- Map third-party integrations
- Expand attack surface

---

## 🚨 Weak Mail Security Indicators

- SPF missing or using ~all
- DKIM missing
- DMARC policy set to p=none

Possible Attacks:
- Email spoofing
- Password reset abuse
- Invoice fraud
- Social engineering campaigns

---

## 🧠 How to Analyze DNS Like a Pentester

Ask these questions:
- Are mail protections enforced or relaxed?
- Are subdomains pointing to third-party services?
- Are dev/staging assets publicly exposed?
- Does IPv6 expose services hidden on IPv4?
- Are DNS records revealing unnecessary information?

---

## 🧠 Quick Memory Guide

A Record      → Website location  
AAAA Record   → IPv6 exposure  
MX Record     → Mail server location  
CNAME         → Alias / takeover risk  
NS            → DNS control  
SPF           → Who can send emails  
DKIM          → Email authenticity  
DMARC         → Action on failure  
Subdomain     → Hidden entry point  
TXT Token     → Third-party integration clue  

---

## 🛠 Common Recon Commands

nslookup example.com  
dig example.com any  

---

## ✅ Skill Completion Checklist

You are ready if you can:
- Identify dangerous DNS configurations
- Explain mail security weaknesses
- Detect takeover and spoofing risks
- Document DNS findings in a recon report

---

## 🔚 Final Note

DNS exposes infrastructure.
Professionals read DNS as a map.
Attackers read DNS as an attack blueprint.
