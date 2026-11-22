# NORTHBRIDGE SERVICES — SECURITY RISK MONITORING & MANAGEMENT REPORT
**Student Name: Confidence Chinwuko** 
**Registration Number: C11-26-CGRCE-17558** 
**Course:** GRC103 Module 4 Lab 2
**Report Date:** 22 November 2026

---

## PART 1: SPREADSHEET APPLICATION USING GOOGLE SHEET.
Solution attached here:: https://docs.google.com/spreadsheets/d/18dFfq5L6fXVwIbrxzKumAiWvOxaUA83cERfiP2IeATc/edit?usp=sharing


---


## PART 2: 
## SECTION 1: ONE-PAGE MANAGEMENT REPORT (TASK 5)

**To:** Head of Operations, Northbridge Services  
**From:** GRC Analyst  
**Date:** 22 November 2026  
**Subject:** March Control Performance Review, Threshold Breaches, and Escalation Actions  

### 1. Executive Summary & March Control Status
In March, all five monitored security and operational risk indicators breached Red classroom thresholds, representing a consistent three-month deterioration from January baseline performance. Per operational escalation rules, Red indicators and High-rated risks require formal escalation to responsible managers within one working day.

| Key Risk Indicator (KRI) | Jan | Feb | Mar | Mar Status | Target (Green) | Accountable Owner |
| :--- | :---: | :---: | :---: | :---: | :---: | :--- |
| Monitoring coverage (%) | 98.0% | 95.0% | 90.0% | **RED** | $\ge 98.0\%$ | Infrastructure & Endpoint Lead |
| Timely critical-alert review (%) | 95.0% | 80.0% | 70.0% | **RED** | $\ge 95.0\%$ | Security Operations (SOC) Lead |
| Restore-test success (%) | 100.0% | 90.0% | 80.0% | **RED** | $100.0\%$ | Backup & Recovery Lead |
| Overdue high-risk actions (%) | 10.0% | 25.0% | 40.0% | **RED** | $\le 10.0\%$ | IT Risk & Compliance Lead |
| Confirmed unauthorised changes (Count) | 1 | 3 | 5 | **RED** | `0` | Infrastructure & Endpoint Lead |

Chart 1 from the Google Sheets link here: "Northbridge Services — 3-Month Control Rate Trends (%)"
https://docs.google.com/spreadsheets/d/18dFfq5L6fXVwIbrxzKumAiWvOxaUA83cERfiP2IeATc/edit?usp=sharing

### 2. Three Priority Concerns in March
1. **Endpoint Monitoring Blind Spot & Rising Confirmed File Changes:** Monitoring coverage fell from 98.0% (Jan) to 90.0% (Mar), leaving **12 of 120 eligible endpoints unmonitored**, alongside **5 confirmed unauthorised file changes** (up from 1 in Jan and 3 in Feb). Unmonitored assets lack telemetry visibility, elevating the risk of undetected compromise or system tampering.
2. **Deteriorating Critical-Alert Triage SLA:** Critical alerts doubled from 20 (Jan) to 40 (Mar), while 24-hour review completion dropped from 95.0% to 70.0% (12 critical alerts unreviewed within 24 hours). Delayed review increases potential attacker dwell time if any unreviewed alert reflects active exploitation.
3. **Declining Backup Restore Reliability & Remediation Backlog:** Restore-test success dropped from 100.0% (10/10) to 80.0% (8/10), while overdue high-risk actions rose from 10.0% (1/10) to 40.0% (6/15). Failed restore tests threaten recovery objectives during an outage, and overdue actions leave known high-risk exposures open past agreed deadlines.

### 3. Decisions & Resources Requested from Operations
* **Mandatory Onboarding Gate:** Approve an immediate policy enforcement blocking production network access for newly provisioned endpoints until monitoring agents report active telemetry (Target: Report Date + 5 days).
* **Temporary SOC Triage Surge & Rule Tuning:** Authorize temporary analyst shift reallocation and alert-rule tuning support to clear the 12-alert backlog and restore $\ge 95.0\%$ 24-hour triage compliance (Target: Report Date + 3 days).
* **Priority Remediation & Backup Engineering Allocation:** Direct system owners to resolve the 6 overdue high-risk actions and allocate backup engineering time to remediate the 2 failed restore configurations (Target: Report Date + 5 to 7 days).

### 4. Governance Schedule & Analytical Caveats
* **Next Formal Review:** **22 December 2026** (30 days from report date), preceded by a 7-day Red-indicator containment checkpoint on **29 November 2026**.
* **Data & Forecasting Caveat:** All figures in this assessment are fictional classroom dataset values. Three monthly observations (January–March) provide an operational snapshot of short-term deterioration but are statistically insufficient to establish a reliable long-term predictive forecast.

---

## SECTION 2: INTERPRETATION OF MARCH RESULTS (TASK 2)

### 2.1 Detailed Analysis of Priority Concerns (Observation vs. Possible Cause)
* **Priority Concern 1 — Expanding Monitoring Gap & Unauthorised File Changes:**
  * *Figures Cited:* Monitoring coverage declined from `98.0%` (`98/100`) in January to `95.0%` (`95/100`) in February and `90.0%` (`108/120`) in March (`Red`). Confirmed post-review unauthorised file changes rose from `1` (`Amber`) to `3` (`Red`) to `5` (`Red`).
  * *Business Consequence:* Blind spots across 12 endpoints prevent detection of unauthorised binaries, privilege escalation, or configuration drift, while repeated unauthorised file modifications indicate weakening host integrity controls.
  * *Observation vs. Possible Cause:* We observe 12 unmonitored endpoints and 5 confirmed unauthorised file changes in March. Possible causes include manual endpoint onboarding gaps during fleet expansion, misconfigured file-integrity baselines, or legitimate administrative changes bypassing change-control approval. Co-movement between unmonitored endpoints and confirmed file changes does not prove causation.
* **Priority Concern 2 — Timely Critical-Alert Review Degradation:**
  * *Figures Cited:* Critical alerts rose from `20` (Jan) to `30` (Feb) to `40` (Mar), while alerts reviewed within 24 hours fell from `95.0%` (`19/20`, `Green`) to `80.0%` (`24/30`, `Red`) and `70.0%` (`28/40`, `Red`), leaving `12` critical alerts unreviewed within SLA.
  * *Business Consequence:* Slow triage delays containment and eradication if a critical alert signals a true compromise, increasing potential operational downtime and data exposure.
  * *Observation vs. Possible Cause:* We observe a 100% increase in critical alert volume paired with a 25-percentage-point drop in 24-hour review completion. Possible causes include fixed SOC staffing capacity facing doubled alert volume, noisy detection thresholds, or triage workflow bottlenecks. Not every critical alert represents a confirmed security incident; each requires analyst triage to determine validity.
* **Priority Concern 3 — Backup Restore Failures & Overdue High-Risk Remediation:**
  * *Figures Cited:* Restore-test success dropped from `100.0%` (`10/10`, `Green`) to `90.0%` (`9/10`, `Amber`) to `80.0%` (`8/10`, `Red`), meaning 2 of 10 March tests failed. High-risk actions overdue at month-end rose from `10.0%` (`1/10`, `Green`) to `25.0%` (`3/12`, `Red`) to `40.0%` (`6/15`, `Red`).
  * *Business Consequence:* Unreliable backups invalidate recovery time and recovery point objectives (RTO/RPO) during ransomware or hardware failure events, while overdue high-risk actions leave known severe vulnerabilities unmitigated.
  * *Observation vs. Possible Cause:* We observe 2 failed restore tests and 6 overdue high-risk actions in March. Possible causes include corrupted backup snapshots, unupdated restore scripts after system changes, and competing operational priorities delaying remediation owners.

### 2.2 Impact of Eligible Endpoint Growth & March Coverage Gap Calculation
* **Effect of Eligible Endpoint Increase:** Eligible endpoints remained `100` in January and February before expanding by `+20` endpoints (`+20.0%`) to `120` in March. Although actively monitored endpoints grew in absolute count from `95` in February to `108` in March (`+13` endpoints), the onboarding rate of new endpoints outpaced monitoring agent deployment (`13` newly monitored vs. `20` newly eligible). Consequently, looking solely at the raw count (`95` to `108`) falsely suggests improving coverage, whereas the percentage indicator accurately exposes a `5.0`-percentage-point drop into `Red` status (`95.0%` to `90.0%`).
* **March Coverage Gap Calculation:**
  {March Coverage Gap} = 120 { (Eligible endpoints)} - 108 { (Actively monitored endpoints)} = \mathbf{12 { unmonitored endpoints}}
  *(This represents a 6-fold increase in unmonitored assets compared to January's gap of 2 endpoints and more than double February's gap of 5 endpoints.)*

---

## SECTION 3: UPDATED RISK REGISTER (TASK 3)

**Scoring Matrix:** Likelihood ($1\text{–}5$) $\times$ Impact ($1\text{–}5$) | **Scale:** Low (`1–4`), Medium (`5–9`), High (`10–16`), Critical (`17–25`).  
**Governance Rule:** Indicator color is not automatically a risk score; scores below reflect technical likelihood and operational impact. Both Red indicators (within 1 working day) and High/Critical risk scores require formal management escalation.

| Risk ID | Asset / Process | Risk Statement | March Evidence | Existing Control | L | I | Score & Rating | Accountable Owner | Planned Action | Review Date |
| :--- | :--- | :--- | :--- | :--- | :---: | :---: | :---: | :--- | :--- | :---: |
| **RSK-01** | Endpoint Fleet & Provisioning Process (120 endpoints) | Unmonitored endpoints and unauthorised host file modifications may allow undetected compromise or integrity loss across operational systems. | 108/120 (90.0%) monitored; 12-endpoint gap; 5 confirmed unauthorised file changes (Red). | Endpoint monitoring enrollment and post-alert file integrity review. | 4 | 4 | **16 (High)** *(Likely due to rapid fleet growth; major integrity impact)* | Infrastructure & Endpoint Lead | Enrol 12 unmonitored endpoints and enforce automated onboarding agent checks. | 22 Dec 2026 |
| **RSK-02** | Security Alert Triage & SOC Operations | Delayed review of critical security alerts beyond 24 hours may prolong adversary dwell time and delay incident containment. | 28/40 (70.0%) reviewed within 24h; 12 critical alerts exceeded 24h SLA (Red). | 24-hour critical-alert triage SLA and analyst alert queue. | 4 | 4 | **16 (High)** *(Likely given 40-alert load; major delay in breach response)* | Security Operations (SOC) Lead | Clear March backlog, rebalance triage coverage, and tune noisy critical rules. | 22 Dec 2026 |
| **RSK-03** | Enterprise Backup & Restoration Process | Failed backup restorations may prevent timely recovery of critical services and data following a destructive cyberattack or outage. | 8/10 (80.0%) restore tests succeeded; 2 restore tests failed in March (Red). | Scheduled monthly backup restoration testing (10 tests/month). | 3 | 5 | **15 (High)** *(Moderate failure rate; severe business continuity impact)* | Backup & Recovery Lead | Remediate 2 failed restore configurations and execute verified re-tests. | 22 Dec 2026 |
| **RSK-04** | High-Risk Remediation & Vulnerability Management | High-risk remediation actions remaining open past due dates leave severe known control weaknesses exposed to exploitation. | 6/15 (40.0%) high-risk actions overdue at March month-end (Red). | Monthly high-risk action register and due-date tracking. | 4 | 4 | **16 (High)** *(Likely per 3-month climb; major exposure from open risks)* | IT Risk & Compliance Lead | Escalate 6 overdue items with binding dates and institute weekly blocker reviews. | 22 Dec 2026 |

---

## SECTION 4: ACTION AND ASSURANCE PLAN (TASK 4)

*Note: All actions below are proposed remediation plans relative to the Report Date (`22 November 2026`) and remain **Open / Not Completed** pending closure evidence and outcome testing.*

| Risk ID | Accountable Owner | Short-Term Containment Action & Deadline | Longer-Term Improvement Action & Deadline | Evidence Required for Closure | Outcome Test (Assurance Verification) | Status |
| :--- | :--- | :--- | :--- | :--- | :--- | :---: |
| **RSK-01** | Infrastructure & Endpoint Lead | Identify all 12 unmonitored endpoints, deploy active agents, and verify containment of the 5 unauthorised file changes. **(Report Date + 5 days: 27 Nov 2026)** | Integrate mandatory monitoring agent enrollment checks into standard endpoint provisioning and NAC onboarding gates. **(Report Date + 30 days: 22 Dec 2026)** | Reconciled 120-endpoint asset list showing 100% active agent heartbeat and signed investigation tickets for all 5 file changes. | Provision 5 test/new endpoints and verify 100% automatically report telemetry within 24 hours without manual intervention. | Open |
| **RSK-02** | Security Operations (SOC) Lead | Triage all 12 aging March critical alerts and assign dedicated shift coverage to eliminate queue backlog. **(Report Date + 3 days: 25 Nov 2026)** | Audit high-volume critical alert rules to eliminate false-positive noise and establish dynamic tier-1 surge escalation thresholds. **(Report Date + 21 days: 13 Dec 2026)** | SIEM queue export showing zero unreviewed March critical alerts and updated alert-tuning change records. | Sample critical alerts across a consecutive 7-day operational window and verify $\ge 95.0\%$ have documented triage within 24 hours. | Open |
| **RSK-03** | Backup & Recovery Lead | Perform root-cause analysis on the 2 failed March restore tests, repair backup job configurations, and re-run restores. **(Report Date + 5 days: 27 Nov 2026)** | Implement automated pre-test backup integrity checksums and standardized restoration runbooks across all critical systems. **(Report Date + 30 days: 22 Dec 2026)** | Root-cause analysis report, updated backup job logs, and signed restore verification records for the 2 failed targets. | Execute a full end-to-end verified restoration of the previously failed datasets/VMs and confirm 100% data integrity and boot/service availability. | Open |
| **RSK-04** | IT Risk & Compliance Lead | Escalate all 6 overdue high-risk actions to department heads, document blockers, and lock binding remediation dates. **(Report Date + 7 days: 29 Nov 2026)** | Deploy automated 7-day and 3-day pre-due-date escalation alerts and require dependency sign-off before setting target dates. **(Report Date + 25 days: 17 Dec 2026)** | Updated risk treatment tracker signed by action owners with documented closure artifacts for completed overdue items. | Audit the April/next monthly cycle close and verify overdue high-risk actions drop to $\le 10.0\%$ with validated closure artifacts. | Open |
