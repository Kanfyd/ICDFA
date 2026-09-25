# TechGlobal Information Security Governance Transformation Report
**Course:** GRC102 – Information Security Governance  
**Client:** TechGlobal Inc. Board of Directors & Executive Leadership  
**Author:** Confidence Chinwuko  

---

## Task 1: Governance Architecture and Stakeholder Map

### Task 1 Prompt & Questions
> **Task 1 Requirements (20 marks):**
> 1. Identify at least five weaknesses in the current governance model and explain the business or risk consequence of each.
> 2. Create a stakeholder map showing the interests, authority, information needs and expected contribution of the Board, CEO, CISO, CRO/Risk, Legal, Finance, HR, IT and Business Units.
> 3. Design a Security Governance Organisation Chart showing reporting lines, oversight relationships and communication paths.
> 4. Explain why the proposed structure is appropriate for a 2,500-employee technology organisation operating across five offices.

---

### 1.1 Governance Gap Assessment

| # | Current Governance Weakness | Business / Risk Consequence |
|---|---|---|
| **1** | **IT-Centric Decision Concentration:** Security is treated as an IT sub-function under the IT Director rather than an enterprise risk domain. | Creates an immediate conflict of interest between operational delivery and risk control. IT prioritizes system uptime and project delivery over security controls, accumulating unmitigated technical debt. |
| **2** | **Absence of Executive Governance Committees:** No formal cross-functional forums exist to review risk, policy, or security investments. | Leads to fragmented decision-making where regional business unit leaders make localized security trade-offs without understanding cross-organizational threat implications or regulatory exposure. |
| **3** | **Blind Board Oversight:** The CEO and Board receive informal, ad-hoc security updates lacking standardized key risk indicators (KRIs). | Causes fiduciary non-compliance with global governance standards (e.g., ISO/IEC 27014), leaving executive directors unable to evaluate organizational risk against approved risk appetite. |
| **4** | **Informal Risk Acceptance:** Security risks are accepted informally by the IT Director or regional teams without legal, financial, or risk management sign-off. | Exposes TechGlobal to unmonitored cyber liabilities and severe regulatory penalties (e.g., GDPR, NDPA) due to unauthorized risk acceptance exceeding enterprise thresholds. |
| **5** | **Undefined Escalation Pathways:** Operational security incidents and vulnerabilities lack clear metrics and paths for escalation to executive management. | Results in delayed incident containment and late regulatory breach disclosures, compounding financial losses and causing reputational damage. |

---

### 1.2 Stakeholder Map

| Stakeholder | Authority / Influence | Primary Interest | Information Needed | Governance Contribution |
|---|---|---|---|---|
| **Board of Directors** | High Authority / High Influence | Fiduciary oversight, enterprise resilience, brand protection, regulatory compliance. | Quarterly risk scorecards, material incident briefs, compliance audit reports. | Sets enterprise risk appetite, approves security strategy, oversees executive leadership. |
| **CEO** | High Authority / High Influence | Strategic growth, operational continuity, business performance, shareholder value. | Material risk dashboard, security investment ROI, critical incident alerts. | Holds ultimate executive accountability, aligns security vision with business goals. |
| **CISO** | Medium Authority / High Influence | Threat reduction, security strategy, policy enforcement, incident readiness. | Threat intelligence, control efficacy metrics, vulnerability logs, incident data. | Drives security program execution, designs controls, advises executive management. |
| **CRO / Risk** | Medium Authority / High Influence | Enterprise risk aggregation, methodology alignment, risk appetite monitoring. | Security risk register, residual risk profiles, risk acceptance documentation. | Integrates cyber risk into Enterprise Risk Management (ERM) framework. |
| **Legal / Compliance** | Medium Authority / Medium Influence | Regulatory duties, contractual liability, privacy governance, breach notification. | Non-compliance reports, statutory changes, regulatory exposure assessments. | Oversees breach notifications, reviews vendor contracts, advises on privacy laws. |
| **Finance** | Medium Authority / High Influence | Financial governance, cost-effective controls, budget prioritization, loss mitigation. | Security budget proposals, loss exposure models, ROI on security capital expenditure. | Funds security investments, evaluates financial risk exposure and cyber insurance. |
| **Human Resources** | Medium Authority / Medium Influence | Personnel security, culture, policy adherence, insider threat reduction. | Background check audits, security awareness metrics, policy violation logs. | Governs joiner/mover/leaver access lifecycle, enforces disciplinary policy. |
| **IT / Technology** | Medium Authority / High Influence | Infrastructure uptime, technical delivery, system scalability, control deployment. | Technical security standards, patch schedules, vulnerability scan outputs. | Operates infrastructure, remediates vulnerabilities, deploys technical controls. |
| **Business Unit Leaders** | High Authority / Medium Influence | Regional productivity, product release velocity, client satisfaction. | BU risk profiles, control impact on workflows, policy compliance standards. | Owns operational risk, implements localized controls, enforces compliance. |

---

### 1.3 Security Governance Organisation Chart

```text
                        +---------------------------------+
                        |       BOARD OF DIRECTORS        |
                        |   (Audit & Risk Committee)      |
                        +---------------------------------+
                                         |
                                         | Fiduciary Oversight & Escalation
                                         v
                        +---------------------------------+
                        |     CHIEF EXECUTIVE OFFICER     |
                        +---------------------------------+
                                         |
               +-------------------------+-------------------------+
               |                                                   |
               v                                                   v
   +-----------------------+                           +-----------------------+
   | EXECUTIVE SECURITY    |                           | SECURITY GOVERNANCE   |
   | COUNCIL (ESC)         |                           | COMMITTEE (SGC)       |
   +-----------------------+                           +-----------------------+
               |                                                   |
               +-------------------------+-------------------------+
                                         |
                                         v
                        +---------------------------------+
                        |  CHIEF INFORMATION SECURITY     |
                        |          OFFICER (CISO)         |
                        +---------------------------------+
                                         |
         +-------------------------------+-------------------------------+
         |                               |                               |
         v                               v                               v
+-----------------+             +-----------------+             +-----------------+
| Security Ops &  |             |  GRC & Vendor   |             | Security Arch.  |
|  Engineering    |             | Risk Governance |             |  & Compliance   |
+-----------------+             +-----------------+             +-----------------+
         |                               |                               |
         +-------------------------------+-------------------------------+
                                         |
                                         v
                         Direct Collaboration & Oversight
         +-------------------------------+-------------------------------+
         |                               |                               |
         v                               v                               v
+-----------------+             +-----------------+             +-----------------+
|   IT Director   |             | Legal, HR, Fin. |             | Business Unit   |
| (Infrastructure)|             |  (Cross-Func.)  |             |  Leaders (x5)   |
+-----------------+             +-----------------+             +-----------------+

1.4 Consultant Architecture Justification
The redesigned governance architecture adopts a Three Lines Model structured specifically for TechGlobal’s operating scale (2,500 employees across five global offices):

Independence of Security Oversight: The CISO reports functionally to the Board Audit & Risk Committee / Executive Security Council and administratively to the CEO or CRO. This decouples security governance from the IT Director, removing the conflict between speed of IT delivery and security control enforcement.

Cross-Functional Governance Alignment: The establishment of the Security Governance Committee (SGC) ensures key functions—Legal, Finance, HR, IT, and Business Units—participate directly in security oversight. Security decisions are evaluated against operational and financial impacts rather than made in technical isolation.

Scalable International Governance: Business Unit Leaders across TechGlobal's five offices act as localized risk owners, executing central policies while escalating regional risks to the SGC. This maintains global control consistency while accommodating regional regulatory requirements (e.g., GDPR in Europe, NDPA in Nigeria).

---

Task 2: Governance Responsibility Matrix, Role Profiles, and Conflict Resolution
Task 2 Prompt & Questions
Task 2 Requirements (20 marks):

Develop a responsibility profile for the Board, CEO, CISO, CRO/Risk, Legal, Finance, HR and IT.

For each role, define purpose, key governance responsibilities, decision authority, reporting obligations and at least two performance indicators.

Identify at least three areas where authority could overlap or conflict and explain how the governance model should resolve those conflicts.

### 2.1 Governance Responsibility Matrix

| Governance Activity | Board | CEO | CISO | CRO | Legal | Finance | HR | IT | BU Leaders |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **Set Security Strategy & Risk Appetite** | **A** | C | R | C | C | C | I | I | C |
| **Approve Enterprise Security Policies** | I | **A** | R | C | C | I | C | C | C |
| **Perform Cyber Risk Assessments** | I | I | **A** | C | I | I | I | C | R |
| **Accept Residual Risk (Material > $500k)** | **A** | C | C | C | C | I | I | I | I |
| **Accept Residual Risk (Operational < $500k)** | I | I | C | **A** | I | I | I | C | R |
| **Approve Cybersecurity Budget** | C | **A** | R | I | I | C | I | I | C |
| **Incident Response Execution** | I | I | **A** | I | C | I | C | R | C |
| **Regulatory Breach Notification Decision** | I | C | C | I | **A** | I | I | I | I |
| **Remediate Technical Vulnerabilities** | I | I | C | I | I | I | I | **A/R** | C |

*RACI Legend: **A** = Accountable; **R** = Responsible; **C** = Consulted; **I** = Informed.*

2.2 Core Role Profiles
1. Board of Directors
Purpose: Provides fiduciary oversight and ensures cybersecurity aligns with business goals and legal requirements.

Key Responsibilities: Approves risk appetite; oversees CISO performance; reviews material cyber risks quarterly.

Decision Authority: Final approval of enterprise risk appetite; accepts material risks exceeding $500,000.

Reporting Obligations: Receives quarterly CISO board risk reports and immediate briefs on Level 3 incidents.

KPIs: 100% attendance at scheduled risk reviews; zero unapproved material risk exposures.

2. Chief Executive Officer (CEO)
Purpose: Holds executive accountability for strategic execution, organizational culture, and business resilience.

Key Responsibilities: Promotes security culture; aligns security funding with business growth; approves top-level policies.

Decision Authority: Approves security strategy and annual security operating budget.

Reporting Obligations: Reports to the Board; receives bi-weekly executive briefings from the CISO.

KPIs: Executive incident simulation completion; security strategy alignment score > 90%.

3. Chief Information Security Officer (CISO)
Purpose: Leads security strategy, policy enforcement, threat management, and risk governance.

Key Responsibilities: Defines security architecture; manages SOC and incident response; reports enterprise cyber risk.

Decision Authority: Defines technical security standards; enforces emergency isolation of compromised assets.

Reporting Obligations: Reports functionally to the Board and administratively to CEO/CRO; delivers monthly SGC reports.

KPIs: Mean Time to Detect (MTTD) < 2 hours; Mean Time to Respond (MTTR) < 4 hours.

4. Chief Risk Officer (CRO)
Purpose: Integrates cyber risk into the enterprise risk framework.

Key Responsibilities: Establishes risk assessment standards; maintains the Enterprise Risk Register; reviews risk acceptances.

Decision Authority: Approves operational risk acceptance requests between $100,000 and $500,000.

Reporting Obligations: Reports to CEO and Board Risk Committee; receives monthly risk updates from CISO.

KPIs: 100% of high/critical cyber risks integrated into ERM; quarterly risk assessment completion rate.

5. Legal & Compliance Counsel
Purpose: Manages legal liability, privacy compliance, and regulatory obligations.

Key Responsibilities: Approves regulatory disclosures; advises on contract terms; manages breach notifications.

Decision Authority: Sole authority to approve breach notifications to regulatory authorities and data subjects.

Reporting Obligations: Reports to CEO; receives immediate notification of data-exposure events.

KPIs: Zero regulatory penalties due to late notification; 100% contract compliance with privacy standards.

6. Finance (CFO)
Purpose: Manages financial control, budget allocation, and loss exposure for cyber risk.

Key Responsibilities: Allocates security funding; manages cyber insurance coverage; models financial loss exposure.

Decision Authority: Approves security capital expenditures (CapEx) and operational budget releases.

Reporting Obligations: Reports to CEO; receives quarterly loss exposure reports from CISO.

KPIs: Cyber insurance coverage aligned with maximum tolerable loss; 100% tracking of security spend vs budget.

7. Human Resources (HR)
Purpose: Governs personnel security, insider threat controls, and security awareness culture.

Key Responsibilities: Enforces Joiner/Mover/Leaver access revocation; mandates security training; manages disciplinary actions.

Decision Authority: Approves disciplinary sanctions for security policy non-compliance.

Reporting Obligations: Reports to CEO; delivers monthly security awareness metrics to SGC.

KPIs: User access revocation completed within 24 hours > 98%; security training completion > 95%.

8. IT Director / Infrastructure
Purpose: Maintains IT infrastructure operations while deploying technical controls mandated by the CISO.

Key Responsibilities: System patching; infrastructure resilience; identity execution; system backup operations.

Decision Authority: Approves technical maintenance windows and system change implementation plans.

Reporting Obligations: Reports to COO/CEO; delivers weekly patching compliance reports to CISO.

KPIs: Critical patch SLA compliance within 14 days > 95%; infrastructure availability > 99.9%.

2.3 Overlapping Authority & Conflict Resolution Note
IT Velocity vs. Security Gating (IT Director vs. CISO):

Conflict: IT prioritizes rapid system deployment; CISO requires security testing, causing project delays.

Resolution: The SGC mandates a formal Security Architecture Gate. Exceptions require a signed Risk Acceptance Form approved by the CRO and BU Leader; IT cannot bypass security controls unilaterally.

Business Risk Acceptance vs. Regulatory Mandates (BU Leaders vs. Legal):

Conflict: A BU Leader accepts the risk of using an unvetted vendor to meet revenue targets, violating privacy laws.

Resolution: Legal Counsel holds absolute veto authority over any risk acceptance proposal that violates statutory requirements (e.g., GDPR, NDPA).

Emergency Incident Containment vs. Business Uptime (CISO vs. BU Leaders):

Conflict: CISO wants to take an active database offline during ransomware activity; the BU Leader resists due to active customer transactions.

Resolution: CISO holds immediate decision authority to isolate systems during a Level 3 (Critical) security incident, delivering written post-action justification to the CEO within 4 hours.


---


Task 3: Committee Ecosystem, Terms of Reference, Agenda, Decision Log, and Governance Calendar
Task 3 Prompt & Questions
Task 3 Requirements (20 marks):

Design an Executive Security Council for strategic oversight.

Design a Security Governance / Steering Committee for cross-functional governance decisions.

Define one specialised Working Group appropriate to TechGlobal.

Define how Business Units will participate in governance without creating separate security silos.

Show how decisions and risk information move from operational forums to executive management and the Board.

3.1 Committee Ecosystem Diagram
[ BOARD OF DIRECTORS / AUDIT & RISK COMMITTEE ]
                     ^
                     | Quarterly Risk Reporting & Material Escalation
                     |
  [ EXECUTIVE SECURITY COUNCIL (ESC) ]  <--- Strategy & Risk Appetite
  Members: CEO, CISO, CRO, Legal, CFO
                     ^
                     | Monthly Escalation & Policy Endorsement
                     |
  [ SECURITY GOVERNANCE COMMITTEE (SGC) ]  <--- Cross-Functional Governance
  Members: CISO (Chair), IT Dir, Legal, HR, Risk, Finance, BU Leaders
                     ^
                     | Fortnightly Vulnerability & Operational Reports
                     |
  [ CLOUD & OPERATIONAL WORKING GROUP ]  <--- Specialized Technical Forum
  Members: Security Architect, DevOps Lead, IT Ops, Cloud Lead

3.2 Terms of Reference (ToR) — Security Governance Committee (SGC)
Purpose: Provides cross-functional leadership and governance for TechGlobal’s security program, ensuring alignment with business objectives and regulatory standards.

Membership: CISO (Chair), IT Director, CRO, Legal Counsel, HR Director, Finance Manager, Representative BU Leaders (x2).

Quorum: Minimum 5 members, requiring the mandatory presence of CISO, IT Director, and Legal (or official delegates).

Meeting Cadence: Monthly (3rd Thursday of every month) for 90 minutes.

Inputs: Monthly Patch & Vulnerability Reports, Risk Register Updates, Incident Summaries, Audit Findings, Policy Change Requests.

Outputs: Approved Policies, Signed Risk Acceptance Forms, Escalated Proposals to ESC, SGC Decision Logs and Action Trackers.

3.3 Sample Committee Agenda and Decision Log
Sample SGC Meeting Agenda (90 Minutes)
Standing Items (15 mins): Action log review; Monthly Threat & Incident Summary (CISO).

Operational Performance (20 mins): Patch Management SLA compliance & Identity Management metrics (IT Director).

Risk & Policy Review (30 mins): Review of updated Third-Party Risk Policy; Evaluation of unresolved High Risk #2026-08 (Cloud Misconfiguration).

Strategic Initiatives (15 mins): Status update on ISO 27001 implementation across regional offices.

Escalations (10 mins): Identification of items requiring escalation to the Executive Security Council.
Sample Decision Log
| Date | Decision / Issue | Decision Owner | Decision | Rationale | Actions / Owner | Review Date |
| :--- | :--- | :--- | :---: | :--- | :--- | :--- |
| **20/09/2026** | Mandate MFA rollout across all global endpoints. | SGC / CISO | **Approved** | Mitigate credential theft and phishing attacks across remote offices. | IT Director to enforce MFA policy by Oct 15. | 20/10/2026 |
| **20/09/2026** | Vendor risk acceptance request for unencrypted legacy analytics tool. | CRO & BU Lead | **Rejected** | Violates data encryption standards; regulatory risk deemed unacceptable. | BU Lead to migrate to approved encrypted SaaS platform. | 15/11/2026 |
| **20/09/2026** | Budget allocation ($150k) for SOC expansion. | CFO / CISO | **Approved** | Address insider threat and cloud monitoring gaps identified in Q3 risk review. | CISO to initiate procurement. | 01/12/2026 |

3.4 12-Month Governance Calendar
| Month | Recurring Governance Activities & Key Milestones |
| :--- | :--- |
| **Jan** | Annual Security Strategy & Budget Approval (ESC) |
| **Feb** | ISO 27001 Internal Control Audit & Policy Refresh |
| **Mar** | Q1 Board Risk Scorecard Delivery & Third-Party Risk Review |
| **Apr** | Executive Incident Response Simulation / Crisis Management Exercise |
| **May** | Regional Office Compliance & Data Protection Review (GDPR/NDPA) |
| **Jun** | Mid-Year Governance Strategy Review (ESC) & Penetration Testing |
| **Jul** | Annual Employee Security Awareness Training Campaign Launch |
| **Aug** | IT Infrastructure Disaster Recovery & Business Continuity Test |
| **Sep** | Q3 Board Risk Scorecard Delivery & Cyber Insurance Policy Review |
| **Oct** | Enterprise Risk Register Aggregation & Vulnerability Audit |
| **Nov** | Penetration Testing Remediation Review & Identity Governance Audit |
| **Dec** | Annual Risk Appetite Review & Year-End Governance Wrap-Up |

---


Task 4: RACI Matrix and Implementation Guide
Task 4 Prompt & Questions
Task 4 Requirements (20 marks):

Create a RACI matrix covering at least the 15 specified governance activities.

Ensure each activity has one clear Accountable role wherever practicable.

Identify and explain at least three problematic assignments that could create confusion, conflict or weak accountability.

4.1 Completed TechGlobal RACI Matrix
| # | Governance Activity | BD | CEO | CISO | CRO | LGL | FIN | HR | IT | BU |
| :---: | :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **1** | Cybersecurity strategy approval | **A** | C | R | C | C | C | I | C | C |
| **2** | Security policy approval | I | **A** | R | C | C | I | C | C | C |
| **3** | Enterprise cyber-risk assessment | I | I | **A** | C | I | I | I | C | R |
| **4** | Risk acceptance (Material) | **A** | C | C | C | C | I | I | I | I |
| **5** | Security budget approval | C | **A** | R | I | I | C | I | I | C |
| **6** | Security architecture approval | I | I | **A** | I | I | I | I | R | C |
| **7** | Third-party security review | I | I | **A** | C | C | I | I | I | R |
| **8** | Access governance | I | I | C | I | I | I | **A** | R | C |
| **9** | Incident response governance | I | **A** | R | C | C | C | C | C | C |
| **10** | Material incident escalation | I | C | **A** | C | C | I | I | I | I |
| **11** | Regulatory notification decision | I | C | C | I | **A** | I | I | I | I |
| **12** | Security awareness programme | I | I | C | I | C | I | **A** | I | C |
| **13** | Vulnerability remediation oversight | I | I | C | I | I | I | I | **A/R** | C |
| **14** | Business continuity governance | I | C | C | **A** | C | C | C | R | R |
| **15** | Board cyber-risk reporting | **A** | C | R | C | I | I | I | I | I |

*Column Key: **BD** = Board of Directors; **LGL** = Legal & Compliance; **FIN** = Finance; **BU** = Business Unit Leaders.*
4.2 Problematic Assignment Analysis
Dual Accountability for Vulnerability Remediation (Activity 13):

Issue: Assigning IT as both Accountable (A) and Responsible (R) for vulnerability remediation can lead to self-policing. IT may deprioritize patching to maintain operational uptime.

Mitigation: CISO maintains independent oversight and reports unmitigated patch SLA breaches directly to the SGC.

Ambiguity in Access Governance (Activity 8):

Issue: HR is designated Accountable (A) for Joiner/Mover/Leaver identity workflows, while IT is Responsible (R) for technical access provisioning. If HR delays offboarding notifications, IT cannot revoke access.

Mitigation: Implement automated IAM synchronization between HR systems and Active Directory/Okta to revoke access automatically within 24 hours of employee status changes.

Split Authority in Material Incident Escalation vs. Regulatory Notification (Activities 10 & 11):

Issue: CISO is Accountable (A) for material incident escalation, but Legal is Accountable (A) for regulatory notifications. Disagreements between CISO and Legal on whether an incident constitutes a "material breach" can delay statutory disclosures.

Mitigation: The escalation workflow defines objective criteria (e.g., > 1,000 compromised records) that trigger mandatory Legal notification review automatically.

4.3 RACI Implementation Guide for Managers
Single Accountable Rule: Every activity MUST have exactly ONE designated Accountable (A) role. Accountable indicates final ownership and decision authority.

Role-Based Mapping: RACI maps to governance roles, not named individuals. Individuals acting in temporary or dual capacities must follow the RACI designation assigned to the specific function being executed.

Operational Execution: Project Leads must consult the RACI Matrix during initial project scoping to ensure security gates, risk assessments, and approvals are integrated before funding release.


---


Task 5: Escalation Workflow, SoD Register, and Assurance Note
Task 5 Prompt & Questions
Task 5 Requirements (20 marks):
Part 1 (Escalation):

Design a major cyber-risk escalation workflow beginning with operational detection and ending with executive or Board decision.

Define at least three escalation levels and the criteria that trigger each level.

Part 2 (SoD & Assurance):

Identify at least five segregation-of-duties or accountability weaknesses in TechGlobal's current IT-centric model.

Recommend a governance control for each weakness.

Explain how decisions will be recorded, tracked, reviewed and closed for an auditable decision trail.

5.1 Cyber-Risk Escalation Workflow
[ PHASE 1: IDENTIFICATION & TRIAGE ]
   • Security event detected via SOC, vulnerability scanner, or employee report.
   • Security Operations performs triage and impact assessment within 1 hour.
                               |
                               v
[ PHASE 2: THRESHOLD EVALUATION ]
   • Measure event against Escalation Threshold Matrix (Financial exposure, Data sensitivity, System outage).
   • Assign Severity Level: Level 1 (Operational), Level 2 (Executive), or Level 3 (Material).
                               |
            +------------------+------------------+
            |                                     |
            v                                     v
[ LEVEL 1 / LEVEL 2 PATHWAY ]             [ LEVEL 3 MATERIAL RISK PATHWAY ]
   • Level 1: Managed by IT/SOC.             • CISO notifies CEO, Legal, and CRO
   • Level 2: CISO convenes Emergency          within 2 hours.
     SGC panel within 12 hours.              • Emergency Executive Council convened.
   • Remediation plan executed.              • Legal drafts regulatory disclosures.
                                                  |
                                                  v
                                          [ BOARD NOTIFICATION ]
                                             • Board Audit & Risk Chair notified
                                               within 6 hours of confirmation.
                                             • Material Risk Acceptance or
                                               Emergency Budget authorized.

5.2 Escalation Threshold Table
| Level | Impact Criteria / Triggers | Decision Authority | Required Notification | Target Response / SLA |
| :--- | :--- | :--- | :--- | :--- |
| **Level 1: Operational** | Low system impact; financial loss < $50,000; non-sensitive data exposure; isolated malware infection or routine policy breach. | CISO / IT Director | SGC Members (via monthly report) | Initial Triage < 2 hrs; Resolution < 5 days |
| **Level 2: Executive** | Moderate disruption; financial loss $50k – $500k; internal data exposure; non-critical system outage > 4 hrs. | SGC / CRO | CEO, Legal Counsel, Finance | Initial Triage < 30 mins; Convene Panel < 12 hrs |
| **Level 3: Material / Board** | Critical operational outage (> 12 hrs); financial loss > $500,000; PII/PHI breach triggering legal disclosure mandates. | CEO / Board of Directors | Full Board, External Regulators (via Legal) | Immediate Triage; Board Notification < 6 hrs |

5.3 Segregation-of-Duties (SoD) Weakness Register
| ID | Weakness / Conflict | Risk Created | Roles Involved | Recommended Control | Residual Risk / Review |
| :---: | :--- | :--- | :--- | :--- | :--- |
| **1** | IT Director acts as both system operator and security approver. | Unchecked infrastructure changes; security controls bypassed to meet IT release deadlines. | IT Director | Separate IT infrastructure management from CISO risk oversight. Mandate CISO approval for architecture changes. | Low; Reviewed quarterly by SGC. |
| **2** | IT System Administrators conduct their own user privilege audits. | Privilege accumulation; undetected insider threat activity or unauthorized access grants. | IT Admins / System Owners | Implement IAM governance where HR triggers access changes and CISO audits permissions independently. | Low; Reviewed bi-annually by Internal Audit. |
| **3** | IT Director accepts security risks on behalf of regional business units. | Unmonitored financial and legal liabilities accepted without executive visibility or business consent. | IT Director / BU Leaders | Transfer risk acceptance authority exclusively to CRO (operational) and Board/CEO (material). | Low; Monitored via Risk Register. |
| **4** | Security Incident Responder evaluates and signs off on incident closure. | Premature incident closure; root-cause suppression; lack of independent assurance. | Incident Responder / SOC Lead | Require CISO or independent Risk Lead sign-off for closure of Level 2 and Level 3 incidents. | Low; Reviewed after major incidents. |
| **5** | Software Developers hold direct deployment access to production systems. | Unauthorized code deployment; backdoor placement; bypass of security testing gates. | Developers / DevOps | Implement CI/CD pipeline automation with Separation of Environments (Dev/Staging/Prod) and automated deployment gates. | Low; Continuous automated monitoring. |

5.4 Decision-Recording and Assurance Note
To establish an auditable decision trail for regulatory and internal governance requirements:

Centralized GRC Repository: All risk acceptance forms, committee minutes, RACI matrices, and policy exceptions must be stored in a centralized, access-controlled GRC platform.

Standardized Decision Logs: Every decision made by the SGC or Executive Council must be recorded in an immutable log containing:

Unique Decision Reference ID

Timestamp and Decision Owner

Detailed Rationale and Risk Assessment Reference

Mandatory Expiry / Review Date (maximum 12 months for any risk acceptance)

Independent Internal Audit Review: Internal Audit will conduct an annual assurance review of the Decision Log to confirm that all active risk acceptances remain within approved enterprise risk thresholds.


---

Evidence Bundle: Governance Templates & Deliverables
Evidence Bundle 1: Formal Cyber Risk Acceptance Form Template
================================================================================
                       TECHGLOBAL INC. - RISK ACCEPTANCE FORM
================================================================================

SECTION 1: RISK IDENTIFICATION
--------------------------------------------------------------------------------
Risk Reference ID   : RISK-2026-08
Risk Title          : Unencrypted SaaS Legacy Analytics Tool Usage
Risk Description    : The Marketing BU utilizes a legacy cloud analytics tool 
                      that lacks TLS 1.3 data-in-transit encryption.
Asset / System      : Marketing Analytics Database (AWS Hosted)
Risk Category       : Data Protection / Compliance

SECTION 2: RISK ASSESSMENT SUMMARY
--------------------------------------------------------------------------------
Likelihood Rating   : High (3/4)
Impact Rating       : High (3/4)
Inherent Risk Score : HIGH (12/16)
Financial Impact    : Estimated $250,000 (Potential regulatory fine + breach notification)

SECTION 3: MITIGATING CONTROLS & JUSTIFICATION
--------------------------------------------------------------------------------
Compensating Control: Access restricted strictly to IP whitelist; Multi-Factor 
                      Authentication (MFA) mandated; direct database export disabled.
Business Justification: Vendor migration scheduled for Q1 2027. Immediate shutdown 
                        disrupts active global marketing campaigns.

SECTION 4: APPROVAL & SIGN-OFF (Based on Threshold Authority)
--------------------------------------------------------------------------------
Risk Owner (BU)     : _______________________ Date: _______________
CISO Review         : _______________________ Date: _______________
CRO Approval        : _______________________ Date: _______________
Legal Counsel Sign-off: _____________________ Date: _______________

Mandatory Expiry Date : September 20, 2027 (Max 12 Months)
================================================================================

Evidence Bundle 2: Security Governance Committee (SGC) Meeting Minutes Record
================================================================================
               TECHGLOBAL SECURITY GOVERNANCE COMMITTEE (SGC)
                             MEETING MINUTES
================================================================================
Date: September 20, 2026                 Time: 10:00 AM - 11:30 AM WAT
Location: Virtual / Main Boardroom       Chair: CISO (Confidence Chinwuko)

ATTENDEES:
- Confidence Chinwuko (CISO / Chair)
- IT Director (Member)
- Chief Risk Officer (Member)
- Legal Counsel (Member)
- HR Director (Member)
- Lead Security Architect (Guest)

AGENDA ITEMS & DISCUSSION SUMMARY:
1. Review of Q3 Vulnerability Scanning Reports (IT Dept):
   - Patch SLA compliance improved from 72% to 88% across regional offices.
   - Action: IT to remediate remaining critical patches on core servers by Oct 5.

2. Review of Risk Acceptance Request (RISK-2026-08):
   - Legal Counsel raised concern regarding NDPA/GDPR compliance exposure.
   - Decision: Approved with mandatory compensating IP-whitelisting controls.

3. MFA Mandate Enforcement:
   - SGC approved mandatory rollout of hardware token MFA for privileged IT users.

DECISION LOG REFERENCE: SGC-DEC-2026-09-20-01 to SGC-DEC-2026-09-20-03
NEXT MEETING DATE    : October 18, 2026
================================================================================

Evidence Bundle 3: Quarterly Board Cyber Risk Scorecard Briefing
================================================================================
              TECHGLOBAL BOARD AUDIT & RISK COMMITTEE
                   QUARTERLY CYBER RISK BRIEFING (Q3 2026)
================================================================================

1. EXECUTIVE RISK DASHBOARD METRICS:
   -----------------------------------------------------------------------------
   Metric                               Target       Q2 Status    Q3 Status
   -----------------------------------------------------------------------------
   Mean Time to Detect (MTTD)          < 2 Hours    4.2 Hours    1.8 Hours [PASS]
   Mean Time to Respond (MTTR)         < 4 Hours    6.5 Hours    3.2 Hours [PASS]
   Critical Patch SLA Compliance (>14d) > 95%        72.0%        88.0%     [WARN]
   Security Awareness Completion       > 95%        81.0%        96.5%     [PASS]
   Unmitigated High Risks Registered    0            4            1         [WARN]

2. TOP ENTERPRISE CYBER RISKS SUMMARY:
   - Cloud Security Misconfiguration (Risk Score: HIGH) - Remediation in progress.
   - Third-Party Vendor Access Integrity (Risk Score: MEDIUM) - Audits ongoing.

3. MATERIAL INCIDENTS THIS QUARTER:
   - ZERO Level 3 (Material/Board Level) security breaches reported in Q3.

4. CISO STRATEGIC RECOMMENDATIONS FOR BOARD APPROVAL:
   - Authorize $150,000 CapEx allocation for 24/7 Managed SOC expansion.
================================================================================


---

References & Bibliography
Information Systems Audit and Control Association (ISACA). (2019). COBIT 2019 Framework: Governance and Management Objectives. ISACA.

International Organization for Standardization. (2020). Information technology — Security techniques — Governance of information security (ISO/IEC Standard No. 27014:2020). ISO/IEC.

International Organization for Standardization. (2022). Information security, cybersecurity and privacy protection — Information security management systems — Requirements (ISO/IEC Standard No. 27001:2022). ISO/IEC.

National Institute of Standards and Technology (NIST). (2024). The NIST Cybersecurity Framework (CSF) 2.0 (NIST Special Publication 1299). U.S. Department of Commerce.

Nigeria Data Protection Commission (NDPC). (2023). Nigeria Data Protection Act (NDPA) 2023. Federal Republic of Nigeria.
