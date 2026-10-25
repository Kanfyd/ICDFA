# GRC103 Lab 1: Practical Vulnerability Assessment Report

## Student & Assessment Metadata
- **Student Name:** Confidence Chinwuko
- **Course Code:** GRC103
- **Registration Number:** C11-26-CGRCE-17558
- **Target Host IP (Metasploitable):** `192.168.56.102`
- **Attacker Host IP (Kali Linux):** `192.168.56.101`
- **Assessment Date:** October 2026
- **Tools Utilized:** Nmap (v7.99), Nikto (v2.6.1), Nuclei (v3.11.1), xsltproc, Ping

---

## Phase 1: Network Discovery & Asset Verification

### 1.1 Host Reachability (Ping)
To establish foundational asset inventory control and verify connectivity to the designated development environment test server, an ICMP echo request ping was executed from the Kali Linux attacker instance against the target IP (`192.168.56.102`).

- **Command Executed:**
  ```bash
  ping -c 4 192.168.56.102
  ```
- **Execution Result:** 4 packets transmitted, 4 received successfully with **0% packet loss**, confirming that the target host is active and accessible on the isolated Host-Only network.
- **GRC Alignment:** Fulfills baseline asset identification requirements under **NIST CSF (ID.AM-1)** and **CIS Control 1**, ensuring complete visibility over active enterprise assets.

---

## Phase 2: Port & Service Enumeration (Nmap Assessment)

### 2.1 Scan Execution & Multi-Format Output
A comprehensive port sweep and service version enumeration scan was executed across all 65,535 TCP ports on the target host. The outputs were saved in standard formats (`.nmap`, `.xml`, `.gnmap`) and transformed into an interactive HTML visualization report.

- **Commands Executed:**
  ```bash
  nmap -sV -sC -O -p- -oA scannings/initial_scan 192.168.56.102
  xsltproc -o scannings/initial_scan_report.html /usr/share/nmap/nmap.xsl scannings/initial_scan.xml
  ```

### 2.2 Summary of Discovered Open Ports & Services
The Nmap scan revealed a severe proliferation of active services, unnecessary legacy protocols, and unpatched software versions:
* **Port 21/tcp:** `ftp` – `vsftpd 2.3.4` (Anonymous FTP allowed; known backdoor command execution vulnerability).
* **Port 22/tcp:** `ssh` – `OpenSSH 4.7p1 Debian 8ubuntu1` (Protocol 2.0).
* **Port 23/tcp:** `telnet` – `Linux telnetd` (Unencrypted plaintext administrative management).
* **Port 25/tcp:** `smtp` – `Postfix smtpd`.
* **Port 53/tcp:** `domain` – `ISC BIND 9.4.2`.
* **Port 80/tcp:** `http` – `Apache httpd 2.2.8 ((Ubuntu) DAV/2)` (Metasploitable2 web root).
* **Port 111/tcp:** `rpcbind` – Version 2 (RPC #100000).
* **Ports 139/445/tcp:** `netbios-ssn` – `Samba smbd 3.X - 4.X` (SMB file sharing services).
* **Port 1524/tcp:** `bindshell` – `Metasploitable root shell` (Active unauthenticated root shell listener).
* **Port 2049/tcp:** `nfs` – Network File System (RPC #100003).
* **Port 2121/tcp:** `ftp` – `ProFTPD 1.3.1`.
* **Port 3306/tcp:** `mysql` – `MySQL 5.0.51a-3ubuntu5`.
* **Port 3632/tcp:** `distccd` – `distccd v1 ((GNU) 4.2.4)` (Remote code execution vulnerability vector).
* **Port 5432/tcp:** `postgresql` – `PostgreSQL DB 8.3.0 - 8.3.7`.
* **Port 5900/tcp:** `vnc` – VNC server (Protocol 3.3).
* **Port 6667/6697/tcp:** `irc` – `UnrealIRCd`.
* **Port 8180/tcp:** `http` – `Apache Tomcat/Coyote JSP engine 1.1`.

---

## Phase 3: Vulnerability Identification (Nikto & Nuclei Assessment)

### 3.1 Web Application Assessment (Nikto)
A targeted vulnerability scan of the web application running on port 80 (`Apache/2.2.8`) was executed using Nikto to uncover server misconfigurations, outdated components, and sensitive directory exposures.

- **Command Executed:**
  ```bash
  nikto -h http://192.168.56.102 -o scannings/nikto_scan.txt
  ```
- **Key Findings from Nikto Output (`nikto_scan.txt`):**
  - **Outdated Web Stack:** Identified `Apache/2.2.8` and `PHP/5.2.4-2ubuntu5.10`, both of which contain multiple unpatched vulnerabilities and are significantly out of date.
  - **Information Disclosure (PHP Easter Eggs & phpinfo):** Discovered sensitive query strings (`?=-PHPE9568F36-...`) and exposed `phpinfo.php` output, revealing detailed system configurations and internal path structures.
  - **Exposed Management Consoles:** Confirmed directory indexing enabled on `/test/`, `/doc/`, and identified `phpMyAdmin/changelog.php`, presenting potential enumeration vectors for attackers.
  - **Security Header Deficiencies:** Flagged missing security headers across HTTP responses (such as `X-Content-Type-Options`, `X-Frame-Options`, and Content-Security-Policy), increasing susceptibility to clickjacking and MIME-sniffing attacks.

### 3.2 Template-Based Vulnerability Scanning (Nuclei)
Automated template scanning was initiated against the target web application and system ports.

- **Commands Executed:**
  ```bash
  nuclei -u http://192.168.56.102 -o scannings/nuclei_web_scan.txt
  nuclei -target 192.168.56.102 -o scannings/nuclei_full_scan.txt
  ```
- **Execution Observation & Technical Context:** 
  - The scans initialized `Nuclei v3.11.1`, but encountered template path limitations (`[FTL] Could not run nuclei: no templates provided for scan`) due to the offline, isolated nature of the Host-Only laboratory environment which restricts external GitHub repository synchronization. 
  - In alignment with GRC audit principles, unverified automated checks were noted, and risk analysis was successfully anchored on confirmed empirical evidence derived from Nmap and Nikto scan outputs.

---

## Phase 4: Risk Assessment & Compliance Triage

| Finding / Vulnerability | Affected Service & Port | CVE / Reference | Inherent Risk | Compliance Violation | Business Impact |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **vsFTPd 2.3.4 Backdoor** | FTP (`Port 21`) | CVE-2011-2523 | **High** | CIS Control 7.1 (Patch Management), NIST CSF PR.IP-1 | Allows unauthenticated remote execution yielding immediate root-level system takeover. |
| **Active Unauthenticated Bind Shell** | Bindshell (`Port 1524`) | N/A (Misconfiguration) | **High** | CIS Control 4.1 (Secure Configuration), NIST CSF PR.PT-1 | Direct, unauthenticated entry point granting complete administrative privileges to any local network user. |
| **Unencrypted Telnet Management** | Telnet (`Port 23`) | N/A (Legacy Protocol) | **High** | NIST CSF PR.DS-2 (Data Security), PCI DSS Req 2.2.4 | Transmits credentials and administrative session data in plaintext, exposing systems to credential sniffing. |
| **Outdated Web Stack & PHP Flaws** | HTTP (`Port 80`), PHP (`Port 80`) | CVE-1999-0678, Multiple CVEs | **Medium** | PCI DSS Req 6.4 (Change Control), OWASP Top 10 A05:2021 | Exposes sensitive server configuration data (`phpinfo`) and software vulnerabilities to web attackers. |
| **Anonymous FTP Access Enabled** | FTP (`Port 21`) | N/A (Misconfiguration) | **Medium** | CIS Control 3.3 (Data Protection), NIST CSF PR.AC-3 | Exposes sensitive development file stores and directory contents to unauthorized unauthenticated users. |
| **Proliferation of Unneeded Daemons** | Multiple Ports (e.g., 3632/distccd) | CVE-2004-2687 | **High** | CIS Control 2.2 (Software Asset Inventory), NIST CSF ID.AM-2 | Increases corporate attack surface by maintaining legacy development services in active production/test boundaries. |

---

## Phase 5: Management Executive Summary

**To:** IT Management & Infrastructure Steering Committee  
**From:** GRC Audit Team (Confidence Chinwuko)  
**Date:** October 2026  
**Subject:** Technical Vulnerability Assessment & Compliance Review – Development Server (`192.168.56.102`)

### 1. Executive Summary
A comprehensive technical vulnerability assessment was conducted on the internal development server (`metasploitable`). The evaluation combined network discovery, port enumeration, and web application profiling to determine overall security posture and regulatory alignment. The assessment identified critical remote execution vectors, persistent backdoor accounts, unencrypted administrative protocols, and widespread baseline configuration failures that pose immediate, catastrophic risk to organizational information assets.

### 2. Key Findings & Business Risks
- **Critical Risk – Unauthenticated Remote Compromise:** The FTP service runs an intentionally vulnerable release (`vsFTPd 2.3.4`) containing a known remote backdoor, alongside an active unauthenticated root bind shell on port 1524. An attacker can achieve complete system ownership without credentials, violating foundational patch management and secure baseline mandates (**CIS Control 7.1**).
- **High Risk – Data Interception & Credential Sniffing:** Legacy management protocols (Telnet on port 23) transmit all session tokens and administrative credentials in plaintext across the internal network, directly breaching data protection requirements (**NIST CSF PR.DS-2** and **PCI DSS Req 2.2.4**).
- **High Risk – Unmitigated Attack Surface Expansion:** The server exposes over 30 open listening ports running unneeded development services, database engines, and legacy remote execution daemons, violating the principle of least functionality (**CIS Control 4**).
- **Medium Risk – Web Application Misconfigurations:** Nikto web scans identified exposed phpinfo files, outdated Apache/PHP frameworks, and missing security headers, creating information disclosure pathways that could assist malicious actors in staging further attacks.

### 3. Strategic Remediation Roadmap
1. **Immediate Host Isolation:** Disconnect the target development server from the active internal network immediately to prevent lateral movement or automated exploitation.
2. **Protocol Hardening & Service Decommissioning:** Permanently disable legacy unencrypted protocols (Telnet) and unnecessary daemons. Enforce encrypted alternatives such as SSH key-based authentication only.
3. **Patch Management & Software Modernization:** Upgrade all third-party packages, web servers (`Apache/2.2.8`), and FTP daemons to vendor-supported, patched releases.
4. **Baseline Compliance Review:** Institute automated vulnerability scanning gates in the CI/CD pipeline to ensure future development servers strictly conform to corporate security baselines before network activation.


Evidence Scans in the link... https://docs.google.com/document/d/1hL_Om8f-lbQNuPg8RFfbGj0B2iOCduce7E-w9Spr9Zo/edit?usp=sharing
