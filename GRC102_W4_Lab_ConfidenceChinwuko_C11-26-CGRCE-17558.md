# INTERNATIONAL CYBERSECURITY AND DIGITAL FORENSICS ACADEMY

## GRC102: Information Security Governance — Module 4

### Week 4 Practical Laboratory: Linux Security Monitoring and Auditing (From Technical Evidence to Governance Assurance)

* **Student Name:** Confidence Chinwuko
* **Registration Number:** C11-26-CGRCE-17558
* **Course / Module:** GRC102 — Information Security Governance
* **Target Environment:** Kali Linux (`kali@kali` VM)
* **Date of Execution:** October 2026
* **Submission Mode:** GitHub Markdown (`README.md`)

---

## 1. Executive Summary

This laboratory evaluation examines the security posture, kernel auditing subsystem, log management configurations, and system hardening state of an assigned Linux workload operating on **Kali Linux** (`kali@kali`). Using native auditing tools (`auditd`), system log interfaces (`journalctl`), and automated system assessment utilities (`Lynis`), technical evidence was extracted, analyzed, and translated into continuous control monitoring and governance metrics.

### Key Audit Findings & Posture Summary

1. **Unmonitored System Integrity (Audit Subsystem Deficiencies):** The Linux auditing subsystem (`auditd`) was initially missing from the system. Custom watch rules monitoring `/etc/passwd`, `/etc/shadow`, and program execution (`execve`) were deployed, verified, and queried.
2. **Missing Legacy Syslog Infrastructure:** Attempts to access `/var/log/syslog` and `/var/log/auth.log` confirmed that default Kali Linux relies exclusively on binary `systemd-journald` logging, requiring explicit `journalctl` queries or forwarder deployment for SIEM ingestion.
3. **Lynis System Hardening Assessment (Initial Score: 61/100 -> Post-Fix Score: 63/100):** Initial automated scanning identified missing host firewalls, unconfigured password hashing parameters, missing file integrity monitoring tools, and an un-rebooted kernel (`KRNL-5830`). Enabling the host firewall successfully raised the Hardening Index to 63/100.

---

## 2. Scope and Authorisation

* **Target System:** Kali Linux Workload (`hostname: kali`, user: `kali`)
* **Kernel & OS:** Linux 6.18.12+kali-amd64 x86_64
* **Authorisation Level:** Explicitly authorized lab environment for GRC102 practical evaluation.
* **Boundaries:** All execution occurred locally using `sudo` privileges. No unauthorized network scanning or binary destruction was performed.

---

## 3. Methodology

The audit followed a four-stage evidence collection framework:

1. **Kernel Auditing Configuration (`auditd`):** Service verification, custom rule deployment (`/etc/audit/rules.d/custom.rules`), event generation, and querying via `ausearch` and `aureport`.
2. **Log Management & Querying:** Analysis of systemd journals (`journalctl`) to investigate privilege escalation and system error/warning telemetry.
3. **Automated Security Assessment (`Lynis`):** System evaluation using Lynis 3.1.6 to compute the Hardening Index, extract warnings/suggestions, and execute verified remediation.
4. **Governance & Control-Assurance Mapping:** Mapping raw technical outputs to control objectives, owners, thresholds, escalation triggers, and retest procedures.

---

## 4. Module 1: System Auditing with auditd (Evidence Bundle 1)

### Activity 1.1 — Verify or Install auditd

#### Step 1: Verify auditd Status

Check whether the `auditd` daemon is installed and running on the target system:

```bash
sudo systemctl status auditd
```

**Observed Terminal Output:**

```text
Unit auditd.service could not be found.
```

*Analysis:* The Linux Kernel Auditing daemon (`auditd`) was not pre-installed on this Kali Linux installation.

#### Step 2: Install and Enable auditd

Install `auditd` and `audispd-plugins` packages using `apt`:

```bash
sudo apt update
sudo apt install auditd audispd-plugins -y
```

Start and enable the service to ensure persistence across reboots:

```bash
sudo systemctl start auditd
sudo systemctl enable auditd
```

Verify identity watermark:

```bash
echo "Confidence Chinwuko"
```

**Observed Terminal Output:**

```text
Created symlink '/etc/systemd/system/multi-user.target.wants/auditd.service' -> '/usr/lib/systemd/system/auditd.service'.
Confidence Chinwuko
```

---

### Activity 1.2 — Configure Audit Rules

#### Step 1: Create Custom Rules File

Create and edit `/etc/audit/rules.d/custom.rules` using `nano`:

```bash
sudo nano /etc/audit/rules.d/custom.rules
```

#### Step 2: Define Rule Definitions

Add the following governance watch rules into `/etc/audit/rules.d/custom.rules`:

```text
-w /etc/passwd -p rwxa -k passwd_changes
-w /etc/shadow -p rwxa -k shadow_changes
-a always,exit -F arch=b64 -S execve -k program_execution
-a always,exit -F arch=b32 -S execve -k program_execution
-w /var/log/auth.log -p wa -k auth_failures
```

#### Step 3: Restart and Verify Active Audit Rules

Reload `auditd` service to apply rules, then verify active rule list:

```bash
sudo systemctl restart auditd
sudo auditctl -l
```

**Observed Terminal Output (`sudo auditctl -l`):**

```text
-w /etc/passwd -p rwxa -k passwd_changes
-w /etc/shadow -p rwxa -k shadow_changes
-a always,exit -F arch=b64 -S execve -F key=program_execution
-a always,exit -F arch=b32 -S execve -F key=program_execution
-w /var/log/auth.log -p wa -k auth_failures
```

---

### Activity 1.3 — Generate and Query Audit Events

#### Step 1: Generate Test Security Events

Simulate file access and program execution to trigger active audit keys:

```bash
sudo nano /etc/passwd
# Opened /etc/passwd and exited (Ctrl+X) without modifying.
ls /tmp
```

#### Step 2: Query Audit Events by Key

Query the audit log using `ausearch` for specific governance keys:

```bash
sudo ausearch -k passwd_changes
```

**Observed Evidence:** Confirms access attempt to identity database `/etc/passwd`.

```bash
sudo ausearch -k auth_failures
```

**Observed Evidence:**

```text
type=CONFIG_CHANGE msg=audit(1790939752.342:231): auid=4294967295 ses=4294967295 subj=unconfined op=add_rule key="auth_failures" list=4 res=1
```

#### Step 3: Generate Summary Reports

Run summary reports using `aureport`:

```bash
sudo aureport
```

**Observed Report Summary:**

```text
Range of time in logs: 10/02/2026 07:02:48.488 - 10/02/2026 07:30:13.328
Number of changes in configuration: 11
Number of executables: 27
Number of commands: 45
Number of failed syscalls: 117
```

```bash
sudo aureport --failed
```

**Observed Failed Report Summary:**

```text
Failed Summary Report
======================================================
Number of failed syscalls: 122
Number of process IDs: 25
Number of events: 122
```

```bash
sudo aureport --login
```

**Observed Login Report Summary:**

```text
Login Report
======================================================
# date time auid host term exe success event
======================================================
<no events of interest were found>
```

#### Step 4: Governance & Forensic Interpretation

1. **User Accountability (`auid=1000`):** The audit records track the Audit User ID (`auid=1000`, belonging to user `kali`) across elevated root commands, preserving non-repudiation.
2. **Identity Integrity:** File watches on `/etc/passwd` and `/etc/shadow` ensure that any unauthorized modification, credential manipulation, or backdoor creation generates immediate, queryable audit trails.

---

## 5. Module 2: Linux Log Management and Analysis (Evidence Bundle 2)

### Activity 2.1 — Explore Logs with journalctl

Execute `journalctl` to view system log events managed by `systemd`:

```bash
sudo journalctl
```

**Observed Evidence Output:**

```text
Jun 25 13:16:09 kali kernel: Linux version 6.18.12+kali-amd64 (devel@kali.org)
Jun 25 13:16:09 kali kernel: Command line: BOOT_IMAGE=/boot/vmlinuz-6.18.12+kali-amd64 root=UUID=...
Jun 25 13:16:09 kali kernel: BIOS-provided physical RAM map: ...
```

---

### Activity 2.2 — Authentication and Privilege-Use Analysis

#### Step 1: Inspect Authentication Logs

Query `/var/log/auth.log` for authentication events:

```bash
sudo less /var/log/auth.log
```

**Observed System Response:**

```text
/var/log/auth.log: No such file or directory
```

*Technical Note:* Kali Linux uses `systemd-journald` for log management by default without traditional syslog file generation (`/var/log/auth.log`). System authentication logs are queried directly via `journalctl`.

#### Step 2: Query Authentication and Privilege Escalation Events via journalctl

Execute equivalent queries against systemd journal telemetry for `sudo` privilege escalation and authentication events:

```bash
sudo journalctl | grep -i "failed password"
sudo journalctl | grep -i "sudo"
```

**Observed Authentication & Privilege Telemetry:**

```text
Jun 25 14:10:34 kali sudo[5541]:   kali : TTY=pts/0 ; PWD=/home/kali ; USER=root ; COMMAND=/usr/bin/apt update
Jun 25 14:10:34 kali sudo[5541]: pam_unix(sudo:session): session opened for user root(uid=0) by kali(uid=1000)
Jun 25 14:15:22 kali sudo[5541]: pam_unix(sudo:session): session closed for user root
Jun 25 14:16:38 kali sudo[8649]:   kali : TTY=pts/0 ; PWD=/home/kali ; USER=root ; COMMAND=/usr/bin/apt upgrade
Jun 25 14:16:38 kali sudo[8649]: pam_unix(sudo:session): session opened for user root(uid=0) by kali(uid=1000)
```

---

### Activity 2.3 — General System Log Review

#### Step 1: Direct File Checks on /var/log/syslog

Execute queries against `/var/log/syslog`:

```bash
sudo less /var/log/syslog
sudo grep -i "error" /var/log/syslog
sudo grep -i "warning" /var/log/syslog
```

**Observed Terminal Output:**

```text
/var/log/syslog: No such file or directory
grep: /var/log/syslog: No such file or directory
grep: /var/log/syslog: No such file or directory
```

*Technical Analysis:* Kali Linux operating in standard VM mode relies entirely on `systemd-journald` for binary system log storage. `/var/log/syslog` does not exist by default unless `rsyslog` is explicitly installed and configured.

#### Step 2: Query Recent System Log Telemetry via journalctl

Query recent journal output for system events:

```bash
sudo journalctl -n 50
```

**Observed Terminal Telemetry Output:**

```text
Oct 02 08:25:48 kali kernel: 12:25:48.366254 vmsvga-session VBoxClient VMSVGA: Error: unable to reconnect to IPC server, rc=VERR_FILE_NOT_FOUND
Oct 02 08:25:48 kali kernel: 12:25:48.372508 vmsvga-session VBoxClient VMSVGA: Error: unable to handle IPC connection, rc=VERR_NET_CONNECTION_RESET_BY_PEER
Oct 02 08:26:00 kali sudo[443759]:   kali : TTY=pts/1 ; PWD=/home/kali ; USER=root ; COMMAND=/usr/bin/journalctl -n 50
Oct 02 08:26:00 kali sudo[443759]: pam_unix(sudo:session): session opened for user root(uid=0) by kali(uid=1000)
```

#### Step 3: Query System Error Telemetry

Filter journal logs specifically for error events:

```bash
sudo journalctl | grep -i "error"
```

**Observed Terminal Telemetry Output:**

```text
Jun 25 13:16:09 kali kernel: RAS: Correctable Errors collector initialized.
Jun 25 13:16:09 kali kernel: vmwgfx 0000:00:02.0: [drm] *ERROR* vmwgfx seems to be running on an unsupported hypervisor.
Jun 25 13:16:09 kali kernel: vmwgfx 0000:00:02.0: [drm] *ERROR* This configuration is likely broken.
Jun 25 13:16:09 kali kernel: vmwgfx 0000:00:02.0: [drm] *ERROR* Please switch to a supported graphics device to avoid problems.
Jun 25 13:17:05 kali virtualbox-guest-utils[779]: error: XDG_RUNTIME_DIR is invalid or not set in the environment.
Jun 25 13:17:05 kali kernel: 17:17:05.986922 Timer VBoxDRMClient: Error: unable to validate screen layout: first monitor is not allowed to be disabled
```

#### Step 4: Query System Warning Telemetry

Filter journal logs for warning conditions:

```bash
sudo journalctl | grep -i "warning"
```

**Observed Terminal Telemetry Output:**

```text
Jun 25 13:16:09 kali kernel: Warning! ehci_hcd should always be loaded before uhci_hcd and ohci_hcd, not after
Jun 25 14:02:46 kali kernel: Warning! ehci_hcd should always be loaded before uhci_hcd and ohci_hcd, not after
Jul 03 07:44:59 kali kernel: Warning! ehci_hcd should always be loaded before uhci_hcd and ohci_hcd, not after
Oct 02 08:23:03 kali sudo[441782]:   kali : TTY=pts/1 ; PWD=/home/kali ; USER=root ; COMMAND=/usr/bin/grep -i warning /var/log/syslog
```

---

### Security Event Summary Table (Activities 2.1 – 2.3)

| Event / Condition | Evidence Source | Time Context | User / Service | Security Significance | Recommended Action |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Audit Service Missing** | `systemctl status auditd` | Initial Check | System (`auditd`) | Subsystem inactive; unmonitored execution. | Install and enable `auditd` and `audispd-plugins`. |
| **Custom Rule Insertion** | `/etc/audit/rules.d/custom.rules` | 07:12 WAT | `kali` (`uid=0`) | Watch rules applied for key identity files. | Enforce WORM storage for `/etc/audit/rules.d/`. |
| **Privilege Escalation (`sudo`)** | `journalctl` | Jun 25 14:10:34 | `kali` (`auid=1000`) | Administrative command execution via `sudo`. | Monitor `sudo` sessions and forward to SIEM. |
| **Missing Legacy Syslog File** | `/var/log/syslog` | Oct 02 08:23:03 | System (`journald`) | `/var/log/syslog` missing; logs managed via `journald`. | Forward `journald` stream via TLS to centralized SIEM. |
| **VM Graphics & Driver Errors** | `journalctl \| grep -i "error"` | Jun 25 13:16:09 | Kernel (`vmwgfx`) | Hypervisor graphics driver incompatibility. | Update VirtualBox Guest Additions and driver modules. |

---

## 6. Module 3: Linux Security Assessment with Lynis (Evidence Bundle 3)

### Activity 3.1 & 3.2 — Install Lynis and Run Initial System Audit

Install Lynis security auditing tool and execute initial system scan:

```bash
sudo apt update
sudo apt install lynis -y
sudo lynis audit system
```

#### Observed Terminal Scan Metrics

* **Lynis Version:** `3.1.6`
* **Scan Mode:** Normal
* **Hardening Index:** `61 / 100` `[########### ]`
* **Tests Performed:** `272`
* **Plugins Enabled:** `1`
* **Software Components Status:**
  * Firewall: `[X]` (Disabled / Missing)
  * Intrusion Software: `[X]` (Missing)
  * Malware Scanner: `[X]` (Missing)
* **Log File:** `/var/log/lynis.log`
* **Report Data File:** `/var/log/lynis-report.dat`

---

### Analysis of Warnings and Suggestions from Lynis Log

#### Step 1: System Warnings Query

Execute search for explicit warnings in the Lynis log file:

```bash
sudo grep "Warning:" /var/log/lynis.log
```

**Observed Terminal Output:**

```text
2026-10-02 09:14:59 Warning: Reboot of system is most likely needed [test:KRNL-5830] [details:-] [solution:text:reboot]
2026-10-02 09:16:18 Warning: Nameserver fd17:625c:f037:2::3 does not respond [test:NETW-2704] [details:-] [solution:-]
```

#### Step 2: System Suggestions Query

Execute search for actionable suggestions in the Lynis log file:

```bash
sudo grep "Suggestion:" /var/log/lynis.log
```

**Observed Key Terminal Output Excerpts:**

```text
Suggestion: Install fail2ban to automatically ban hosts that commit multiple authentication errors. [test:DEB-0880]
Suggestion: Configure password hashing rounds in /etc/login.defs [test:AUTH-9230]
Suggestion: Install a PAM module for password strength testing like pam_cracklib or pam_passwdqc [test:AUTH-9262]
Suggestion: Disable drivers like USB storage when not used [test:USB-1000]
Suggestion: Enable logging to an external logging host for archiving purposes [test:LOGG-2154]
Suggestion: Install a file integrity tool to monitor changes to critical and sensitive files [test:FINT-4350]
Suggestion: Harden the system by installing at least one malware scanner [test:HRDN-7230]
```

---

### Module 3 Prioritized Findings Table

| Finding ID | Lynis Test / Warning ID | Risk / Control Issue | Evidence / Detail | Accountable Owner | Recommended Remediation | Priority |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **W4-F01** | `AUTH-9230` / `AUTH-9262` | Weak default password policy and unconfigured hashing rounds. | `/etc/login.defs` missing explicit SHA-512 rounds; PAM strength checks absent. | System Administrator | Configure `SHA_CRYPT_MIN_ROUNDS 5000` in `/etc/login.defs` and install `libpam-passwdqc`. | **High** |
| **W4-F02** | `NETW-2704` | Non-responsive DNS nameserver IPv6 address (`fd17:625c:f037:2::3`). | `Warning: Nameserver fd17:625c:f037:2::3 does not respond` in `/var/log/lynis.log`. | Network Admin | Update `/etc/resolv.conf` to point to responsive corporate/DNS servers. | **Medium** |
| **W4-F03** | `LOGG-2154` | Absence of centralized log shipping to remote syslog/SIEM host. | Local logs vulnerable to erasure following root compromise. | SecOps Lead | Configure `Filebeat` or `rsyslog` to forward logs securely via TLS to central SIEM. | **High** |
| **W4-F04** | `FINT-4350` / `HRDN-7230` | Absence of file integrity monitoring (FIM) and malware scanning software. | Firewall `[X]`, Intrusion Software `[X]`, Malware Scanner `[X]` in Lynis report summary. | Security Operations | Install AIDE/Tripwire for FIM and ClamAV/Rkhunter for malware scanning. | **High** |
| **W4-F05** | `KRNL-5830` | Pending kernel reboot required following updates. | `Warning: Reboot of system is most likely needed [test:KRNL-5830]`. | IT Operations | Schedule system reboot during approved maintenance window. | **Medium** |

---

### Activity 3.3 — Hardening Action and Post-Fix Retest

#### Selected Control: Host Firewall Activation (`FIRE-8410`)

* **Control Objective:** Enable host-based packet filtering to prevent unauthorized network access to running services.
* **Initial State:** Firewall status displayed `[X]` (Disabled), Hardening Index **61/100**, 272 tests performed.
* **Remediation Action Executed:** Enabled host firewall service (`ufw`) and re-ran the Lynis assessment suite:

```bash
sudo ufw enable
sudo lynis audit system
```

#### Post-Hardening Retest Verification Metrics

* **Hardening Index:** Increased from **61 / 100** to **63 / 100** `[########### ]`
* **Tests Performed:** Increased from **272** to **273**
* **Software Components Updated State:**
  * Firewall: `[V]` (**Active / Verified**)
  * Intrusion Software: `[X]`
  * Malware Scanner: `[X]`
* **Verification Conclusion:** Host firewall activation successfully raised system hardening index by **2 points** and passed Lynis verification check `FIRE-8410`.

---

## 7. Control Monitoring and Governance Register (Evidence Bundle 4)

| Control / Objective | Evidence Source | Owner | Observed Status | KPI / Threshold | Remediation Action |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **IAM-01:** Account Integrity | `auditd` (`passwd_changes`) | SysAdmin | **AMBER** | 0 unapproved edits | Audit `/etc/passwd` against approved change requests. |
| **LOG-01:** Host Auditing | `systemctl status auditd` | SecOps | **GREEN** | Service Uptime > 99.9% | Maintain persistent systemd auto-restart. |
| **NET-01:** Host Firewall | Lynis `FIRE-8410` | IT Admin | **GREEN** (Post-Fix) | Firewall status `[V]` | Enabled UFW firewall; raised score to 63/100. |
| **VULN-01:** Patch / Reboot Status | Lynis `KRNL-5830` | System Owner | **AMBER** | Pending reboots = 0 | Schedule kernel reboot during maintenance window. |
| **SIEM-01:** Off-Host Logging | `LOGG-2154` / Filebeat | CloudOps | **RED** | 100% logs shipped off-host | Deploy Filebeat agent to stream journald logs over TLS. |

---

## 8. Conclusion

The evaluation of the Kali Linux workload demonstrated functional kernel auditing once `auditd` was deployed, but highlighted critical governance gaps in default log retention files (`/var/log/syslog` missing) and baseline security hardening (Hardening Index 61/100). By activating the host firewall, the hardening index was improved to 63/100. Implementing central log forwarding via Filebeat and automating file integrity checks will transition this host into continuous control compliance.

---

## Appendix A: Security Finding Record

```text
================================================================================
                        SECURITY FINDING RECORD [W4-F01]
================================================================================
Finding ID:             W4-F01
Date / Time Observed:   02 October 2026, 09:14 WAT
Evidence Source:        Lynis Audit / /var/log/lynis.log [FIRE-8410]
Evidence Summary:       Host firewall was inactive (Software component Firewall [X])
Security Significance:  Exposes active network services to unauthorized network probing
Control Objective:      Enforce host-based access boundaries (NIST SP 800-53 SC-7)
Control Owner:          IT Infrastructure / SecOps Lead
Risk / Priority:        HIGH
Recommended Action:     Enable UFW/iptables service and enforce default ingress deny rule
Retest Evidence:        Lynis test FIRE-8410 passing; Firewall status [V]; Index improved to 63/100
================================================================================
```


##  Lab Evidence & Screenshots

The complete visual evidence, terminal outputs, and screenshots demonstrating the successful execution of all lab activities can be reviewed at the link below:

**Click Here; https://docs.google.com/document/d/15l7MgaHwUnjQ-EJXzH7iv_Z_1-MqkCA8YMFZxij2cq8/edit?usp=drivesdk
  to View All Lab Screenshots and Evidence
