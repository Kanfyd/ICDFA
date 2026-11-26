# GRC103 Lab: Practical Risk Monitoring with Wazuh (File Integrity Monitoring)

**Course:** GRC103 – Risk Assessment and Management Techniques  
**Module:** Practical Risk Assessment Workshop  
**Control Objective:** Operationalize a Detective Control for Financial Document Integrity  

---

## 1. Executive Summary & Risk Mandate

A recent risk assessment identified the **unauthorized modification or deletion of sensitive financial forecast documents** as a medium-to-high business risk. To satisfy the Risk Treatment Plan, **Wazuh (v4.12.0)** was deployed as a centralized security monitoring platform and configured with **File Integrity Monitoring (FIM / `syscheck`)** as a **detective control**.

### Architecture Implemented
| Component | Host Environment | GRC Role |
| :--- | :--- | :--- |
| **Wazuh Manager, Indexer & Dashboard** | Ubuntu Server (`kanfyd-ubuntu`) | **Risk Monitoring Platform:** Aggregates endpoint telemetry, evaluates rules, and maintains a central audit trail. |
| **Wazuh Agent** | Windows Endpoint (`Finance-Dept-Workstation`) | **Control Agent:** Monitors `C:\Users\confidence\SensitiveFiles` in real time and forwards file change events. |

---

## 2. Technical Implementation & Verification Log

### Part 1: Environment Preparation & Wazuh Manager Deployment (Ubuntu)
1. **Network & Connectivity Verification:** Verified outbound internet reachability (`ping -c 3 google.com`) on `kanfyd-ubuntu` (`172.20.29.247`) and configured reliable DNS resolution (`8.8.8.8` / `1.1.1.1`) via `/etc/systemd/resolved.conf.d/dns_servers.conf`.
2. **Storage & Package Readiness:** Extended the root LVM volume (`sudo lvextend -l +100%FREE /dev/ubuntu-vg/ubuntu-lv`) and resized the filesystem (`sudo resize2fs /dev/ubuntu-vg/ubuntu-lv`) to `23 GB` (`14 GB` available) to accommodate the Wazuh Indexer, Manager, Filebeat, and Dashboard packages.
3. **All-in-One Deployment:** Executed `sudo bash wazuh-install.sh -a -i` to deploy Wazuh `v4.12.0`, initialize cluster certificates, and generate administrative credentials.
4. **Firewall & Service Verification:** Allowed ports `443/tcp` (Dashboard HTTPS), `1514/tcp` (Agent communication), and `1515/tcp` (Agent enrollment) in UFW, then verified `wazuh-manager.service` was `active (running)`.

> *[Insert Screenshot: Ubuntu terminal showing `wazuh-install.sh` completion summary and `systemctl status wazuh-manager` active]*

---

### Part 2: Accessing the Wazuh Dashboard
1. Navigated to the Wazuh web console (`https://127.0.0.1/app/login`), accepted the expected self-signed TLS certificate warning, and authenticated as `admin`.
2. Confirmed under **Server APIs** that `kanfyd-ubuntu` (`v4.12.0`) showed a status of **Online**.

> *[Insert Screenshot: Wazuh Dashboard Server API connection showing `kanfyd-ubuntu` Online]*

---

### Part 3 & 4: Windows Agent Installation & Registration
1. Installed the matching `v4.12.0` Wazuh Agent on the Windows endpoint (`Finance-Dept-Workstation`).
2. Registered the agent via `/var/ossec/bin/manage_agents` (`ID: 001` / `002`, Name: `Finance-Dept-Workstation`, IP: `any`), imported the authentication key into the Windows Wazuh Agent Manager, and restarted `WazuhSvc`.
3. Verified on the Wazuh Dashboard **Overview** panel that the agent reported **Active (1)** with **Disconnected (0)**.

> *[Insert Screenshot: Windows Wazuh Agent Manager status "Running" and Dashboard "Active (1)"]*

---

### Part 5 & 6: Configuring FIM & Verifying Risk Events
1. **Control Configuration:** Added real-time monitoring to `C:\Program Files (x86)\ossec-agent\ossec.conf` inside the `<syscheck>` block:
   ```xml
   <directories realtime="yes">C:\Users\confidence\SensitiveFiles</directories>
   ```
2. **Simulated Risk Events:** Performed controlled file creation, modification, and deletion actions on `Q4_Financial_Forecast.docx` inside `C:\Users\confidence\SensitiveFiles`.
3. **Audit Trail Verification:** Filtered the dashboard under **File Integrity Monitoring > Events** (`manager.name: kanfyd-ubuntu`, `rule.groups: syscheck`, `agent.id: 002`), capturing **84 hits**, including:

| Timestamp (Nov 24, 2026) | Agent Name | File Path | Action (`syscheck.event`) | Rule ID & Description | Level |
| :--- | :--- | :--- | :--- | :--- | :---: |
| `13:15:04.4...` | `Finance-Dept-Workstation` | `c:\users\confidence\sensitivefiles\q4_financial_forecast...` | `added` | `554` – File added to the system | 5 |
| `13:15:35.7...` | `Finance-Dept-Workstation` | `c:\users\confidence\sensitivefiles\q4_financial_forecast...` | `modified` | `550` – Integrity checksum changed | 7 |
| `13:19:50.5...` | `Finance-Dept-Workstation` | `c:\users\confidence\sensitivefiles\q4_financial_forecast...` | `modified` | `550` – Integrity checksum changed | 7 |
| `13:20:25.6...` | `Finance-Dept-Workstation` | `c:\users\confidence\sensitivefiles\q4_financial_forecast...` | `deleted` | `553` – File deleted | 7 |

> *[Insert Screenshot: Wazuh FIM Events table showing Rule IDs 554, 550, and 553 for `q4_financial_forecast`]*

---

## 3. GRC Workshop & Analysis Questions

### 1. Risk Identification & Analysis
* **Potential Business Impact:**
  * **Financial Impact:** Decisions made from altered revenue or expense projections can lead to misallocated budgets, liquidity shortfalls, or inaccurate financial reporting.
  * **Operational Impact:** Finance and leadership teams must pause planning cycles to investigate discrepancies, audit historical records, and rebuild forecast models from backups.
  * **Reputational & Regulatory Impact:** Compromised financial records weaken stakeholder, auditor, and regulator confidence in internal controls over financial reporting.
* **Quantifying Risk via FIM Alerts:**
  * Rather than relying solely on subjective estimates, Wazuh provides empirical metrics—such as the frequency of file changes (`added`, `modified`, `deleted`), timestamps (e.g., off-hours modifications), and affected endpoints—to establish baseline change rates and estimate event likelihood over time.
  * *Analyst Note:* An FIM alert confirms that a file changed; determining whether the change was **unauthorized** requires correlating the event timestamp and user context against approved change windows.

### 2. Control Evaluation & Treatment
* **Complementary Preventive Control:**
  * **Role-Based Access Control (RBAC) / NTFS Least-Privilege Permissions:** Restricting write, modify, and delete permissions on `C:\Users\confidence\SensitiveFiles` strictly to authorized finance personnel (while assigning read-only or deny permissions to all other accounts) stops unauthorized edits *before* they happen.
* **Triggering a Corrective Control:**
  * If Wazuh generates a high-priority `modified` (Rule `550`) or `deleted` (Rule `553`) alert on `Q4_Financial_Forecast.docx` outside approved hours or from a compromised workstation, that detective alert triggers **corrective controls**: isolating the host or revoking the suspicious user session, investigating the root cause, and restoring the verified clean forecast document from backup using its known-good cryptographic hash.

### 3. Risk Monitoring & Reporting
* **Three Key Operational Effectiveness Metrics:**
  1. **Agent Connectivity Rate (`Active` vs. `Disconnected`):** Confirms continuous control coverage across monitored finance endpoints.
  2. **FIM Alert Volume by Event Type (`added` / `modified` / `deleted`):** Tracks baseline file change activity and flags unusual spikes in modifications or deletions.
  3. **Mean Time to Detect & Triage (MTTD/MTTA):** Measures how quickly file change alerts are ingested, reviewed, and resolved by analysts.
* **Value of Centralization for Governance & Auditability:**
  * Reviewing local Windows logs on individual computers does not scale and exposes logs to local tampering or deletion by privileged users. Centralizing events in Wazuh establishes a single, tamper-resistant audit trail, enforces consistent alerting rules across endpoints, and simplifies evidence retrieval during management reviews.

### 4. Compliance Mapping
* **Providing Evidence for Compliance Audits (SOX, PCI DSS, HIPAA):**
  * Regulatory frameworks require verifiable proof that critical files are monitored for unauthorized changes. Wazuh generates timestamped audit records containing the exact file path, event action, rule attribution, and cryptographic checksums (MD5, SHA-1, SHA-256) before and after modification.
* **Demonstrating Unaltered File Integrity Over a Defined Period (e.g., Last Quarter):**
  1. Open the Wazuh Dashboard and set the **Time Range Filter** in the top-right corner to the exact audit quarter (e.g., `Last 90 days` or custom start/end dates).
  2. Filter the search bar by endpoint and file path:
     ```text
     agent.name: "Finance-Dept-Workstation" AND syscheck.path: "c:\\users\\confidence\\sensitivefiles\\q4_financial_forecast.docx"
     ```
  3. Present the query results to the auditor showing **zero unauthorized `modified` (Rule `550`) or `deleted` (Rule `553`) alerts** during that quarter, supported by the file's baseline and current cryptographic hashes in the **FIM Inventory** tab.