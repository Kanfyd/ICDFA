# Lab 3A: Phishing Simulation Metrics and Quantitative Risk Analysis

**Student Name:** Confidence Chinwuko  
**Registration Number:** C11-26-CGRCE-17558  
**Course Code:** GRC103 – Risk Analysis and Evaluation  
**Institution:** International Cybersecurity and Digital Forensics Academy (ICDFA)  
**Organization:** GlobalTech Inc.  
**Role:** Lead GRC Risk Analyst  

---

## Executive Summary

This report delivers a quantitative risk analysis of GlobalTech Inc.'s human risk posture, using empirical data collected from three phishing simulation campaigns conducted in Q3. By converting raw user interaction rates (opens, clicks, credential submissions) into financial risk metrics—specifically Annualized Loss Expectancy (ALE) and Return on Investment (ROI)—this analysis outlines the monetary justification for implementing Multi-Factor Authentication (MFA) and expanded security awareness controls.

---

## PHASE 1: Basic Metric Calculations

### Step 1: Fundamental Rates

The core interaction rates for each campaign are calculated using the formula:
$$\text{Rate} = \left(\frac{\text{Number of Events}}{\text{Number of Emails Sent}}\right) \times 100$$

#### Detailed Working:
* **Campaign A ("HR Bonus Notification" - 100 Sent):**
  * Email Open Rate: $(82 / 100) \times 100 = 82.0\%$
  * Click-Through Rate (CTR): $(47 / 100) \times 100 = 47.0\%$
  * Credential Submission Rate: $(18 / 100) \times 100 = 18.0\%$
  * Data Entry Rate: $(5 / 100) \times 100 = 5.0\%$

* **Campaign B ("IT System Password Reset" - 250 Sent):**
  * Email Open Rate: $(200 / 250) \times 100 = 80.0\%$
  * Click-Through Rate (CTR): $(150 / 250) \times 100 = 60.0\%$
  * Credential Submission Rate: $(75 / 250) \times 100 = 30.0\%$
  * Data Entry Rate: $(25 / 250) \times 100 = 10.0\%$

* **Campaign C ("CEO Urgent Document Review" - 80 Sent):**
  * Email Open Rate: $(72 / 80) \times 100 = 90.0\%$
  * Click-Through Rate (CTR): $(60 / 80) \times 100 = 75.0\%$
  * Credential Submission Rate: $(12 / 80) \times 100 = 15.0\%$
  * Data Entry Rate: $(8 / 80) \times 100 = 10.0\%$

#### Completed Fundamental Rates Table:

| Campaign | Email Open Rate | Click-Through Rate | Credential Submission Rate | Data Entry Rate |
| :--- | :--- | :--- | :--- | :--- |
| **A** | 82.0% | 47.0% | 18.0% | 5.0% |
| **B** | 80.0% | 60.0% | 30.0% | 10.0% |
| **C** | 90.0% | 75.0% | 15.0% | 10.0% |

---

### Step 2: Calculate Efficiency Metrics

Efficiency metrics measure user susceptibility at each subsequent stage of an attack chain.

#### 1. Conversion Rate from Open to Click:
$$\text{Open-to-Click Conversion} = \left(\frac{\text{Clicked}}{\text{Opened}}\right) \times 100$$
* **Campaign A:** $(47 / 82) \times 100 = 57.3\%$
* **Campaign B:** $(150 / 200) \times 100 = 75.0\%$
* **Campaign C:** $(60 / 72) \times 100 = 83.3\%$

#### 2. Post-Click Credential Submission Rate:
$$\text{Post-Click Submission Rate} = \left(\frac{\text{Credentials Submitted}}{\text{Clicked}}\right) \times 100$$
* **Campaign A:** $(18 / 47) \times 100 = 38.3\%$
* **Campaign B:** $(75 / 150) \times 100 = 50.0\%$
* **Campaign C:** $(12 / 60) \times 100 = 20.0\%$

---

## PHASE 2: Advanced Risk Quantification

### Step 3: Calculate Organizational Risk Exposure

To estimate full organizational risk, simulation findings are projected across GlobalTech’s total workforce of 2,000 employees based on Campaign B (the most effective technical vector).

#### Calculations:
* **Total Employee Base:** 2,000 employees
* **Campaign B Credential Rate:** 30.0%
* **Projected Compromised Accounts:** 
  $$2,000 \times 0.30 = 600 \text{ employees}$$
* **Probability of Data Breach given Stolen Credentials:** 25.0%
* **Expected Annual Data Breaches:** 
  $$600 \times 0.25 = 150 \text{ breach incidents}$$

---

### Step 4: Financial Impact Analysis

#### A. Total Financial Exposure:
Using the industry average cost per data breach of $4,350,000:
$$\text{Total Financial Exposure} = 150 \text{ breaches} \times \$4,350,000 = \$652,500,000$$

#### B. Annualized Loss Expectancy (ALE):
$$\text{ALE} = \text{Single Loss Expectancy (SLE)} \times \text{Annual Rate of Occurrence (ARO)}$$
* **Single Loss Expectancy (SLE):** $4,350,000
* **Annual Rate of Occurrence (ARO):** 150
$$\text{ALE} = \$4,350,000 \times 150 = \$652,500,000$$

---

### Step 5: Control Effectiveness & Cost-Benefit Analysis

#### Option 1: Multi-Factor Authentication (MFA) Implementation
* **Implementation Cost:** $45/user \times 2,000 \text{ users} = \$90,000$
* **Control Effectiveness:** 99.9% risk reduction
* **Gross Risk Reduction Benefit:** 
  $$\$652,500,000 \times 0.999 = \$651,847,500$$
* **Net Benefit:** 
  $$\$651,847,500 - \$90,000 = \$651,757,500$$
* **Return on Investment (ROI):**
  $$\text{ROI} = \left(\frac{\$651,847,500 - \$90,000}{\$90,000}\right) \times 100 = 724,175\%$$

#### Option 2: Security Awareness Training
* **Implementation Cost:** $50/user \times 2,000 \text{ users} = \$100,000$
* **Control Effectiveness:** 60.0% reduction in click rates
* **New Click-Through Rate:** $30\% \times (1 - 0.60) = 12.0\%$
* **New Projected Compromised Credentials:** $2,000 \times 0.12 = 240 \text{ accounts}$
* **New Expected Breaches:** $240 \times 0.25 = 60 \text{ breaches}$
* **New ALE:** $60 \times \$4,350,000 = \$261,000,000$
* **Gross Risk Reduction Benefit:** 
  $$\$652,500,000 - \$261,000,000 = \$391,500,000$$
* **Net Benefit:** 
  $$\$391,500,000 - \$100,000 = \$391,400,000$$
* **Return on Investment (ROI):**
  $$\text{ROI} = \left(\frac{\$391,500,000 - \$100,000}{\$100,000}\right) \times 100 = 391,400\%$$

---

## PHASE 3: Comprehensive Risk Assessment

### Step 6: Complete Risk Assessment Matrix

#### Exposure Derivations for Matrix:
* **Campaign A Exposure:** 
  $$2,000 \times (18/100) \times 0.25 \times \$4,350,000 = 360 \times 0.25 \times \$4,350,000 = \$156,600,000$$
* **Campaign B Exposure:** 
  $$2,000 \times (75/250) \times 0.25 \times \$4,350,000 = 600 \times 0.25 \times \$4,350,000 = \$652,500,000$$
* **Campaign C Exposure:** 
  $$2,000 \times (12/80) \times 0.25 \times \$4,350,000 = 300 \times 0.25 \times \$4,350,000 = \$104,400,000$$

#### Risk Assessment Matrix:

| Campaign | Overall Risk Score | Financial Exposure | Priority Level | Recommended Action |
| :--- | :--- | :--- | :--- | :--- |
| **A** | MEDIUM-HIGH | $156,600,000 | 2 | Enhanced Training |
| **B** | CRITICAL | $652,500,000 | 1 | IMMEDIATE MFA |
| **C** | HIGH | $104,400,000 | 2 | Executive Training |

---

### Step 7: Statistical Significance Analysis

To evaluate whether the sample results represent the entire organization, we calculate the 95% Confidence Interval for **Campaign A**.

#### Given Parameters:
* Sample size ($n$): 100
* Proportion ($p$): 0.18 (18.0%)
* Critical Value ($z$ for 95% Confidence): 1.96

#### Standard Error (SE) Calculation:
$$\text{SE} = \sqrt{\frac{p(1 - p)}{n}} = \sqrt{\frac{0.18 \times (1 - 0.18)}{100}} = \sqrt{\frac{0.18 \times 0.82}{100}} = \sqrt{\frac{0.1476}{100}} = \sqrt{0.001476} \approx 0.03842$$

#### Margin of Error (MoE) Calculation:
$$\text{MoE} = z \times \text{SE} = 1.96 \times 0.03842 \approx 0.0753 \text{ (or } 7.53\%)$$

#### Confidence Interval Range:
$$\text{True Rate Range} = p \pm \text{MoE} = 0.18 \pm 0.0753$$
$$\text{Lower Bound} = 0.18 - 0.0753 = 0.1047 \text{ (10.47\%)}$$
$$\text{Upper Bound} = 0.18 + 0.0753 = 0.2553 \text{ (25.53\%)}$$

**Statistical Interpretation:** We are 95% confident that the true credential submission rate for the entire enterprise under HR-themed lures lies between **10.47% and 25.53%**.

---

## PHASE 4: Executive Reporting

### Executive Briefing Memorandum

**TO:** Board of Directors, Chief Information Security Officer (CISO), Chief Financial Officer (CFO)  
**FROM:** GRC Risk Analysis Team  
**DATE:** November 1, 2026  
**SUBJECT:** CRITICAL: Quantitative Phishing Risk Assessment & $652M Exposure  

#### 1. Executive Summary
Our Q3 phishing simulations demonstrate an unmitigated enterprise loss exposure of **$652.5 million annually**. The "IT Password Reset" scenario revealed a 30% credential theft rate, indicating that up to 600 user accounts are vulnerable to compromise without technical intervention. Deploying MFA and targeted training will mitigate over 90% of this exposure.

#### 2. Key Quantitative Findings

| Risk Metric | Value | Industry Average | Severity |
| :--- | :--- | :--- | :--- |
| Overall Credential Theft Rate | 22.1% | 15.3% | HIGH |
| Maximum Campaign Success Rate | 30.0% | 18.7% | CRITICAL |
| Annualized Loss Expectancy | $652.5M | $285.0M | SEVERE |
| MFA Implementation ROI | 724,175% | 350.0% | EXCELLENT |

#### 3. Detailed Financial Analysis & Investment Portfolio

* **Current State ALE:** $652,500,000
* **Projected Compromised Accounts:** 600
* **Expected Annual Incidents:** 150 breaches
* **Per-Employee Risk Exposure:** $326,250

##### Proposed Security Investment Portfolio:

| Control | Cost | Risk Reduction | Net Benefit | ROI | Priority |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **MFA Implementation** | $90,000 | $651.8M | $651.7M | 724,175% | 1 |
| **Enhanced Training** | $100,000 | $391.5M | $391.4M | 391,400% | 2 |
| **Email Filtering** | $50,000 | $130.5M | $130.4M | 260,800% | 3 |

#### 4. Strategic Action Plan

##### Immediate Actions (Q1)
1. Enforce mandatory, hardware-backed or authenticator-app Multi-Factor Authentication across all 2,000 user endpoints ($90,000 investment).
2. Deploy emergency role-based security training focused on IT service desk and credential reset impersonation lures ($100,000 investment).
3. Introduce automated credential-leak detection and inline banner warnings on external communications ($25,000 investment).

##### Strategic Initiatives (FY2024–FY2025)
1. Upgrade email filtering controls to analyze dynamic payloads and suspicious domain lookalikes ($50,000 investment).
2. Integrate User and Entity Behavior Analytics (UEBA) within the SIEM environment to catch abnormal account logins ($75,000 investment).
3. Conduct quarterly targeted simulations across C-suite and executive assistant pathways ($150,000 investment).

#### 5. Post-Control Risk Posture

| Metric | Current Baseline | Post-Control State | Absolute Reduction |
| :--- | :--- | :--- | :--- |
| Credential Theft Rate | 22.1% | 2.2% | 90.0% |
| Annual Loss Expectancy | $652.5M | $65.25M | 90.0% |
| Breach Probability / Rate | 150 Breaches | 15 Breaches | 90.0% |

* **Total Security Investment Required:** $490,000
* **Total Gross Risk Reduction:** $587,250,000
* **Net Financial Benefit:** $586,760,000

---

## BONUS CHALLENGE: Break-Even Point Analysis

To determine how many data breaches must be prevented to offset the full security portfolio cost of $490,000:

$$\text{Break-Even Point} = \frac{\text{Total Security Investment Cost}}{\text{Single Loss Expectancy (Cost per Breach)}}$$

$$\text{Break-Even Point} = \frac{\$490,000}{\$4,350,000} \approx 0.1126 \text{ breaches}$$

### Conclusion:
Preventing just **1 single data breach** (which saves $4,350,000) covers the full $490,000 control suite almost **9 times over**, producing an immediate net saving of $3,860,000 in avoided loss.
