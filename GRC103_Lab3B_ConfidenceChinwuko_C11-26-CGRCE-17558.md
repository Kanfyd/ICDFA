# Lab 3B: Advanced Cybersecurity Risk Quantification and Control Investment Analysis

**Student Name:** Confidence Chinwuko
**Registration Number:** C11-26-CGRCE-17558
**Course:** GRC103 – Risk Analysis and Evaluation  
**Institution:** International Cybersecurity and Digital Forensics Academy (ICDFA)  
**Organization:** SecureBank Financial  
**System Evaluated:** "SecureMobile" Banking Platform  
**Role:** Lead GRC Risk Analyst  

---

## Executive Summary

This submission details a quantitative cybersecurity risk assessment of SecureBank Financial’s "SecureMobile" platform serving 500,000 active customers. By converting technical penetration testing findings into monetary metrics—specifically Single Loss Expectancy (SLE), Annual Rate of Occurrence (ARO), Annualized Loss Expectancy (ALE), and Return on Investment (ROI)—this report establishes a clear financial business case for deploying defensive controls to reduce baseline risk exposure down to residual risk levels.

---

## Phase 1: Risk Exposure Calculation

### Task 1: Calculate Annualized Loss Expectancy (ALE)

The primary quantitative metrics are defined as:
$$\text{SLE} = \text{Asset Value / Impact per Incident}$$
$$\text{ARO} = \text{Probability of Exploitation per Year}$$
$$\text{ALE} = \text{SLE} \times \text{ARO}$$

#### Detailed Step-by-Step Mathematical Derivations:

1. **Vulnerability 1: API Authentication Bypass**
   * **Given:** Maximum Single Incident Loss = $5,000,000; Exploit Probability = 15% (0.15)
   * **SLE:** $\$5,000,000$
   * **ARO:** $0.15$
   * **ALE Calculation:** 
     $$\text{ALE}_1 = \$5,000,000 \times 0.15 = \mathbf{\$750,000}$$


2. **Vulnerability 2: Database Injection Vulnerability**
   * **Given:** 500,000 customer profiles at risk; Cost per Record = $250; Exploit Probability = 25% (0.25)
   * **SLE Calculation:** 
     $$\text{SLE}_2 = 500,000 \text{ records} \times \$250/\text{record} = \mathbf{\$125,000,000}$$

   * **ARO:** $0.25$
   * **ALE Calculation:** 
     $$\text{ALE}_2 = \$125,000,000 \times 0.25 = \mathbf{\$31,250,000}$$


3. **Vulnerability 3: Session Hijacking**
   * **Given:** 5,000 simultaneous sessions at risk; Average Loss per Account = $1,500; Exploit Probability = 40% (0.40)
   * **SLE Calculation:** 
     $$\text{SLE}_3 = 5,000 \text{ accounts} \times \$1,500/\text{account} = \mathbf{\$7,500,000}$$

   * **ARO:** $0.40$
   * **ALE Calculation:** 
     $$\text{ALE}_3 = \$7,500,000 \times 0.40 = \mathbf{\$3,000,000}$$


* **Total Baseline Exposure Calculation:**
  $$\text{Total Baseline ALE} = \text{ALE}_1 + \text{ALE}_2 + \text{ALE}_3 = \$750,000 + \$31,250,000 + \$3,000,000 = \mathbf{\$35,000,000}$$


---

### Task 2: Prioritize Risks (Risk Prioritization Matrix)

| Vulnerability | SLE ($) | ARO | Base ALE ($) | Risk Priority Level | Primary Affected Asset |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Database Injection Vulnerability** | $125,000,000 | 0.25 | $31,250,000 | **Priority 1 (CRITICAL)** | Customer Profile Database |
| **Session Hijacking** | $7,500,000 | 0.40 | $3,000,000 | **Priority 2 (HIGH)** | User Session Tokens |
| **API Authentication Bypass** | $5,000,000 | 0.15 | $750,000 | **Priority 3 (MEDIUM-HIGH)** | Transaction Processing Engine |

---

### Task 3: Risk Visualizations & Heat Map

#### 1. Baseline ALE Comparison (Bar Chart)
```text
Vulnerability Financial Loss Exposure (ALE in Millions USD)
===================================================================================
Database Injection  | [##################################################] $31.25M
Session Hijacking   | [#####] $3.00M
API Auth Bypass     | [#] $0.75M
===================================================================================
Total Base Risk Exposure: $35.00 Million

---

2. Risk Distribution Breakdown
Risk Proportion by Loss Contribution (% Share of $35M Total ALE)
===================================================================================
Database Injection  : (89.29%) | [========================================]
Session Hijacking   : ( 8.57%) | [==]
API Auth Bypass     : ( 2.14%) | [=]
===================================================================================

---

3. Quantitative Risk Heat Map Matrix
PROBABILITY (ARO)
  High (0.40)    |                        | [Session Hijacking]    | 
                 |                        | SLE: $7.5M | ALE: $3M  | 
  Medium (0.25)  |                        |                        | [Database Injection]
                 |                        |                        | SLE: $125M | ALE: $31.25M
  Low (0.15)     | [API Auth Bypass]      |                        | 
                 | SLE: $5M | ALE: $0.75M |                        | 
                 +------------------------+------------------------+------------------------
                 | Low Impact (<$6M)      | Medium Impact ($6M-$50M)| High Impact (>$50M)
                                          IMPACT (SLE)


---


Task 4: Cost-Benefit & Financial Metrics Analysis

#### Formulas Used:
* **Gross Risk Reduction ($):** $\text{Target ALE} \times \text{Control Effectiveness (\%)}$[cite: 33]
* **Net Annual Cost:** $\text{Year 1 Investment} + \text{Annual Maintenance}$[cite: 33]
* **ROI (%):** $\left(\frac{\text{Gross Risk Reduction} - \text{Initial Investment}}{\text{Initial Investment}}\right) \times 100$[cite: 33]
* **Payback Period (Months):** $\left(\frac{\text{Initial Investment}}{\text{Annual Risk Reduction - Maintenance}}\right) \times 12$[cite: 33]

#### Detailed Computations per Control Option:

1. **Control 1: Advanced API Security Gateway**
   * Target Vulnerability: API Authentication Bypass ($\text{ALE} = \$750,000$)[cite: 33]
   * Initial Investment: $350,000 | Annual Maintenance: $50,000[cite: 33]
   * Control Effectiveness: 90%[cite: 33]
   * Gross Risk Reduction: $\$750,000 \times 0.90 = \mathbf{\$675,000}$[cite: 33]
   * Net Annual Savings: $\$675,000 - \$50,000 = \$625,000$[cite: 33]
   * ROI Calculation:
     $$\text{ROI} = \left(\frac{\$675,000 - \$350,000}{\$350,000}\right) \times 100 = \mathbf{92.86\%}$$[cite: 33]
   * Payback Period:
     $$\text{Payback} = \left(\frac{\$350,000}{\$675,000 - \$50,000}\right) \times 12 = \mathbf{6.72 \text{ months}}$$[cite: 33]

2. **Control 2: Web Application Firewall (WAF)**
   * Target Vulnerability: Database Injection Vulnerability ($\text{ALE} = \$31,250,000$)[cite: 33]
   * Initial Investment: $150,000 | Annual Maintenance: $25,000[cite: 33]
   * Control Effectiveness: 75%[cite: 33]
   * Gross Risk Reduction: $\$31,250,000 \times 0.75 = \mathbf{\$23,437,500}$[cite: 33]
   * Net Annual Savings: $\$23,437,500 - \$25,000 = \$23,412,500$[cite: 33]
   * ROI Calculation:
     $$\text{ROI} = \left(\frac{\$23,437,500 - \$150,000}{\$150,000}\right) \times 100 = \mathbf{15,525.00\%}$$[cite: 33]
   * Payback Period:
     $$\text{Payback} = \left(\frac{\$150,000}{\$23,437,500 - \$25,000}\right) \times 12 = \mathbf{0.08 \text{ months}}$$[cite: 33]

3. **Control 3: Multi-Factor Authentication (MFA) Enhancement**
   * Target Vulnerability: Session Hijacking ($\text{ALE} = \$3,000,000$)[cite: 33]
   * Initial Investment: $200,000 | Annual Maintenance: $30,000[cite: 33]
   * Control Effectiveness: 95%[cite: 33]
   * Gross Risk Reduction: $\$3,000,000 \times 0.95 = \mathbf{\$2,850,000}$[cite: 33]
   * Net Annual Savings: $\$2,850,000 - \$30,000 = \$2,820,000$[cite: 33]
   * ROI Calculation:
     $$\text{ROI} = \left(\frac{\$2,850,000 - \$200,000}{\$200,000}\right) \times 100 = \mathbf{1,325.00\%}$$[cite: 33]
   * Payback Period:
     $$\text{Payback} = \left(\frac{\$200,000}{\$2,850,000 - \$30,000}\right) \times 12 = \mathbf{0.85 \text{ months}}$$[cite: 33]

#### Financial Evaluation Summary Table:

| Control Option | Initial Investment | Annual Maintenance | Target ALE | Risk Reduction ($) | ROI (%) | Payback Period |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Web Application Firewall (WAF)**[cite: 33] | $150,000[cite: 33] | $25,000[cite: 33] | $31,250,000 | $23,437,500 | **15,525.00%** | **0.08 Months** |
| **MFA Enhancement**[cite: 33] | $200,000[cite: 33] | $30,000[cite: 33] | $3,000,000 | $2,850,000 | **1,325.00%** | **0.85 Months** |
| **API Security Gateway**[cite: 33] | $350,000[cite: 33] | $50,000[cite: 33] | $750,000 | $675,000 | **92.86%** | **6.72 Months** |
| **TOTAL COMBINED PORTFOLIO** | **$700,000** | **$105,000** | **$35,000,000** | **$26,962,500** | **3,751.79%** | **0.31 Months** |

---

## Bonus Challenge: Combined Risk-Control Matrix

The matrix below optimizes control selection based on capital budget allocations, displaying current exposure versus residual risk posture:

| Vulnerability Target | Current ALE ($) | Optimal Control Selection | Initial Cost ($) | Control Effectiveness (%) | Residual ALE ($) | Net Risk Reduction Benefit ($) | Budget Selection Priority |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Database Injection**[cite: 33] | $31,250,000[cite: 33] | Web Application Firewall (WAF)[cite: 33] | $150,000[cite: 33] | 75.0%[cite: 33] | $7,812,500 | $23,437,500 | **Rank 1 (Immediate Must-Fund)** |
| **Session Hijacking**[cite: 33] | $3,000,000[cite: 33] | MFA Enhancement[cite: 33] | $200,000[cite: 33] | 95.0%[cite: 33] | $150,000 | $2,850,000 | **Rank 2 (High-Impact ROI)** |
| **API Auth Bypass**[cite: 33] | $750,000[cite: 33] | API Security Gateway[cite: 33] | $350,000[cite: 33] | 90.0%[cite: 33] | $75,000 | $675,000 | **Rank 3 (Strategic Capital Allocation)** |
| **TOTALS** | **$35,000,000** | **Full Defense Portfolio** | **$700,000** | **77.04% (Avg)**| **$8,037,500** | **$26,962,500** | **Recommended Budget Envelope: $700,000** |

### Strategic Budget Constraint Decision Rules:
1. **Under a $200,000 Micro-Budget Constraint:** Deploy **WAF ($150,000)** first. This single control captures **86.9%** of all achievable risk reduction ($23.44M saved)[cite: 33].
2. **Under a $350,000 Mid-Tier Budget Constraint:** Combine **WAF ($150,000)** and **MFA ($200,000)** to eliminate **97.5%** of preventable risk ($26.29M saved)[cite: 33].
3. **At Full Allocation ($700,000 Budget):** Deploy all three controls to achieve complete continuous compliance alignment and maximum security posture resilience[cite: 33].


---


Task 5: Control Selection Analysis
1. Cost vs. Effectiveness Comparison (Scatter Plot Mapping)
EFFECTIVENESS (%)
100% |                                    [MFA Enhancement] (95%, $200k)
 90% |                                                                      [API Gateway] (90%, $350k)
 80% |                  [WAF] (75%, $150k)
 70% |
     +----------------------------------------------------------------------------------------------
     $0                $100k             $200k              $300k             $400k
                                         INITIAL COST ($)

---


2. Return on Investment (ROI) Comparison (Horizontal Bar Chart)
Control Option ROI Performance (%)
===================================================================================
WAF Implementation    | [##################################################] 15,525.00%
MFA Enhancement       | [#####] 1,325.00%
API Security Gateway  | [#] 92.86%
===================================================================================

---

3. Risk Reduction Over Time (Line Graph Trend)
Enterprise Exposure Trajectory (ALE in Millions USD over 12 Months)
===================================================================================
Month 0 (Baseline)  : [########################################] $35.00M
Month 1 (WAF Live)  : [#############] $11.56M
Month 3 (MFA Live)  : [####] $8.71M
Month 6 (API Live)  : [###] $8.04M (Residual Exposure)
Month 12 (Steady)   : [###] $8.04M
===================================================================================


---


Phase 3: Executive Reporting
Task 6: Executive Dashboard & Summary

===================================================================================
                      SECUREBANK FINANCIAL - EXECUTIVE DASHBOARD                    
===================================================================================
TARGET SYSTEM: SecureMobile Platform (500,000 Active Accounts)[cite: 33]
PREPARED BY: Lead GRC Risk Analyst (Confidence Chinwuko)[cite: 33]
-----------------------------------------------------------------------------------

1. TOP 3 QUANTIFIED RISKS
• Database Injection (Critical): SLE = $125.00M | ARO = 0.25 | ALE = $31.25M[cite: 33]
• Session Hijacking (High)     : SLE = $7.50M   | ARO = 0.40 | ALE = $3.00M[cite: 33]
• API Auth Bypass (Medium-High): SLE = $5.00M   | ARO = 0.15 | ALE = $0.75M[cite: 33]
TOTAL CURRENT ENTERPRISE EXPOSURE (ALE): $35.00 Million / Year[cite: 33]

2. PROPOSED CONTROL INVESTMENT PORTFOLIO
• Web Application Firewall (WAF) : Initial $150,000 | Maint. $25,000/yr[cite: 33]
• Multi-Factor Auth Enhancement : Initial $200,000 | Maint. $30,000/yr[cite: 33]
• API Security Gateway          : Initial $350,000 | Maint. $50,000/yr[cite: 33]
TOTAL CAPITAL INVESTMENT REQUIRED: $700,000 (Year 1) | $105,000 (Annual Recurrent)[cite: 33]

3. FINANCIAL IMPACT & RETURN ON INVESTMENT
• Gross Annual Risk Reduction : $26,962,500
• Post-Control Residual Risk   : $8,037,500 (77.04% Risk Elimination)
• Portfolio Net ROI (Year 1)   : 3,751.79%
• Combined Payback Horizon    : 0.31 Months (~9.3 Days)
===================================================================================

---

Executive Dashboard Visuals:
A. Risk Exposure Before vs. After Controls (Double Bar Chart)
Financial Risk Exposure Comparison (ALE in Millions USD)
===================================================================================
Database Injection  | Before: [##############################] $31.25M
                    | After : [########] $7.81M
-----------------------------------------------------------------------------------
Session Hijacking   | Before: [###] $3.00M
                    | After : [#] $0.15M
-----------------------------------------------------------------------------------
API Auth Bypass     | Before: [#] $0.75M
                    | After : [#] $0.08M
===================================================================================

---

B. Capital Investment Breakdown (Stacked Bar Chart)
Year 1 Portfolio Allocation ($700,000 Total Capital)
===================================================================================
[API Security Gateway: $350k (50%)] [MFA Enhancement: $200k (28.6%)] [WAF: $150k (21.4%)]
===================================================================================


---


Task 7: Risk Treatment Plan & Timeline (Gantt Chart)
SECUREMOBILE RISK REMEDIATION ROADMAP (GANTT CHART)
===================================================================================
Phase / Task                 | Days 1-30 | Days 31-90 | Days 91-365 | Owner
-----------------------------+-----------+------------+-------------+--------------
Phase 1: Immediate Actions   |           |            |             |
• Emergency WAF Deployment   | [=======] |            |             | SecOps / Network
• DB Input Sanitization      | [=======] |            |             | AppDev
• Virtual Patching           | [=======] |            |             | CISO Team
-----------------------------+-----------+------------+-------------+--------------
Phase 2: Short-Term Controls |           |            |             |
• MFA Protocol Upgrade       |           | [========] |             | Identity Team
• Session Token Hardening    |           | [========] |             | AppDev
• SecOps Monitoring Integration|          | [========] |             | SOC Manager
-----------------------------+-----------+------------+-------------+--------------
Phase 3: Long-Term Strategy  |           |            |             |
• API Gateway Architecture   |           |            | [=========] | Enterprise Arch
• Penetration Retesting      |           |            | [=========] | GRC / Audit
• Continuous Governance      |           |            | [=========] | GRC Lead
===================================================================================


---


## Section 4: Strategic Risk-Control Optimization Portfolio

The matrix below optimizes control selection based on capital budget allocations, displaying current exposure versus residual risk posture[cite: 1]:

| Vulnerability Target | Current ALE ($) | Optimal Control Selection | Initial Cost ($) | Control Effectiveness (%) | Residual ALE ($) | Net Risk Reduction Benefit ($) | Budget Selection Priority |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Database Injection**[cite: 1] | $31,250,000[cite: 1] | Web Application Firewall (WAF)[cite: 1] | $150,000[cite: 1] | 75.0%[cite: 1] | $7,812,500 | $23,437,500 | **Rank 1 (Immediate Must-Fund)** |
| **Session Hijacking**[cite: 1] | $3,000,000[cite: 1] | MFA Enhancement[cite: 1] | $200,000[cite: 1] | 95.0%[cite: 1] | $150,000 | $2,850,000 | **Rank 2 (High-Impact ROI)** |
| **API Auth Bypass**[cite: 1] | $750,000[cite: 1] | API Security Gateway[cite: 1] | $350,000[cite: 1] | 90.0%[cite: 1] | $75,000 | $675,000 | **Rank 3 (Strategic Capital Allocation)** |
| **TOTALS** | **$35,000,000** | **Full Defense Portfolio** | **$700,000** | **77.04% (Avg)**| **$8,037,500** | **$26,962,500** | **Recommended Budget Envelope: $700,000**[cite: 1] |

### Strategic Budget Constraint Decision Rules:
1. **Under a $200,000 Micro-Budget Constraint:** Deploy **WAF ($150,000)** first. This single control captures **86.9%** of all achievable risk reduction ($23.44M saved)[cite: 1].
2. **Under a $350,000 Mid-Tier Budget Constraint:** Combine **WAF ($150,000)** and **MFA ($200,000)** to eliminate **97.5%** of preventable risk ($26.29M saved)[cite: 1].
3. **At Full Allocation ($700,000 Budget):** Deploy all three controls to achieve complete continuous compliance alignment and maximum security posture resilience[cite: 1].
