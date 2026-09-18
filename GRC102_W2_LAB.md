# NexusTech Solutions — Information Security Governance Report

---

### Task 1: Establish the Security Policy Hierarchy

<details>
<summary><b>Click to view Task 1 Requirements & Scenario</b></summary>

> **Scenario Requirement:** Define the security documentation hierarchy (Policy, Standard, Guideline, Procedure) covering purpose, authority, mandatory/recommended nature, and level of detail. Categorise all eight provided brainstorming statements with a one-sentence justification for each classification, and provide a policy hierarchy diagram.
> 
> **Statements to Categorise:**
> 1. All NexusTech employees must use multi-factor authentication (MFA) when accessing the corporate network remotely.
> 2. To configure MFA on your mobile device, download the Authenticator app, scan the QR code provided in the IT portal, and enter the six-digit verification code.
> 3. It is recommended that developers use parameterised queries to reduce SQL injection risk.
> 4. NexusTech is committed to protecting the confidentiality, integrity and availability of all client data.
> 5. All corporate laptops must have full-disk encryption enabled using BitLocker (Windows) or FileVault (macOS).
> 6. Employees should avoid connecting to public, unsecured Wi-Fi networks when travelling.
> 7. In the event of a suspected security breach, employees must immediately contact the IT Helpdesk at extension 5555.
> 8. Passwords must be a minimum of 14 characters and contain at least one uppercase letter, one lowercase letter, one number and one special character.

</details>

#### Evidence Bundle 1: Hierarchy Deliverables
Evidence Bundle 1: Policy Hierarchy, Hierarchy Diagram and Statement Categorisation
1. Hierarchy Definition Table
Tier
Document Type
Purpose
Authority
Mandatory / Recommended
Level of Detail
1
Policy
Establishes high-level strategic direction, governance goals, and management intent.
Board / CEO
Mandatory
High-level; defines what and why.
2
Standard
Mandates specific minimum technical baselines and configuration requirements.
CISO / IT Director
Mandatory
Specific; defines minimum measurable specifications.
3
Guideline
Recommends operational best practices and implementation options.
Security Team / SMEs
Discretionary / Recommended
Flexible; offers advice and best practices.
4
Procedure
Outlines step-by-step instructions to execute operational tasks.
System Administrators
Mandatory
Highly detailed; defines how, when, and by whom.



2. Statement Categorisation and Justification
Policy: Sets an enterprise wide mandate requiring multi factor authentication for remote access without step by step technical instructions.
Procedure: Provides sequential operational steps directing an employee on how to configure an authenticator app.
Guideline: Uses discretionary language ("recommended") to suggest secure coding best practices for developers.
Policy: States executive security intent and core principles regarding client data protection.
Standard: Mandates a specific hardware configuration and names approved platform technologies (BitLocker/FileVault).
Guideline: Offers advisory behavior recommendations ("should avoid") for remote workers on public Wi-Fi.
Procedure: Directs immediate, step by step actions for reporting a suspected security incident.
Standard: Defines measurable technical requirements for password complexity that systems must enforce.
+-----------------------------------+
                  |             POLICY                |
                  |  Executive Intent & Mandates      |
                  |   (e.g., Acceptable Use Policy)   |
                  +-----------------+-----------------+
                                    |
                                    v
                  +-----------------------------------+
                  |            STANDARDS              |
                  |   Mandatory Technical Baselines   |
                  |   (e.g., Password Requirements)   |
                  +-----------------+-----------------+
                                    |
                +-------------------+-------------------+
                |                                       |
                v                                       v
+-----------------------------------+   +-----------------------------------+
|            PROCEDURES             |   |            GUIDELINES             |
| Step-by-Step Operating Directives |   | Discretionary Best Practices      |
|  (e.g., User Access Provisioning) |   | (e.g., Secure Coding Guidance)    |
+-----------------------------------+   +-----------------------------------+

---

---

### Task 2: Draft an Effective Acceptable Use Policy (AUP)

<details>
<summary><b>Click to view Task 2 Requirements & Scenario</b></summary>

> **Scenario Requirement:** Draft a complete, professionally formatted Acceptable Use Policy (AUP) for NexusTech Solutions to address unauthorised software downloads, unapproved personal cloud usage, and compliance risks.
> 
> **Mandatory Structure:**
> * Document control (Title, Version, Policy Owner, Approval Authority, Effective Date, Review Date).
> * Purpose and Scope.
> * Clear, concise, and enforceable policy statements (Acceptable use, Prohibited activities, Reasonable personal use).
> * Roles and responsibilities (Users, IT/Security, Managers, HR, CEO).
> * Compliance, exceptions handling, and enforcement mechanisms.
> * Formal approval information.

</details>

#### Evidence Bundle 2: Acceptable Use Policy Deliverables
Evidence Bundle 2: Acceptable Use Policy (AUP)
Document Control
Document Ref: NTS-POL-SEC-001 | Version: 1.0
Owner: Information Security Manager | Approver: Marcus Vance, CEO
Effective Date: 18 September 2026 | Review Date: 18 September 2027
1. Purpose and Scope
This policy defines requirements for the acceptable, secure use of NexusTech Solutions (NexusTech) IT assets, network resources, and data. It applies to all full time employees, contractors, consultants, and third parties accessing corporate systems or data.
2. Policy Statements
Acceptable Use: IT assets must be used primarily for legitimate business functions. Equipment and client data must be protected against unauthorized access, loss, or theft.
Prohibited Activities: Users shall not install unauthorized third-party software, exfiltrate or store company data on unapproved personal cloud accounts (e.g., personal Google Drive, Dropbox), bypass security controls, or share corporate login credentials.
Personal Use: Incidental personal use is permitted if it remains reasonable, lawful, non disruptive, and creates no expectation of privacy.
3. Roles and Responsibilities
CEO / Leadership: Approves policy and authorizes enforcement actions.
Information Security Manager: Maintains policy updates and oversees compliance monitoring.
IT Technicians: Enforces technical access controls and system configurations.
Users: Adheres to policy provisions and reports security incidents immediately.
4. Exceptions and Enforcement
Exceptions: Must be formally submitted to the GRC portal, undergo a risk assessment, include compensating controls, and receive written approval from the Information Security Manager.
Enforcement: Non compliance may result in disciplinary action up to termination of employment and legal prosecution.


---

---

### Task 3: Create an Actionable User Access Request Procedure

<details>
<summary><b>Click to view Task 3 Requirements & Scenario</b></summary>

> **Scenario Requirement:** Develop a step-by-step Standard Operating Procedure (SOP) for user access provisioning to eliminate informal requests via email/chat and ensure least-privilege access enforcement.
> 
> **Mandatory Elements:**
> * Purpose, scope, and prerequisites.
> * Request intake via approved ticketing workflow.
> * Verification of Line Manager and Data Owner approvals.
> * Identity verification and RBAC matrix alignment.
> * Account creation and permission assignment using template security groups.
> * Temporary credential delivery, MFA enrollment, and user notification.
> * Evidence capture, audit trail retention, and ticket closure.
> * Emergency ("Break-Glass") access procedures.

</details>

#### Evidence Bundle 3: User Access Procedure Deliverables
Evidence Bundle 3: User Access Request Procedure
Document Control
Document Ref: NTS-SOP-SEC-002 | Version: 1.0
Target Audience: IT Helpdesk Technicians, System Administrators

Operating Steps
[Requester / Manager]           [Service Desk Portal]             [IT Helpdesk]
           |                               |                             |
           |--- 1. Submits Ticket -------->|                             |
           |    (Informal requests rejected)|                             |
           |                               |                             |
           |--- 2. Digital Sign-off ------>|                             |
           |    (Manager & Data Owner)     |                             |
           |                               |                             |
                                           |--- 3. Assigns Ticket ------>|
                                           |                             |--- 4. Verifies RBAC Matrix
                                           |                             |    & Least-Privilege
                                           |                             |
                                           |                             |--- 5. Provisions Account
                                           |                             |    via AD/Entra Templates
                                           |                             |
                                           |                             |--- 6. Issues Temp Password
                                           |                             |    & Enrolls MFA
                                           |                             |
                                           |<-- 7. Attaches Logs & ------|
                                           |    Closes Ticket (Archived)

Request Intake: Requester or line manager submits a ticket through the IT Service Portal. Informal requests (email/chat) must be rejected.
Approval Verification: System routes ticket to Line Manager and Data Owner (for financial/health data) for digital sign-off.
Identity Verification: Technician verifies requested roles against the Role Based Access Control (RBAC) matrix using least privilege principles.
Provisioning Execution: Technician provisions user in Active Directory/Entra ID using pre configured security group templates.
MFA Enrolment: Technician generates a temporary password ("Change on First Login") and provides MFA setup instructions.
Audit Logging and Closure: Technician attaches approval records to the ticket, sets status to "Closed," and archives logs for audit trails.
Emergency Access: "Break Glass" access requires verbal authorization from an Incident Commander, is capped at 8 hours, and requires retrospective manager approval within 24 hours.


---

---

### Task 4: Policy Implementation and Communication

<details>
<summary><b>Click to view Task 4 Requirements & Scenario</b></summary>

> **Scenario Requirement:** Design a comprehensive Communication and Training Plan for rolling out the new Acceptable Use Policy and Access Request Procedure across 250 employees.
> 
> **Mandatory Elements:**
> * Target audience segmentation (General Employees, IT Staff, Executive Leadership).
> * Key messages and appropriate delivery channels for each audience.
> * Implementation timeline and policy attestation/acknowledgement mechanism.
> * Rollout effectiveness metrics and success criteria.
> * Multi-stage non-compliance escalation framework.

</details>

#### Evidence Bundle 4: Communication & Training Plan Deliverables
Evidence Bundle 4: Communication and Training Plan
Audience
Key Message
Delivery Channel
Owner
Timing
Attestation Mechanism
Success Metric
Executive Leadership
Governance rationale, risk mitigation, and manager approval duties.
Executive Briefing
InfoSec Manager
Week 1: Day 1
Digital Sign-off
100% executive sign-off.
All Staff
Usage rules, cloud storage restrictions, and incident reporting.
LMS Module & Intranet
InfoSec / HR
Weeks 2–3
Policy Click-Through
≥95% completion within 14 days.
IT Staff
Ticket-only provisioning workflows and enforcement.
Technical Workshop
IT Director
Week 1: Day 3
Signed SOP Acknowledgment
0% ticket bypass on audit.


Non-Compliance Escalation: Automated reminder at Day 14 → HR/Manager notification at Day 21 → Temporary account suspension at Day 28.



---

---

### Task 5: Policy Review and Maintenance

<details>
<summary><b>Click to view Task 5 Requirements & Scenario</b></summary>

> **Scenario Requirement:** Prepare a concise 2–3 paragraph Policy Review Memo addressed to the Information Security Steering Committee one year post-rollout.
> 
> **Mandatory Elements:**
> * Identify specific review triggers resulting from an AWS database migration and a personal cloud storage file-sharing incident.
> * Outline the policy review and stakeholder consultation process.
> * Propose at least two specific updates or clarifications to the Acceptable Use Policy.
> * Define the policy approval route, annual review schedule, and early-review triggers.

</details>

#### Evidence Bundle 5: Policy Review Memo Deliverables
Evidence Bundle 5: Policy Review and Maintenance Memo
MEMORANDUM

TO: Information Security Steering Committee

FROM: Information Security Manager

DATE: 18 September 2027

SUBJECT: Annual Policy Review Memo: AUP Updates

Review Triggers: A mandatory review was triggered by two events: (a) the migration of primary databases to AWS, which introduced new cloud access boundaries; and (b) a security incident where an employee shared sensitive files using personal cloud storage.
Proposed Updates:
Amend AUP Section 3.2 to explicitly prohibit transferring corporate data to unapproved personal cloud accounts or unsanctioned SaaS applications.
Add a Cloud Access control requiring all administrative database interactions to occur through enterprise Single Sign-On (SSO) and approved access brokers.
Approval & Schedule: The revised policy (v1.1) will be reviewed by HR/Legal and submitted to CEO Marcus Vance for signature. Moving forward, we will maintain an annual review cycle, with early reviews triggered by major IT changes or security incidents.


---

References
Federal Republic of Nigeria. (2023). Nigeria Data Protection Act (NDPA) 2023. Official Gazette of the Federal Republic of Nigeria.
Federal Republic of Nigeria. (2024). Cybercrimes (Prohibition, Prevention, etc.) Amendment Act 2024. Official Gazette of the Federal Republic of Nigeria.
International Organization for Standardization. (2022). Information security, cybersecurity and privacy protection — Information security management systems — Requirements (ISO/IEC Standard No. 27001:2022). https://www.iso.org/standard/27001
National Institute of Standards and Technology. (2014). Guidelines for Media Sanitization (NIST Special Publication 800-88, Revision 1). U.S. Department of Commerce. https://doi.org/10.6028/NIST.SP.800-88r1
National Institute of Standards and Technology. (2024). The NIST Cybersecurity Framework (CSF) 2.0 (NIST Special Publication 800-53, Revision 5). U.S. Department of Commerce. https://doi.org/10.6028/NIST.CSWP.29
Types of Security Policies [PowerPoint slides]. (n.d.). File: Types_of_Security_Policies (2).pptx.
