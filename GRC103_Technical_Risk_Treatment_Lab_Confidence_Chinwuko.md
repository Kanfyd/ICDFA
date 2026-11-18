# GRC103 Risk Assessment and Management Techniques: Technical Risk Treatment Lab Report
**Organization:** Northbridge Services  
**Analyst:** Confidence Chinwuko  
**Target Environment:** Isolated Host-Only Network (`192.168.56.0/24`)  
**Ubuntu Server IP:** `192.168.56.104` (`kanfyd-ubuntu`)  
**Kali Linux IP:** `192.168.56.101` (`kali`)  

---

## 1. Executive Management Summary
Northbridge Services operates an internal document server hosting an approved web portal alongside an obsolete legacy training endpoint. Management required measurable technical risk treatment to eliminate unnecessary service exposure, prevent unauthorized directory and file disclosure, restrict unauthenticated network access, and establish verifiable recovery resilience—all without disrupting authorized access to the approved web service.

Executing a structured lab implementation across an isolated dual-virtual-machine environment (Ubuntu Server 24.04 LTS and Kali Linux), we applied all four core risk treatment strategies: **Avoidance**, **Mitigation (Preventive, Detective, and Corrective Controls)**, **Transfer**, and **Acceptance**. 

* **Key Outcomes:** 
  * Retired the unmaintained legacy service (`8080/tcp`), completely eliminating its attack surface.
  * Relocated sensitive archive files outside the web root and enforced strict Nginx `deny all` access controls.
  * Restricted network-layer access via Ubuntu Uncomplicated Firewall (UFW) to allow only authorized management traffic.
  * Correlated application and kernel firewall logs to prove architectural defense-in-depth.
  * Executed a timed backup and restoration exercise with cryptographic hash verification (`SHA-256`), demonstrating sub-minute recovery capability.
  * Evaluated financial costs, residual risk scores, and ongoing governance triggers to ensure long-term operational accountability.

---

## 2. Baseline Environment & Risk Assessment (Steps 1–5)

### Environment Architecture & Network Verification
Both virtual machines were provisioned on an isolated host-only network (`192.168.56.0/24`) with external bridged/NAT interfaces disconnected prior to standing up exposed services:
* **Target Server (`kanfyd-ubuntu`):** `192.168.56.104` (MAC: `08:00:27:B1:61:86`)
* **Assessment Host (`kali`):** `192.168.56.101` (MAC: `08:00:27:8A:35:D2`)

### Baseline Reconnaissance & Evidence Collection (Step 4)
Initial scanning and HTTP enumeration from Kali (`2026-11-11T09:07:00-05:00`) established the pre-treatment baseline:

1. **Port & Service Scan (`baseline-ports.txt`):**
   * `80/tcp` — **Open** (`http`, Nginx 1.28.3)
   * `8080/tcp` — **Open** (`http-proxy`, Python `SimpleHTTP/0.6` legacy endpoint)
2. **Web Root Enumeration (`baseline-web.txt`):**
   * `GET http://192.168.56.104/` returned `HTTP/1.1 200 OK` with Nginx `autoindex` enabled, publicly displaying links to both `/archive/` and `/public/`.
3. **Archive Directory & File Exposure (`baseline-listing.txt`, `baseline-file.txt`):**
   * `GET http://192.168.56.104/archive/` returned `HTTP/1.1 200 OK`, exposing `dummy-records.txt`.
   * `GET http://192.168.56.104/archive/dummy-records.txt` returned `HTTP/1.1 200 OK` and leaked the file content: `DUMMY RECORD A001 - training only`.
4. **Legacy Endpoint Exposure (`baseline-legacy.txt`):**
   * `GET http://192.168.56.104:8080/` returned `HTTP/1.0 200 OK` and served `Legacy training endpoint`.

### Baseline Risk Register (Step 5)
Risks were evaluated using classroom ordinal scales ($\text{Likelihood } 1\text{–}5 \times \text{Impact } 1\text{–}5 = \text{Score}$; Bands: $1\text{–}4$ Low, $5\text{–}9$ Medium, $10\text{–}16$ High, $17\text{–}25$ Critical):

| Risk ID | Asset | Threat Event | Observed Weakness | Likelihood | Impact | Score | Risk Band | Evidence Reference | Treatment Owner |
| :--- | :--- | :--- | :--- | :---: | :---: | :---: | :---: | :--- | :--- |
| **R1** | Legacy Endpoint (`8080/tcp`) | Unauthorized access or exploitation of obsolete service | Unnecessary Python HTTP server listening on all interfaces (`0.0.0.0:8080`) without authentication. | 4 | 3 | **12** | **High** | `baseline-ports.txt`, `baseline-legacy.txt` | System Administration |
| **R2** | Archive Directory (`/var/www/grc-lab/archive`) | Unauthorized disclosure of internal records | Directory indexing enabled (`autoindex on`) and dummy records stored directly inside web root. | 4 | 4 | **16** | **High** | `baseline-web.txt`, `baseline-listing.txt`, `baseline-file.txt` | Web Operations Lead |
| **R3** | Server Network Interface (`192.168.56.104`) | Network reconnaissance and unauthorized client access | Host firewall inactive/unrestricted; any IP on the subnet can query ports 80 and 8080. | 3 | 3 | **9** | **Medium** | `baseline-ports.txt` | Network Security Team |
| **R4** | Approved Portal (`/var/www/grc-lab/public`) | Accidental deletion, corruption, or loss of portal content | No automated backup archive or cryptographic integrity baseline in place. | 2 | 4 | **8** | **Medium** | `portal-before.sha256` | Backup Administrator |

---

## 3. Change Management & Technical Risk Treatment (Steps 6–8)

### Step 6: Applying Avoidance to the Legacy Workflow (R1)
* **Change Control Record:**
  * **Proposed Change:** Stop, disable, and retire the unnecessary `grc-legacy.service` systemd unit while preserving Nginx on port 80.
  * **Business Impact:** None; the legacy endpoint contains only obsolete training data and is not part of the approved internal portal.
  * **Approval Role:** IT Change Advisory Board / GRC Lead *(Simulated Approval)*.
  * **Test Plan:** Verify service state (`systemctl is-active`), local socket listeners (`ss -lntp`), and remote Nmap/`curl` probes from Kali.
  * **Rollback Plan:** Execute `sudo systemctl enable --now grc-legacy` to restore service availability if unexpected dependencies arise.
* **Execution & Verification (`avoidance-ports.txt`, `avoidance-legacy.txt`):**
  ```bash
  sudo systemctl disable --now grc-legacy
  sudo systemctl is-active grc-legacy
  sudo ss -lntp
  ```
  * Post-treatment Nmap scan from Kali confirmed `8080/tcp` state changed from `open` to **`closed`**, while `80/tcp` remained **`open`**.
  * `curl -i "http://192.168.56.104:8080/"` failed immediately (`curl: (7) Failed to connect to 192.168.56.104:8080 after 0 ms: Could not connect to server`).
  * Rollback was tested and verified operational, after which the service was re-disabled for the final hardened state.
* **Analytical Distinction (Avoidance vs. Total Risk Elimination):** Retiring `grc-legacy` completely eliminates the specific attack surface and operational exposure of the legacy Python web server (Avoidance). However, it does **not** eliminate risks to the remaining approved web service on port 80 (such as web application vulnerabilities, unauthorized directory access, or network-level attacks), which still require active preventive and detective controls.

### Step 7: Preventive Controls — Archive Removal & Nginx Hardening (R2)
* **Implementation:**
  Moved `/archive` out of the web root into a root-restricted directory (`/srv/grc-private`), disabled `autoindex`, and added an explicit `deny all` location block in `/etc/nginx/sites-available/grc-lab`:
  ```bash
  sudo mkdir -p /srv/grc-private
  sudo mv /var/www/grc-lab/archive /srv/grc-private/
  sudo chmod -R go-rwx /srv/grc-private/
  ```
  ```nginx
  server {
      listen 80;
      server_name _;
      root /var/www/grc-lab;
      access_log /var/log/nginx/grc_access.log combined;
      error_log /var/log/nginx/grc_error.log;

      location / {
          autoindex off;
      }
      location /archive/ {
          deny all;
      }
  }
  ```
* **Validation Results:**
  * `GET http://192.168.56.104/public/` (`preventive-public-200.txt`): Returned **`HTTP/1.1 200 OK`** (`Approved internal portal`).
  * `GET http://192.168.56.104/archive/` (`preventive-archive-403.txt`): Returned **`HTTP/1.1 403 Forbidden`**.
  * `GET http://192.168.56.104/archive/dummy-records.txt` (`preventive-file-403.txt`): Returned **`HTTP/1.1 403 Forbidden`**.
  * `GET http://192.168.56.104/` (`preventive-root-403.txt`): Returned **`HTTP/1.1 403 Forbidden`** (because directory listing is off and no root `index.html` exists).
* **Analytical Explanation:** Setting `autoindex off` alone only stops the web server from generating an HTML index page listing directory contents; it does **not** block direct HTTP requests to known or guessed file paths (e.g., `/archive/dummy-records.txt`). Relocating files outside the web root and applying explicit `location /archive/ { deny all; }` directives provides true defense-in-depth against direct-URI enumeration.

### Step 8: Preventive Network Access Control with UFW (R3)
* **Implementation:**
  Configured Ubuntu's host firewall on the VM console to drop all unsolicited inbound packets while permitting TCP port 80 exclusively from Kali's primary IP (`192.168.56.101`):
  ```bash
  sudo ufw default deny incoming
  sudo ufw default allow outgoing
  sudo ufw allow from 192.168.56.101 to any port 80 proto tcp
  sudo ufw logging on
  sudo ufw enable
  ```
* **Permitted vs. Blocked Client Validation:**
  * **Permitted Source (`192.168.56.101`):** `curl -i "http://192.168.56.104/public/"` (`ufw-allowed-200.txt`) returned **`HTTP/1.1 200 OK`**.
  * **Blocked Source (`192.168.56.11`):** Added a temporary secondary alias (`sudo ip addr add 192.168.56.11/24 dev eth0`) on Kali and executed `curl --interface 192.168.56.11 --connect-timeout 5 "http://192.168.56.104/public/"` (`ufw-blocked-timeout.txt`). The connection timed out after `5002 ms` (`curl: (28)`), after which the alias IP was removed.

---

## 4. Detective Log Correlation & Corrective Recovery (Steps 9–10)

### Step 9: Control Evidence Correlation
To prove that network-layer and application-layer controls operate independently without blind spots, requests from Kali were correlated against Ubuntu's `/var/log/nginx/grc_access.log` and `/var/log/ufw.log`:

| Test ID | Source IP | Requested Service / Path | Expected Outcome | Actual Outcome | Timestamp (UTC / Local) | Log Reference |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **T-01** | `192.168.56.101` | `GET /public/` (Port 80) | Permitted (`HTTP 200`) | `HTTP/1.1 200 OK` | `10/Nov/2026:01:38:00 +0000` | `/var/log/nginx/grc_access.log` (`"GET /public/ HTTP/1.1" 200 25`) |
| **T-02** | `192.168.56.101` | `GET /archive/` (Port 80) | Blocked by Nginx (`HTTP 403`) | `HTTP/1.1 403 Forbidden` | `10/Nov/2026:01:38:23 +0000` | `/var/log/nginx/grc_access.log` (`"GET /archive/ HTTP/1.1" 403 162`) |
| **T-03** | `192.168.56.11` | `GET /public/` (Port 80) | Dropped by UFW (Timeout) | `Connection timed out (5002 ms)` | `2026-11-09T21:12:31+00:00` | `/var/log/ufw.log` (`[UFW BLOCK] IN=enp0s3 SRC=192.168.56.11 DST=192.168.56.104 DPT=80`) |

* **Analytical Explanation:** Requests from `192.168.56.101` pass through UFW's allow rule and reach Nginx, where authorized paths (`/public/`) log `200` and restricted paths (`/archive/`) log `403`. Conversely, packets from the unapproved IP `192.168.56.11` are dropped at the Linux kernel netfilter layer (`[UFW BLOCK]`) before a TCP handshake can complete. Because the connection never reaches user space, Nginx logs zero entries for `192.168.56.11`, confirming effective network-layer isolation. *(Note: During testing, `journalctl -k --since '15 minutes ago'` returned empty due to log window timing, so `/var/log/ufw.log` was inspected directly to confirm genuine kernel block records without fabricating events).*

### Step 10: Backup & Verified Portal Recovery (R4)
1. **Baseline Archive & Integrity Hashing:**
   * Created restricted backup directory `/srv/grc-backups` (`chmod 700`), archived `/var/www/grc-lab/public` to `public-before-test.tgz`, and generated the reference hash:
     `e5b34d9b4fa6452b6b1d292b0ced654c99977f7ebece28a2731f633f53a50f72  /var/www/grc-lab/public/index.html`
2. **Disruption & Restoration Timing:**
   * **Start Time (`date -Is`):** `2026-11-10T02:15:34+00:00`
   * **Simulated Loss:** Deleted `/var/www/grc-lab/public/index.html`. Kali verification (`step10-failed-check.txt` at `02:23:21 GMT`) confirmed service disruption (`HTTP/1.1 403 Forbidden`).
   * **Restoration & Hash Validation:** Extracted `public-before-test.tgz` and ran `sha256sum -c ~/portal-before.sha256`, which returned **`/var/www/grc-lab/public/index.html: OK`**.
   * **Completion Time (`date -Is`):** `2026-11-10T02:26:59+00:00`
   * **Observed Recovery Time:** **11 minutes, 25 seconds** total exercise duration (actual extraction and hash validation took **$< 2\text{ seconds}$**). Kali check (`step10-restored-check.txt` at `02:27:52 GMT`) confirmed **`HTTP/1.1 200 OK`** and intact content (`Approved internal portal`).
* **Architectural Limitation:** Storing backups locally on `/srv/grc-backups` protects effectively against accidental file deletion or logical corruption, but it provides **zero protection** against full virtual disk corruption, ransomware encryption of the entire OS, or physical host hardware failure. Production environments require off-host or immutable remote replication.

---

## 5. Strategic Governance, Cost Analysis & Reassessment (Steps 11–12)

### Step 11: Risk Transfer & Risk Acceptance Governance

#### Risk Transfer Model (Managed Backup Service Evaluation)
* **Comparison:** Evaluated a managed off-host backup service ($120 setup + $20/month = **$360/year**) against local-only tar archives ($0 software cost, high single-point-of-failure risk).
* **Division of Responsibilities:**
  * *Provider Duties:* Automated off-host storage replication, encryption at rest/transit, infrastructure uptime, and storage media redundancy.
  * *Retained Customer Duties (Northbridge Services):* Data classification, access control governance, defining Recovery Point/Time Objectives (RPO/RTO), and periodic restoration testing.
  * *Mandatory Operational Clauses:* Requires quarterly documented restoration drills and a minimum 12-month retention policy for backup verification logs.
* **Proposed Service Clause:**
  > *"The Service Provider shall maintain encrypted off-host backup replicas of designated Northbridge Services web directories with a 99.9% storage availability target and support quarterly customer-initiated restoration tests. Execution of this agreement transfers operational storage maintenance duties but does not absolve Northbridge Services of regulatory accountability, data governance, or technical security obligations."*
* **Governance Principle:** Contracts, insurance, and SLAs transfer financial or operational burdens, **never** the underlying technical risk or institutional accountability.

#### Risk Acceptance Record (Plain HTTP on Isolated Lab Network)
* **Decision:** **Conditionally Accepted** for classroom/isolated lab scope only.
* **Risk Owner:** GRC Operations Lead *(Simulated Approval)*.
* **Residual Risk Score:** **Low (2)** ($\text{Likelihood } 1 \times \text{Impact } 2$).
* **Rationale:** Traffic is confined strictly to an isolated host-only subnet (`192.168.56.0/24`) protected by UFW host whitelisting and contains exclusively non-sensitive dummy text.
* **Expiry & Review Date:** **14-day temporary acceptance** (Expires: `2026-11-25`).
* **Mandatory Revocation Triggers:** Any introduction of real/sensitive organizational data, bridging to external/corporate networks, or onboarding of additional client subnets immediately invalidates this acceptance and requires mandatory TLS deployment (Option C).

---

### Step 12: Financial Cost Comparison & Illustrative ALE Calculation

#### First-Year Treatment Option Comparison
Using the formula $\text{First-Year Cost} = \text{Setup} + \text{Labour} + \text{Annual Recurring Cost}$:

| Option | Description | Setup Cost | Labour Calculation | Annual Recurring | First-Year Total |
| :--- | :--- | :---: | :---: | :---: | :---: |
| **Option A** | System & Web Hardening | $0 | $4\text{ hrs} \times \$25/\text{hr} = \$100$ | $50 | **$150** |
| **Option B** | Managed Off-Host Backup | $120 | $0 (vendor-managed) | $\$20/\text{mo} \times 12 = \$240$ | **$360** |
| **Option C** | TLS/HTTPS Deployment | $0 | $3\text{ hrs} \times \$25/\text{hr} = \$75$ | $25 | **$100** |

* **Recommended Combination:** **Option A + Option B ($510 First-Year Total)** for production readiness, or **Option A + Option C ($250 First-Year Total)** if local backups are retained while transitioning to production TLS. Choosing **Option A + Option B ($510)** directly addresses both preventive hardening and off-host disaster recovery resilience.
* **Excluded Costs:** Internal management review overhead, staff training time, VM compute/storage licensing, and potential downtime costs during maintenance windows.

#### Illustrative Backup Scenario — Quantitative ALE Analysis (Option B)
*(Note: Every figure below is strictly a classroom assumption for financial modeling; the technical lab recovery test validates operational capability but does not empirically establish loss frequencies or dollar valuations. Ordinal risk scores are never converted into dollar amounts.)*

* **Assumed Parameters:**
  * $\text{Annual Rate of Occurrence (ARO)} = 0.2$ *(Assumed: 1 major data loss event every 5 years)*
  * $\text{Baseline Single Loss Expectancy (SLE}_{\text{baseline}}) = \$5,000$ *(Assumed)*
  * $\text{Post-Control Single Loss Expectancy (SLE}_{\text{residual}}) = \$1,000$ *(Assumed with verified recovery control)*
  * $\text{First-Year Control Cost (Option B)} = \$360$
* **Calculations:**
  $$\text{Baseline ALE} = \text{ARO} \times \text{SLE}_{\text{baseline}} = 0.2 \times \$5,000 = \mathbf{\$1,000/\text{year}}$$
  $$\text{Residual ALE} = \text{ARO} \times \text{SLE}_{\text{residual}} = 0.2 \times \$1,000 = \mathbf{\$200/\text{year}}$$
  $$\text{Annual Risk Reduction Benefit} = \text{Baseline ALE} - \text{Residual ALE} = \$1,000 - \$200 = \mathbf{\$800/\text{year}}$$
  $$\text{First-Year Net Benefit} = \text{Annual Benefit} - \text{First-Year Cost} = \$800 - \$360 = \mathbf{+\$440}$$

---

### Post-Treatment Residual Risk Register (Reassessment of R1–R4)

| Risk ID | Strategy Applied | Baseline Score | Residual Likelihood | Residual Impact | Residual Score | New Band | Validation Evidence | Owner & Review Trigger |
| :--- | :--- | :---: | :---: | :---: | :---: | :---: | :--- | :--- |
| **R1** | **Avoidance** | 12 (High) | 1 | 2 | **2** | **Low** | `avoidance-ports.txt`, `avoidance-legacy.txt` (Port 8080 closed) | SysAdmin; trigger if port 8080 or `grc-legacy` reappears |
| **R2** | **Mitigation** | 16 (High) | 1 | 3 | **3** | **Low** | `preventive-archive-403.txt`, `preventive-file-403.txt` (HTTP 403) | Web Ops; trigger on Nginx config edit or web root file addition |
| **R3** | **Mitigation** | 9 (Medium) | 1 | 3 | **3** | **Low** | `ufw-allowed-200.txt`, `ufw-blocked-timeout.txt`, `/var/log/ufw.log` | NetSec; trigger on UFW rule change or new subnet host |
| **R4** | **Mitigation / Transfer** | 8 (Medium) | 1 | 2 | **2** | **Low** | `portal-before.sha256` (`OK`), `step10-restored-check.txt` | Backup Admin; trigger on failed monthly restore test or host migration |

---

## 6. Ongoing Monitoring & Operational Handover

To distinguish one-time lab verification results from continuous operational assurance, the following recurring monitoring controls are handed over to operations:

| Control Check | Operational Owner | Frequency | Alert Threshold | Escalation Procedure |
| :--- | :--- | :--- | :--- | :--- |
| **1. Approved Portal Availability** | System Administration | Automated every 5 mins / Daily audit | HTTP status $\neq 200$ on `/public/` or response time $> 3\text{s}$ | Restart Nginx (`systemctl restart nginx`), inspect `grc_error.log`, escalate to Web Ops Lead if unresolved in 15 mins. |
| **2. Unexpected Open Ports & Configuration Drift** | Security Operations | Weekly automated scan | Any listening TCP/UDP port other than `80/tcp` (e.g., `8080/tcp`) or `grc-legacy.service` status $\neq \text{inactive}$ | Immediately stop/disable unauthorized unit, isolate host via UFW, and open security incident ticket. |
| **3. Backup & Recovery Integrity Verification** | Backup Administrator | Monthly | `sha256sum -c` mismatch or test extraction failure in staging directory | Halt backup rotation, inspect disk/archive integrity, and re-run baseline backup immediately. |

---

## 7. Submission Package Inventory (`README` Mapping)
All raw command outputs, configuration snapshots, logs, and screenshots are packaged in this link: https://docs.google.com/document/d/1zBU9nYNYV3MGPl1P-TDyEDW8o5GIQRghN0COl1eQJDA/edit?usp=sharing

* **Step 1–3 (Environment Setup):** `ip-addr-ubuntu.txt`, `ip-addr-kali.txt`, `grc-lab.nginx.conf`
* **Step 4 (Baseline Evidence):** `baseline-time.txt`, `baseline-ports.txt`, `baseline-web.txt`, `baseline-listing.txt`, `baseline-file.txt`, `baseline-legacy.txt`
* **Step 6 (Avoidance Validation):** `avoidance-ports.txt`, `avoidance-legacy.txt`
* **Step 7 (Preventive Web Hardening):** `preventive-public-200.txt`, `preventive-archive-403.txt`, `preventive-file-403.txt`, `preventive-root-403.txt`
* **Step 8–9 (Firewall & Log Correlation):** `ufw-allowed-200.txt`, `ufw-blocked-time.txt`, `ufw-blocked-timeout.txt`, `grc_access.log.extract`, `ufw.log.extract`
* **Step 10 (Backup & Recovery):** `portal-before.sha256`, `step10-failed-check.txt`, `step10-restored-check.txt`
* **Visual Proof:** Terminal captures (`kl1.jpg`–`kl9.PNG`, `ubt1.PNG`)
