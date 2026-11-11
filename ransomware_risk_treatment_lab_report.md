# Practical Lab: Ransomware Risk Treatment — Case Analysis and Management
**Course:** GRC103 — Risk Assessment and Management Techniques  
**Institution:** International Cybersecurity and Digital Forensics Academy (ICDFA)  
**Student Name:** [Insert Your Name Here]  
**Registration Number:** [Insert Registration Number Here]  
**Official Case Source:** [Health Service Executive (HSE) Cyber-attack Briefing](https://www2.hse.ie/services/cyber-attack/what-happened/)  

---

## Executive Summary & Fact Separation

To establish a clear foundation for risk management, real incident facts from the 2021 Health Service Executive (HSE) attack in Ireland are explicitly separated from the fictional scenario assumptions for Northbridge Community Health.

### Real HSE Incident Facts (2021)
1. **Initial Vector & Dwell Time:** The intrusion began on March 18, 2021, when an employee opened a malicious Microsoft Excel file attached to a phishing email. Threat actors maintained undetected access to the network for approximately eight weeks (until May 14, 2021) before triggering the Conti ransomware payload.
2. **Impact & Ransom Policy:** The attack encrypted critical clinical and administrative systems nationwide, forcing hospitals to revert to paper-based operations. The Irish government and HSE maintained a strict policy against paying the ransom demand. Full system recovery required over four months of remediation work.

### Fictional Exercise Assumptions (Northbridge Community Health)
* Northbridge operates three healthcare clinics under a strict first-year treatment budget of **$100,000**.
* An unused supplier workflow remains enabled across the infrastructure.
* System backup restoration procedures have never been formally validated or tested.
* User-reported phishing emails have no assigned escalation owner.
* Essential clinical bookings must remain operational during an incident.

---

## Task 1: Risk Register & Initial Assessment

Risk scores are calculated using a $1 \text{ to } 5$ scale for Likelihood ($L$) and Impact ($I$), where:

$$\text{Risk Score} = \text{Likelihood } (L) \times \text{Impact } (I)$$

### Scoring Thresholds
* **Low (1–4):** Acceptable under normal operational oversight.
* **Medium (5–9):** Requires monitoring and mitigation planning.
* **High (10–16):** Requires mitigation and formal escalation to senior management/board.
* **Critical (17–25):** Unacceptable; cannot be accepted; requires immediate treatment.

### Initial Risk Register

| Risk ID | Asset / Process | Threat | Weakness / Vulnerability | Business Impact | Likelihood (1–5) | Impact (1–5) | Score & Rating | Initial Risk Owner | Rating Rationale |
| :--- | :--- | :--- | :--- | :--- | :---: | :---: | :---: | :--- | :--- |
| **R-01** | Clinical Booking & Patient Database | Ransomware / Malware Encryption | Untested backups & legacy operational dependencies | Complete inability to schedule appointments; severe patient care disruption | 4 | 5 | **20 (Critical)** | Head of IT Operations | Likelihood is high due to lack of backup testing. Impact is maximum because clinical care relies on operational bookings. |
| **R-02** | Electronic Medical Records (EMR) | External Threat Actor / Exfiltration | Flat network structure; unmonitored lateral movement | Sensitive data theft, regulatory fines, and loss of public trust | 4 | 4 | **16 (High)** | Data Protection Officer | Network gaps allow attackers to pivot into data stores once initial access is gained. |
| **R-03** | Supply Chain Interface | Unauthorized Third-Party Entry | Active, unmonitored supplier workflow left enabled | Supply chain compromise and unauthorized network access vector | 3 | 4 | **12 (High)** | Vendor Management Lead | Unused external connections create unnecessary attack paths that bypass primary controls. |
| **R-04** | User Endpoints & Email Gateway | Spear-Phishing / Malicious Attachment | Lack of awareness training & unassigned report ownership | Delayed detection of initial intrusion, extending attacker dwell time | 5 | 3 | **15 (High)** | Information Security Manager | High likelihood due to staff exposure to phishing without clear reporting escalation paths. |

---

## Task 2: Initial Treatment Portfolio & Budget Allocation

### Selected Treatment Options (Cap: $100,000)

| Option ID | Description | Strategy Type | Cost | Targeted Risk(s) | Justification |
| :---: | :--- | :--- | :---: | :---: | :--- |
| **A** | Retire the unused supplier workflow | Risk Avoidance | $5,000 | R-03 | Completely eliminates an unnecessary third-party entry point at minimal cost. |
| **C** | Protected backups, restoration tests, and recovery plan | Risk Mitigation | $30,000 | R-01 | Addresses the critical backup weakness, ensuring system restoration and continuity. |
| **D** | Managed detection and incident escalation service | Risk Mitigation | $35,000 | R-02, R-04 | Provides 24/7 monitoring to detect intrusion early and eliminate long attacker dwell times. |
| **E** | Targeted awareness training and reporting process | Risk Mitigation | $10,000 | R-04 | Reduces phishing susceptibility and creates a designated owner for reported threats. |

### Financial Summary
* **Total Spending:** $\$5,000 + \$30,000 + \$35,000 + \$10,000 = \mathbf{\$80,000}$
* **Remaining Budget Reserve:** $\$100,000 - \$80,000 = \mathbf{\$20,000}$

### Analysis of Portfolio Strategy
* **Avoidance & Mitigation:** Option A avoids unnecessary exposure. Options C, D, and E mitigate core operational risks by hardening controls and reducing detection time.
* **Evaluation of Transfer (Option G - $20,000):** Insurance transfer was evaluated but not selected initially. Insurance does not prevent operational outages or secure assets; investing directly in technical and operational controls provides immediate risk reduction. The $20,000 remaining budget is retained as a liquidity buffer.
* **Time-Limited Acceptance:** Residual risk for R-02 (EMR exfiltration) is accepted for a maximum of 90 days while Option D is deployed. Full network segmentation (Option F) is deferred due to cost constraints.

### Rejection Rationale for Unselected Options
* **Option B ($25,000 - MFA & access review):** Exceeded the initial budget when combined with mandatory backup restoration (Option C) and managed detection (Option D).
* **Option F ($40,000 - Network segmentation):** High relative cost (40% of total budget) would prevent implementing essential backup and detection measures.

---

## Task 3: Retained Financial Exposure & Insurance Calculations

Calculations use the parameters of **Option G** (Deductible: $\$25,000$; Maximum Payout: $\$250,000$; Annual Premium: $\$20,000$).

### Mathematical Formulae

$$\text{Insurer Payment} = \min\Big(\max(\text{Covered Loss} - \$25,000,\, 0),\, \$250,000\Big)$$

$$\text{Retained Loss} = \text{Covered Loss} - \text{Insurer Payment}$$

$$\text{Total First-Year Outlay} = \text{Retained Loss} + \text{Insurance Premium } (\$20,000)$$

---

### Scenario A: Covered Loss of $180,000

1. **Insurer Payment:**
   $$\max(\$180,000 - \$25,000,\, 0) = \$155,000$$
   $$\min(\$155,000,\, \$250,000) = \mathbf{\$155,000}$$

2. **Retained Loss:**
   $$\$180,000 - \$155,000 = \mathbf{\$25,000} \quad \text{(Equals the deductible)}$$

3. **Total Outlay:**
   $$\$25,000 \text{ (Retained Loss)} + \$20,000 \text{ (Premium)} = \mathbf{\$45,000}$$

---

### Scenario B: Covered Loss of $400,000

1. **Insurer Payment:**
   $$\max(\$400,000 - \$25,000,\, 0) = \$375,000$$
   $$\min(\$375,000,\, \$250,000) = \mathbf{\$250,000} \quad \text{(Capped at policy maximum)}$$

2. **Retained Loss:**
   $$\$400,000 - \$250,000 = \mathbf{\$150,000} \quad \text{(\$25k Deductible + \$125k Uninsured Loss)}$$

3. **Total Outlay:**
   $$\$150,000 \text{ (Retained Loss)} + \$20,000 \text{ (Premium)} = \mathbf{\$170,000}$$

---

### Policy Exclusion Clause Note
If a loss is excluded by the insurer (e.g., failure to maintain required baseline security controls), **Northbridge Community Health bears 100% of the financial loss**. Contractual transfer or insurance policies do not remove organizational accountability.

---

## Task 4: Response to Operational & Cost Changes

### Scenario Change Event
1. An initial restoration test **fails**.
2. Clinics can sustain manual paper bookings for **a maximum of four hours**.
3. **Option B (MFA rollout)** increases in cost from $\$25,000$ to **$\$35,000$**.

### Portfolio Revision & Reallocation
Because backup restoration failed and paper processing is strictly limited to four hours, backup validation (Option C) is vital for business survival. To fund the mandatory price increase for Option B ($35,000), Option D ($35,000) must be deferred.

| Option ID | Description | Status | Revised Cost | Budget Impact |
| :---: | :--- | :--- | :---: | :--- |
| **A** | Retire unused supplier workflow | Retained | $5,000 | Unchanged |
| **B** | MFA rollout and account review | Added (Revised Cost) | $35,000 | Cost increased by +$10,000 |
| **C** | Protected backups & recovery plan | Retained | $30,000 | Priority increased due to test failure |
| **E** | Awareness training & reporting | Retained | $10,000 | Unchanged |
| **D** | Managed detection service | **Deferred** | $0 | Savings of -$35,000 used to fund Option B |

### Revised Financial Summary
* **Revised Total Spending:** $\$5,000 + \$35,000 + \$30,000 + \$10,000 = \mathbf{\$80,000}$
* **Remaining Reserve:** $\$100,000 - \$80,000 = \mathbf{\$20,000}$

### Risk Ownership & Escalation
* **Deferred Risk Owner:** The Information Security Manager assumes temporary ownership of the unmitigated monitoring gap resulting from deferring Option D.
* **Board Escalation:** Deferring managed detection (Option D) under a 4-hour manual backup limit creates high risk exposure for undetected intruder dwell time. This operational decision requires **formal escalation to the Board of Directors**.

---

## Task 5: 30-Day Implementation Plan & Residual Risk

### 30-Day Treatment Plan

| Action Item | Option | Assigned Owner | Allocation | Target Date | Effectiveness Test Method |
| :--- | :---: | :--- | :---: | :---: | :--- |
| Decommission unused supplier workflow | A | Vendor Manager | $5,000 | Day 7 | Firewall rule audit and external interface port scan |
| Remediate backups & rerun restoration test | C | IT Operations Lead | $30,000 | Day 14 | Full bare-metal system restoration drill under timed conditions |
| Enforce MFA across all clinic accounts | B | IT Systems Lead | $35,000 | Day 21 | Automated access control check and unauthorized login attempt test |
| Conduct phishing training & establish escalation | E | Security Training Lead | $10,000 | Day 30 | Simulated phishing campaign targeting a click rate of $<5\%$ |

---

### Proposed Residual Risk Scores

*Note: Controls are treated as unproven until the corresponding test method is successfully verified.*

| Risk ID | Risk Name | Initial Score | Proposed Residual Score | Residual Level | Assumptions & Key Controls |
| :---: | :--- | :---: | :---: | :---: | :--- |
| **R-01** | Booking Disruption | 20 (Critical) | **4 (Low)** | Low | Assumes Option C backup restoration passes validation within 14 days ($L=1, I=4$). |
| **R-02** | EMR Data Loss | 16 (High) | **6 (Medium)** | Medium | Assumes MFA prevents unauthorized entry ($L=2, I=3$); residual risk remains due to deferred Option D. |
| **R-03** | Supplier Exposure | 12 (High) | **2 (Low)** | Low | Assumes supplier workflow is decommissioned and confirmed via port scans ($L=1, I=2$). |
| **R-04** | Delayed Detection | 15 (High) | **6 (Medium)** | Medium | Assumes training lowers click rates ($L=2, I=3$); lack of 24/7 detection service maintains medium risk. |

---

### Time-Limited Risk Acceptance Record

* **Accepted Risk:** R-04 (Detection gap due to deferral of Option D).
* **Risk Owner:** Information Security Manager.
* **Expiry Date:** 90 Days from approval.
* **Review Trigger:** Any detected security incident or changes to available security funding.
* **Simulated Approver:** Chief Executive Officer / Board Risk Committee.

---

## Board Memorandum

**TO:** Board of Directors, Northbridge Community Health  
**FROM:** Risk Assessment & Management Lead  
**DATE:** November 11, 2026  
**SUBJECT:** Executive Briefing: Revised Ransomware Risk Treatment Plan ($100,000 Cap)  

### 1. Requested Decision
Board approval for the revised **$80,000** risk treatment portfolio, preserving a **$20,000** contingency buffer under our fixed first-year budget.

### 2. Operational Context & Priority Shifts
Following a failed backup restoration test and confirmation that clinic operations can sustain paper-based bookings for only **four hours**, our treatment priorities were updated. Restoring tested, immutable recovery capabilities (Option C: $30,000) is necessary to ensure clinical continuity and mitigate critical operational risks.

### 3. Revised Budget Allocation
To secure system authentication and close external access points, we have allocated resources to:
* **Option A ($5,000):** Retiring the unused supplier workflow (Avoidance).
* **Option B ($35,000):** Mandating MFA rollout following an updated vendor price increase (Mitigation).
* **Option C ($30,000):** Remediating backups and validating recovery workflows (Mitigation).
* **Option E ($10,000):** Delivering targeted awareness training and establishing incident reporting (Mitigation).

### 4. Unresolved Risks & Escalation
Funding the MFA price increase required deferring the Managed Detection Service (Option D: $35,000). This creates an unmitigated monitoring gap owned by the Information Security Manager. Given our 4-hour limit on manual bookings, operating without 24/7 detection exceeds our target risk tolerance and is submitted to the Board for formal risk sign-off.
```

Let me know if you would like me to adjust any of the numerical figures or calculations before you submit this to your repository!