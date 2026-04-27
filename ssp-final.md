# System Security Plan — Final
## NEXUS Electronic Health Records System | Step 4 — Implement Controls

| Field | Detail |
|---|---|
| **Document Reference** | NEXUS-RMF-SSP-001 |
| **Version** | 1.0 — Final |
| **Classification** | Internal — Controlled |
| **FIPS 199 Impact Level** | HIGH |
| **Control Baseline** | NIST SP 800-53 Rev 5 — HIGH |
| **Prepared By** | [ISSO Name] |
| **Approved By** | [AO Name] |
| **Date** | 2025 |

> See [ssp-cover-page.md](./ssp-cover-page.md) for the formal cover page, signature blocks, and document index (Reference 4).

---

## Table of Contents

1. [System Identification](#section-1--system-identification)
2. [System Description and Architecture](#section-2--system-description-and-architecture)
3. [System Environment](#section-3--system-environment)
4. [Security Categorisation](#section-4--security-categorisation)
5. [Information Types](#section-5--information-types)
6. [Control Baseline and Tailoring Summary](#section-6--control-baseline-and-tailoring-summary)
7. [Control Implementation Statements](#section-7--control-implementation-statements)
8. [Interconnection Agreements](#section-8--interconnection-agreements)
9. [Laws, Regulations, and Policies](#section-9--laws-regulations-and-policies)
10. [Plan of Action and Milestones](#section-10--plan-of-action-and-milestones)


## Section 1 — System Identification

| Attribute | Value |
|---|---|
| System Name | NEXUS Electronic Health Records System |
| System Abbreviation | NEXUS EHR |
| System Owner | [Name], Director of Clinical Informatics |
| Authorising Official | [Name], Chief Information Officer |
| ISSO | [Name], Lead Information Security Analyst |
| ISSM | [Name], Deputy Chief Information Security Officer |
| Privacy Officer | [Name], Chief Privacy Officer |
| System Administrator | [Name], IT Infrastructure Lead |
| Database Administrator | [Name], Senior Database Administrator |
| Incident Response Lead | [Name], SOC Manager |
| System Type | Major Application |
| Operational Status | Operational |
| Deployment Model | Hybrid — AWS Cloud + On-Premises |
| FIPS 199 Impact Level | HIGH (C: HIGH, I: HIGH, A: HIGH) |
| Control Baseline | NIST SP 800-53 Rev 5 HIGH |
| ATO Status | Pending — Awaiting Step 5 Assessment |


## Section 2 — System Description and Architecture

### 2.1 Mission and Purpose

NEXUS is a hybrid Electronic Health Records System designed to support comprehensive day-to-day healthcare operations across multi-site clinical environments. The system enables healthcare providers to manage patient records, lab results, referrals, appointments, billing, and clinical documentation in a secure and centralised environment.

NEXUS processes, stores, and transmits Protected Health Information (PHI) and Personally Identifiable Information (PII) for approximately 500,000+ active patient records, serving ~2,000 daily clinical and administrative users across all hospital sites.

### 2.2 Core Business Functions

| Function | Description |
|---|---|
| Patient Records Management | Creation, storage, retrieval, and update of comprehensive patient health records |
| Clinical Documentation | Physician notes, nursing assessments, discharge summaries, care plans |
| Laboratory Results | Ordering, tracking, and reviewing lab results linked to patient records |
| Referrals Management | Electronic referral creation, routing, and tracking between providers |
| Appointment Scheduling | Multi-site booking, reminders, and calendar management |
| Billing and Revenue Cycle | Insurance claims, payment processing, billing audit trails |
| Medication Management | Prescriptions, medication administration records (MAR) |
| Medical IoT Integration | Real-time vital signs capture from bedside and wearable monitoring devices |

### 2.3 Architecture Overview

NEXUS operates across three distinct security zones:

**Zone 1 — Internet Zone**
Untrusted external boundary. External users (patients, remote clinicians) access NEXUS via HTTPS. No PHI stored here. All traffic filtered before reaching the AWS zone.

**Zone 2 — AWS Cloud Zone**
- Security Stack: AWS Shield (DDoS), AWS WAF (application filtering), Application Load Balancer (ALB)
- Public Subnet: Web/App Server 1 and 2 (redundant) — NEXUS application logic
- Private Subnet: AWS Backup Vault and Amazon S3 — encrypted PHI backup and long-term storage

**Zone 3 — On-Premises Hospital Zone**
- Data Tier: Primary PostgreSQL DB Server (live PHI/PII), Secondary Failover Server (real-time replication)
- Security and Audit: Audit Logging Server, SIEM Monitoring Server
- Hospital Endpoints: Admin workstations, clinician laptops, nurses' tablets, medical IoT devices

The AWS Cloud Zone and On-Premises Hospital Zone are connected via an **IPSec VPN Tunnel** (AES-256, certificate-based mutual authentication). PHI is never transmitted over the public internet unencrypted.


## Section 3 — System Environment

### 3.1 Hardware and Software Inventory

| Component | Type | Location | OS / Platform | Role |
|---|---|---|---|---|
| Web/App Server 1 | AWS EC2 (m5.large) | AWS us-east-1 Public Subnet | Amazon Linux 2 | NEXUS application hosting |
| Web/App Server 2 | AWS EC2 (m5.large) | AWS us-east-1 Public Subnet | Amazon Linux 2 | NEXUS application — redundant |
| AWS Backup Vault | AWS managed service | AWS us-east-1 Private Subnet | AWS managed | Scheduled application backups |
| Amazon S3 Bucket | AWS managed service | AWS us-east-1 Private Subnet | AWS managed | Long-term encrypted PHI archival |
| Primary DB Server | Physical / VM | On-Premises Site A | RHEL 9 / PostgreSQL 15 | Primary PHI/PII data store |
| Secondary DB Server | Physical / VM | On-Premises Site B | RHEL 9 / PostgreSQL 15 | Failover and replication target |
| Audit Logging Server | Physical / VM | On-Premises Site A | RHEL 9 / Syslog-ng | Centralised audit log collection |
| SIEM Server | Physical / VM | On-Premises Site A | RHEL 9 / [SIEM Product] | Real-time monitoring and alerting |
| Admin Workstations | Physical desktop | All hospital sites | Windows 11 | Administrative NEXUS access |
| Clinician Laptops | Physical laptop | All hospital sites | Windows 11 | Clinical NEXUS access |
| Nurses' Tablets | Physical tablet | All hospital wards | iOS 17 (MDM managed) | Bedside charting and MAR |
| Medical IoT Devices | Specialised hardware | All hospital wards | Vendor firmware | Vital signs capture |
| VPN Gateway | Physical / VM | On-Premises Site A | [VPN Product] | IPSec tunnel to AWS |

### 3.2 Network Connectivity Summary

| Connection | Protocol | Encryption | Authentication |
|---|---|---|---|
| External users → AWS (Port 443) | HTTPS | TLS 1.2+ (TLS 1.3 preferred) | Username + MFA |
| AWS Cloud ↔ On-Premises | IPSec VPN | AES-256 | Certificate-based mutual auth |
| Primary DB ↔ Secondary DB | PostgreSQL streaming replication | TLS 1.2+ | Certificate-based |
| Hospital endpoints → NEXUS | HTTPS (internal) | TLS 1.2+ | Username + MFA |
| Medical IoT → Hospital LAN | Encrypted proprietary protocol | Device-level encryption | Device certificates |
| SIEM ← All components | Syslog/TLS | TLS 1.2+ | Read-only audit credentials |
| AWS App Servers → S3/Backup | AWS internal SDK | TLS 1.2+ / AES-256 | AWS IAM roles (CMK) |

---

## Section 4 — Security Categorisation

### 4.1 FIPS 199 Result

```
SC NEXUS EHR = {(Confidentiality, HIGH), (Integrity, HIGH), (Availability, HIGH)}
Overall System Impact Level: HIGH
```

### 4.2 Justification Summary

| Objective | Level | Justification |
|---|---|---|
| Confidentiality | HIGH | PHI/PII breach triggers HIPAA penalties up to $1.9M per category; direct patient harm through stigmatisation and discrimination; 500,000+ patient records at risk |
| Integrity | HIGH | Corrupted clinical data (altered prescriptions, lab results, allergy records) directly threatens patient safety at the point of care — risk of death |
| Availability | HIGH | NEXUS supports active real-time clinical care across all sites simultaneously; no viable manual fallback at 50,000+ daily transactions |

Full analysis: [categorise/fips199-system-categorisation.md](./fips199-system-categorisation.md)

---

## Section 5 — Information Types

Per NIST SP 800-60 Vol 2, NEXUS processes the following primary information types (all adjusted to HIGH):

| Information Type | SP 800-60 ID | C | I | A |
|---|---|---|---|---|
| Health Care Delivery Services | C.2.8.1 | HIGH | HIGH | HIGH |
| Patient Health Records (PHI) | C.2.8.1 / D.14 | HIGH | HIGH | HIGH |
| Patient Identity / PII | D.14 | HIGH | HIGH | HIGH |
| Laboratory Results | C.2.8.1 | HIGH | HIGH | HIGH |
| Prescriptions and Medications | C.2.8.1 | HIGH | HIGH | HIGH |
| Clinical Documentation | C.2.8.1 | HIGH | HIGH | HIGH |
| Medication Administration Records | C.2.8.1 | HIGH | HIGH | HIGH |
| Medical Device / IoT Data | C.2.8.1 | HIGH | HIGH | HIGH |
| Vital Signs (real-time) | C.2.8.1 | HIGH | HIGH | HIGH |
| Billing and Financial Records | D.12 | HIGH | HIGH | Moderate |
| Audit and Accountability Records | D.20 | HIGH | HIGH | Moderate |


---

## Section 6 — Control Baseline and Tailoring Summary

**Baseline applied:** NIST SP 800-53 Rev 5 — HIGH Impact Baseline
**Total controls selected:** 221 across 20 control families
**Tailoring actions:** 21 (14 additions, 3 enhancements, 3 inherited, 1 scoped out)

| Family | Controls | Key Tailoring |
|---|---|---|
| AC — Access Control | 23 | MFA extended to all clinical staff; separate privileged accounts |
| AU — Audit and Accountability | 16 | 6-year retention; dedicated Audit Server; SIEM bulk export detection |
| CA — Assessment and Monitoring | 9 | Annual third-party pen test added |
| CP — Contingency Planning | 13 | Quarterly backup restoration test; RTO < 4hr |
| IA — Identification and Authentication | 13 | MFA for all clinical staff (not just privileged) |
| IR — Incident Response | 10 | HIPAA breach notification procedures; 1-hour SIEM escalation |
| PT — PII Processing | 8 | All 18 HIPAA Safe Harbour identifiers explicitly controlled |
| SC — System and Comms Protection | 19 | TLS 1.3 preferred; TLS 1.0/1.1 disabled; CMK in AWS KMS |
| SI — System and Info Integrity | 18 | Automated FIM alerts; de-identification procedures |

Full detail: [select/control-baseline-summary.md](./control-baseline-summary.md)
Tailoring log: [-select/tailoring-decisions.md](./tailoring-decisions.md)

---

## Section 7 — Control Implementation Statements

> This section documents how each priority control is implemented within NEXUS. Implementation statements follow the format:
> - **Control Requirement** — what the control requires
> - **Implementation** — how NEXUS satisfies the requirement
> - **Evidence** — what artefacts demonstrate implementation
> - **Status** — current implementation state
> - **Responsible Party** — who owns this control
>
> Full control-by-control detail for all 221 controls is maintained in the [Control Implementation Statements](./IMP-control-implementation-statements.md) document.

---

### AC-2 — Account Management

**Control Requirement:** The organisation manages information system accounts including establishing, activating, modifying, reviewing, disabling, and removing accounts.

**Implementation:**
NEXUS implements role-based account management through Microsoft Active Directory integrated with the NEXUS application layer. Five defined roles exist: Clinical Staff, Administrative Staff, Billing Officer, System Administrator (privileged), and Read-Only Auditor. Each role is provisioned with the minimum access necessary to perform its function per the minimum necessary standard.

Account lifecycle procedures are as follows:
- **Provisioning:** HR submits a new user request to IT; IT creates the Active Directory account and assigns the correct NEXUS role group within 24 hours
- **Modification:** Role changes triggered by HR transfer notification; access re-provisioned within 24 hours of transfer
- **Review:** ISSO conducts quarterly access reviews; all accounts certified or de-provisioned
- **De-provisioning:** HR departure notification triggers automated Active Directory disable within 24 hours; NEXUS session terminated immediately
- **Privileged accounts:** System Administrators are issued separate privileged accounts; no dual-use accounts permitted
- **Inactive accounts:** Accounts inactive for 90 days are automatically flagged and disabled pending ISSO review
- **Service accounts:** All service accounts inventoried in the configuration management database; reviewed annually

**Evidence:** Active Directory group policy configuration; quarterly access review logs; HR-IT account provisioning workflow documentation; privileged account register

**Status:** Implemented
**Responsible Party:** ISSO (oversight); System Administrator (execution)
**HIPAA Mapping:** §164.308(a)(3)(ii)(C) — Termination Procedures

---

### AC-3 / AC-3(7) — Access Enforcement / Role-Based Access Control

**Control Requirement:** The system enforces approved authorisations for logical access to information and system resources; implements role-based access control.

**Implementation:**
NEXUS enforces access through a five-tier RBAC model applied at the application layer and backed by Active Directory group membership:

| Role | PHI Access Scope | System Functions |
|---|---|---|
| Clinical Staff | Full PHI for assigned patients | View, create, modify clinical records; order labs; prescribe |
| Administrative Staff | Demographics, scheduling, billing only | Appointments, billing, registration — no clinical notes |
| Billing Officer | Diagnosis codes, billing data only | Billing and insurance functions — no treatment records |
| System Administrator | No PHI access | System configuration, maintenance — data blind |
| Read-Only Auditor | Audit logs only (metadata, no PHI content) | Log review, reporting |

Access enforcement is applied at three layers: (1) Active Directory group membership, (2) NEXUS application-layer RBAC, and (3) PostgreSQL database row-level security policies. An authenticated user who is not in the correct role group cannot access PHI even if they bypass the application layer.

Patient portal users are provisioned a separate Patient role with access limited strictly to their own records.

**Evidence:** Active Directory group policy; NEXUS RBAC configuration documentation; PostgreSQL row-level security policy; role definitions document

**Status:** Implemented
**Responsible Party:** System Administrator (technical); ISSO (governance)
**HIPAA Mapping:** §164.308(a)(4)(i) — Isolating Healthcare Clearinghouse Functions; §164.308(a)(4)(ii)(B) — Minimum Necessary

---

### AC-17 — Remote Access

**Control Requirement:** The organisation establishes and documents usage restrictions, configuration and connection requirements, and implementation guidance for each type of allowed remote access.

**Implementation:**
Remote access to NEXUS is permitted only through two authorised pathways:

1. **Clinical and administrative remote access:** All remote users connect through the NEXUS patient portal or clinical web interface over HTTPS (TLS 1.2+). MFA is enforced at authentication. Sessions terminate automatically after 30 minutes of inactivity (AC-12).

2. **Administrative and maintenance remote access:** System administrators and IT personnel access the on-premises infrastructure via a dedicated VPN (IPSec, AES-256, certificate-based mutual authentication). Remote maintenance sessions are logged in full and reviewed by the ISSO monthly. Privileged sessions require the separate privileged account (AC-2(7)).

All other remote access methods (RDP without VPN, SSH without MFA, direct database connections from external networks) are blocked at the firewall and security group level. Remote access policy is documented and distributed to all staff with remote access capability.

**Evidence:** VPN configuration documentation; firewall/security group rule set; remote access policy; session logs; MFA enforcement configuration

**Status:** Implemented
**Responsible Party:** System Administrator
**HIPAA Mapping:** §164.312(e)(1) — Transmission Security

---

### AU-2 — Event Logging

**Control Requirement:** The organisation determines that the system is capable of auditing defined events and coordinates the security audit function with other organisations requiring audit-related information.

**Implementation:**
NEXUS logs the following events across all system components. Logs are generated at the source component and forwarded in real-time to the dedicated on-premises Audit Logging Server via TLS-encrypted Syslog:

**Authentication events:** All successful logins (user ID, timestamp, source IP, device); all failed login attempts (user ID, timestamp, source IP, reason); account lockouts; MFA success and failure; session termination

**PHI access events:** Every view of a patient record (user ID, patient record ID, timestamp, role); every creation of a clinical document; every modification to a patient record (before/after values logged); every deletion or voiding of a record; every prescription issued or modified; every lab result accessed

**Privileged actions:** All System Administrator actions; all account management operations; all configuration changes; all security group or firewall rule modifications

**System events:** Application start/stop; database start/stop; backup initiation and completion; VPN tunnel status; replication status changes; patch application

**Security events:** IDS/WAF alert triggers; failed authentication thresholds; bulk data access patterns (SIEM rule); SIEM alert generation

All log entries include: user ID or service account, timestamp (NTP-synchronised to ±1 second), event type and category, source IP address, target resource (patient record ID where applicable), outcome (success/failure).

**Evidence:** Syslog-ng forwarding configuration; Audit Server log samples; SIEM alert rule documentation; NTP configuration

**Status:** Implemented
**Responsible Party:** ISSO (policy); System Administrator (technical); SOC Analyst (daily review)
**HIPAA Mapping:** §164.312(b) — Audit Controls

---

### AU-9 / AU-9(2) — Protection of Audit Information / Separate Storage

**Control Requirement:** The system protects audit information and audit tools from unauthorised access, modification, and deletion. Audit records are stored on a component different from the component being audited.

**Implementation:**
Audit logs are protected through the following mechanisms:

**Separation:** The Audit Logging Server is a physically and logically separate server from the Primary Database Server, SIEM, and all application servers. Logs are written to the Audit Server in append-only mode. The Audit Server does not host any NEXUS application functions.

**Access restriction:** Log deletion and modification rights are restricted to the ISSO role. Standard system administrators and SOC analysts have read-only access to logs. Log access is itself logged (meta-audit).

**Integrity protection:** Logs are cryptographically signed on ingestion using SHA-256 hash chaining. Any modification to a historical log entry invalidates the hash chain and triggers an immediate SIEM alert.

**Availability:** Audit Server is protected by RAID storage and monitored 24/7 by SIEM. Storage capacity is reviewed quarterly. A low-storage alert triggers at 75% capacity.

**Backup:** Audit logs are included in daily backup to AWS Backup Vault (encrypted, AES-256, CMK).

**Evidence:** Audit Server configuration documentation; access control policy for log systems; hash chain integrity verification process; SIEM alert for log modification; RAID configuration; backup policy

**Status:** Implemented
**Responsible Party:** ISSO
**HIPAA Mapping:** §164.312(b) — Audit Controls

---

### AU-11 — Audit Record Retention

**Control Requirement:** The organisation retains audit records for a defined period to provide support for after-the-fact investigations of security incidents.

**Implementation:**
NEXUS retains all audit and security logs for a minimum of **6 years** from the date of creation, in alignment with HIPAA's 6-year retention requirement for security-relevant documentation (45 CFR §164.316(b)(2)(i)).

Retention is enforced as follows:
- **Active retention (Years 1–2):** Logs stored on the on-premises Audit Logging Server in searchable format; available for SIEM queries and incident investigation
- **Near-line retention (Years 2–4):** Logs archived to AWS S3 (encrypted, AES-256, CMK) with S3 Object Lock (WORM — Write Once, Read Many) to prevent deletion
- **Long-term retention (Years 4–6):** Logs transitioned to S3 Glacier (encrypted) for cost-effective long-term storage; retrievable within 12 hours
- **Deletion:** Logs are only deleted after 6 years and only following ISSO approval; deletion events themselves are logged

**Evidence:** S3 lifecycle policy configuration; S3 Object Lock policy; retention policy documentation; ISSO approval workflow for deletion

**Status:** Implemented
**Responsible Party:** ISSO (governance); System Administrator (technical)
**HIPAA Mapping:** §164.316(b)(2)(i) — Documentation Retention

---

### CA-2 / CA-2(1) — Control Assessments / Independent Assessors

**Control Requirement:** The organisation assesses the security controls in the system at defined frequencies to determine whether the controls are implemented correctly, operating as intended, and producing the desired outcome with respect to meeting established security requirements. Employs independent assessors to conduct control assessments.

**Implementation:**
NEXUS undergoes a formal annual security control assessment conducted by the Security Control Assessor (SCA). The assessment uses the three assessment methods defined in NIST SP 800-53A:
- **Examine:** Review of policies, procedures, architecture diagrams, configuration settings, and SSP documentation
- **Interview:** Structured interviews with the ISSO, System Administrator, DBA, SOC Manager, and Privacy Officer
- **Test:** Technical testing of control implementations including account management, encryption, logging, and access enforcement

**Independence requirement:** The SCA must be independent of NEXUS operations and the ISSO. For NEXUS, the annual assessment is conducted jointly by: (1) the Internal Audit Team (for process controls) and (2) an external third-party security assessor (for technical controls including penetration testing). The SCA role is occupied by a designated individual who has no operational responsibility for NEXUS.

The assessment produces a **Security Assessment Report (SAR)** — see [05-assess/security-assessment-report.md](../05-assess/security-assessment-report.md).

**Evidence:** Annual assessment schedule; SCA independence attestation; assessment methodology documentation; SAR from most recent assessment

**Status:** Implemented (process established; first full assessment scheduled)
**Responsible Party:** ISSO (coordination); SCA (execution); AO (review)
**HIPAA Mapping:** §164.308(a)(8) — Evaluation

---

### CA-7 — Continuous Monitoring

**Control Requirement:** The organisation develops a continuous monitoring strategy and implements a continuous monitoring programme.

**Implementation:**
NEXUS operates a continuous monitoring programme across the following activities:

| Activity | Frequency | Owner | Tool / Method |
|---|---|---|---|
| SIEM log review | Daily | SOC Analyst | On-premises SIEM |
| Vulnerability scanning | Weekly | ISSO / SA | AWS Inspector (cloud); Nessus (on-premises) |
| Critical patch monitoring | Daily | SA | NVD CVE feed; AWS Inspector findings |
| User access review | Quarterly | ISSO | Active Directory; manual review |
| Backup integrity test | Quarterly | DBA | Restoration to test environment |
| Control reassessment | Annually | SCA | Formal assessment (CA-2) |
| Penetration test | Annually | Third-party | External red team assessment |
| Risk assessment review | Annually | ISSO | Formal risk assessment update |
| POA&M status review | Monthly | ISSO | POA&M tracking document |
| Security status report to AO | Quarterly | ISSO | Written security status report |

SIEM alerting is configured for: bulk PHI access (>100 records in 10 minutes), failed authentication surges (>5 failures in 60 seconds), after-hours access to PHI by non-on-call staff, file integrity monitoring alerts, VPN tunnel disruption, replication lag >5 minutes, Audit Server disk >75% capacity.

**Evidence:** Continuous monitoring plan document; SIEM configuration and alert rules; vulnerability scan reports; quarterly access review records; backup test results

**Status:** Implemented
**Responsible Party:** ISSO (programme ownership); SOC (daily execution)
**HIPAA Mapping:** §164.308(a)(8) — Evaluation; §164.308(a)(1)(ii)(D) — Information System Activity Review

---

### CP-9 / CP-9(1) — System Backup / Reliability Testing

**Control Requirement:** The organisation conducts backups of system-level information, user-level information, and system documentation at defined frequencies. Tests backup information to verify media reliability and information integrity.

**Implementation:**
NEXUS operates a tiered backup strategy:

| Backup Type | Frequency | Target | Encryption | Retention |
|---|---|---|---|---|
| Database incremental | Daily (02:00 AM) | AWS Backup Vault | AES-256, CMK | 90 days |
| Database full | Weekly (Sunday 01:00 AM) | AWS Backup Vault + S3 | AES-256, CMK | 1 year |
| Application configuration | Weekly | AWS Backup Vault | AES-256, CMK | 1 year |
| Audit logs | Daily (continuous append) | AWS S3 (WORM) | AES-256, CMK | 6 years |
| System state | Weekly | AWS Backup Vault | AES-256, CMK | 1 year |

**Reliability testing (CP-9(1)):** A backup restoration test is conducted quarterly in a dedicated test environment (isolated from production). The test verifies:
- Backup files are accessible and not corrupted
- Database can be fully restored from the most recent full backup + incrementals
- Restoration completes within the defined RTO of 4 hours
- Restored data integrity verified by DBA (row count validation, sample record spot-check)

Test results are documented and reported to the ISSO. Failed restoration tests trigger immediate investigation and POA&M entry.

**RTO/RPO targets:** RTO < 4 hours (system fully operational); RPO < 1 hour (maximum data loss acceptable)

**Evidence:** AWS Backup Vault configuration; backup schedule documentation; quarterly restoration test reports; RTO/RPO policy

**Status:** Implemented
**Responsible Party:** DBA (execution); ISSO (oversight)
**HIPAA Mapping:** §164.308(a)(7)(ii)(A) — Data Backup Plan

---

### CP-10 — System Recovery and Reconstitution

**Control Requirement:** The organisation provides for the recovery and reconstitution of the system to a known state within a defined time period after a disruption, compromise, or failure.

**Implementation:**
NEXUS has documented recovery procedures for three primary failure scenarios:

**Scenario 1 — AWS Web/App Server failure:**
The Application Load Balancer automatically routes traffic to the remaining healthy server. If both servers fail, the ALB health check detects failure within 30 seconds and the on-call SA is paged. New EC2 instances are launched from the pre-configured AMI within 30 minutes. RTO: 1 hour.

**Scenario 2 — Primary Database failure:**
PostgreSQL streaming replication to the Secondary Failover Server maintains a lag of <1 minute. On primary failure, the DBA promotes the secondary to primary within 15 minutes using documented manual failover procedure. The VPN gateway is reconfigured to route app server queries to Site B. RTO: 30 minutes. RPO: <1 minute.

**Scenario 3 — Complete site failure (on-premises Site A):**
App servers rerouted to secondary DB at Site B. AWS Backup Vault restoration initiated for any data not captured in replication. Full restoration from backup tested quarterly. RTO: <4 hours. RPO: <1 hour.

**Clinical downtime procedure:** During any NEXUS outage, clinical staff activate the paper-based downtime procedure — pre-printed patient information sheets, paper MAR, and handwritten orders. Downtime data is reconciled into NEXUS within 4 hours of system restoration.

**Evidence:** Recovery procedure documentation; failover runbooks; downtime procedure binder (clinical); quarterly restoration test reports; ALB health check configuration

**Status:** Implemented
**Responsible Party:** DBA and SA (execution); ISSO (oversight)
**HIPAA Mapping:** §164.308(a)(7)(ii)(C) — Disaster Recovery Plan

---

### IA-2(1)(2) — MFA for Privileged and Non-Privileged Accounts

**Control Requirement:** The system implements multi-factor authentication for network access to privileged and non-privileged accounts.

**Implementation:**
Multi-factor authentication is enforced for all NEXUS user accounts at login, regardless of role. This is a tailoring enhancement beyond the HIGH baseline (which mandates MFA for privileged accounts only) — justified by the sensitivity of PHI accessible to all clinical roles.

**MFA Implementation:**
- **Authentication factors used:** (1) Username and password (knowledge factor) + (2) TOTP authenticator app or hardware security key (possession factor)
- **Accepted MFA methods:** Microsoft Authenticator app (TOTP); hardware FIDO2 security key (YubiKey or equivalent)
- **Rejected methods:** SMS OTP is not accepted due to SIM-swapping vulnerability
- **Enforcement point:** MFA challenge is enforced at the AWS ALB layer for external access and at the Active Directory federated authentication layer for internal access
- **Patient portal:** MFA is enforced for all patient portal users from initial registration
- **Emergency access:** A break-glass procedure exists for clinical emergencies. Break-glass accounts are tightly controlled, logged automatically, and reviewed by the ISSO within 24 hours of use

**Password requirements (IA-5(1)):**
- Minimum 15 characters
- Complexity: uppercase, lowercase, number, special character
- No reuse of last 24 passwords
- 90-day maximum age
- Dictionary attack protection enabled

**Evidence:** Active Directory MFA enforcement policy; Azure AD Conditional Access configuration; authenticator app enrolment records; break-glass procedure documentation; MFA bypass attempt logs

**Status:** Implemented
**Responsible Party:** System Administrator
**HIPAA Mapping:** §164.312(d) — Person Authentication

---

### IR-4 / IR-6 — Incident Handling / Incident Reporting (HIPAA Enhanced)

**Control Requirement:** The organisation implements an incident handling capability including preparation, detection, analysis, containment, eradication, and recovery. Reports incidents to appropriate authorities.

**Implementation:**
NEXUS operates a formal incident response programme aligned with NIST SP 800-61 Rev 2 and enhanced with HIPAA breach notification procedures.

**Incident Handling Phases:**

*Detection:* The SIEM monitors all NEXUS components 24/7 and generates automated alerts on defined triggers (bulk PHI access, failed auth surges, FIM alerts, anomalous after-hours access). The SOC Analyst reviews SIEM alerts daily during business hours; after-hours alerts page the on-call SOC analyst.

*Triage:* Analyst categorises the alert as True Positive (incident) or False Positive. True positives are escalated to ISSO within 1 hour.

*Containment:* ISSO and SOC Manager determine containment strategy. For PHI-involving incidents: isolate affected system, preserve forensic evidence, initiate breach assessment.

*HIPAA Breach Assessment:* Privacy Officer conducts a four-factor breach risk assessment per 45 CFR §164.402:
1. Nature and extent of PHI involved
2. Who used or received the PHI
3. Whether PHI was actually acquired or viewed
4. Extent to which risk has been mitigated

*Notification (IR-6 — HIPAA Enhanced):*
- **ISSO notified:** Within 1 hour of SIEM detection (automated alert)
- **Privacy Officer and AO notified:** Within 4 hours of ISSO notification
- **Breach determination:** Within 5 business days of detection
- **Affected individuals notified:** Within 60 days of discovery (by first-class mail; email if preference given)
- **HHS OCR notified:** Within 60 days via HHS breach portal
- **Media notice:** Required if 500+ individuals in a state are affected
- **All notifications logged** and retained for 6 years

*Eradication and Recovery:* Root cause identified; system restored from clean backup or rebuilt; patches applied; access credentials rotated where compromised.

*Post-Incident Review:* PIR completed within 2 weeks. Lessons learned documented. POA&M entry created for identified gaps.

**Evidence:** Incident Response Plan (IRP) document; SIEM alert configuration; HIPAA breach notification templates; IR ticketing system; past IR exercise reports; Privacy Officer breach risk assessment form

**Status:** Implemented
**Responsible Party:** SOC Manager (response lead); ISSO (coordination); Privacy Officer (breach notification)
**HIPAA Mapping:** §164.308(a)(6) — Security Incident Procedures; Breach Notification Rule §164.400–414

---

### RA-5 — Vulnerability Monitoring and Scanning

**Control Requirement:** The organisation monitors and scans for vulnerabilities in the system and hosted applications at a defined frequency and when new vulnerabilities are identified.

**Implementation:**
NEXUS operates a layered vulnerability management programme:

**Scanning cadence:**
- **Weekly automated scans:** AWS Inspector scans all EC2 instances (Web/App Servers) for OS and application vulnerabilities; Nessus (credentialed) scans all on-premises servers and endpoints
- **Daily CVE monitoring:** Automated feed from NIST NVD and CISA KEV (Known Exploited Vulnerabilities) catalogue; SIEM correlation of new CVEs against NEXUS component inventory
- **Quarterly credentialed deep scans:** Full credentialed vulnerability scan of all network-accessible NEXUS components

**Remediation timelines:**
| Severity | Remediation Deadline | Escalation |
|---|---|---|
| Critical (CVSS 9.0+) | 24–72 hours | ISSO + AO immediate notification |
| High (CVSS 7.0–8.9) | 30 days | ISSO notification |
| Medium (CVSS 4.0–6.9) | 90 days | POA&M tracked |
| Low (CVSS < 4.0) | 180 days | POA&M tracked |

**Patch management:** AWS Systems Manager Patch Manager handles cloud tier patching. WSUS / RHEL Satellite handles on-premises server patching. Clinical endpoints are managed via MDM (tablets) and SCCM (workstations/laptops). Patch status reports provided to ISSO weekly.

**Evidence:** AWS Inspector findings reports; Nessus scan reports; NVD/KEV alert integration documentation; patch management policy; patch status dashboard

**Status:** Implemented
**Responsible Party:** ISSO (programme); System Administrator (execution)
**HIPAA Mapping:** §164.308(a)(8) — Evaluation; §164.308(a)(1)(ii)(A) — Risk Analysis

---

### SC-8 / SC-8(1) — Transmission Confidentiality / Cryptographic Protection

**Control Requirement:** The system implements cryptographic mechanisms to prevent unauthorised disclosure of information during transmission. TLS 1.3 preferred; TLS 1.0 and 1.1 disabled.

**Implementation:**
All NEXUS data in transit is protected by TLS encryption. The following configuration is enforced:

**External (Internet → AWS):**
- TLS 1.3 preferred; TLS 1.2 accepted; TLS 1.0 and 1.1 explicitly disabled at ALB
- Strong cipher suites only: ECDHE-RSA-AES256-GCM-SHA384, ECDHE-RSA-CHACHA20-POLY1305
- HSTS (HTTP Strict Transport Security) enabled with 1-year max-age
- Certificate: SHA-256 signed; 2048-bit RSA minimum; renewed before expiry via automated Let's Encrypt / AWS ACM

**VPN (AWS Cloud ↔ On-Premises):**
- IPSec with IKEv2; AES-256-GCM encryption; SHA-256 integrity
- Certificate-based mutual authentication (both ends present certificates)
- PFS (Perfect Forward Secrecy) enabled

**Internal (Endpoints → NEXUS):**
- TLS 1.2+ on all internal HTTPS connections
- TLS 1.0 and 1.1 disabled at the application server configuration level

**Database Replication:**
- PostgreSQL SSL replication with TLS 1.2+; server and client certificates

**Medical IoT:**
- Device-level encrypted transmission; IoT devices communicate on a network-segmented VLAN

**Verification:** Annual TLS configuration scan using SSL Labs / Qualys SSL Server Test targeting the patient portal (target: A or A+ rating).

**Evidence:** ALB TLS policy configuration; VPN configuration documentation; SSL Labs scan report; cipher suite documentation; HSTS header configuration

**Status:** Implemented
**Responsible Party:** System Administrator
**HIPAA Mapping:** §164.312(e)(2)(ii) — Encryption and Decryption

---

### SC-28 / SC-28(1) — Protection of Information at Rest / Customer-Managed Keys

**Control Requirement:** The system implements cryptographic mechanisms to prevent unauthorised disclosure of information at rest. Customer-managed encryption keys required.

**Implementation:**
All PHI and PII stored within NEXUS is encrypted at rest using AES-256:

| Component | Encryption Method | Key Management |
|---|---|---|
| Primary PostgreSQL DB | PostgreSQL TDE + OS-level LUKS encryption | On-premises HSM (FIPS 140-2 validated) |
| Secondary PostgreSQL DB | PostgreSQL TDE + OS-level LUKS encryption | On-premises HSM (FIPS 140-2 validated) |
| AWS Backup Vault | AES-256 (SSE) | AWS KMS — Customer-Managed Key (CMK) |
| Amazon S3 (archive) | AES-256 (SSE-KMS) | AWS KMS — Customer-Managed Key (CMK) |
| Clinical endpoint hard drives | BitLocker (Windows) / FileVault (iOS MDM) | Active Directory BitLocker recovery key escrow; MDM key management |
| Application configuration secrets | AWS Secrets Manager | AWS KMS — CMK |

**Customer-Managed Keys (SC-28(1)):** AWS KMS CMKs are used for all cloud-tier encryption. CMKs are owned and controlled by Nexus Health System — AWS cannot access the unencrypted data. CMK rotation is set to automatic annual rotation. CMK access is restricted to the ISSO and System Administrator roles via AWS IAM.

**Key management policy:** HSM and CMK access logs are reviewed monthly by the ISSO. CMK deletion requires ISSO and AO approval with a 30-day waiting period before deletion takes effect.

**Evidence:** PostgreSQL encryption configuration; LUKS configuration on DB servers; AWS KMS CMK policy; AWS S3 bucket encryption configuration; BitLocker policy (GPO); MDM encryption enforcement; CMK access log reviews

**Status:** Implemented
**Responsible Party:** System Administrator (technical); ISSO (governance)
**HIPAA Mapping:** §164.312(a)(2)(iv) — Encryption and Decryption (at rest)

---

### SI-2 — Flaw Remediation

**Control Requirement:** The organisation identifies, reports, and corrects information system flaws; installs security-relevant software updates within an organisationally defined time period.

**Implementation:**
NEXUS operates a formal patch management programme:

**Discovery:** Vulnerabilities are identified through weekly Nessus/Inspector scans, daily CVE monitoring, and vendor security advisories. All findings are triaged by the ISSO against the NEXUS component inventory.

**Remediation timelines** (per Risk Tolerance Statement):
- Critical patches: within 24–72 hours; emergency change request raised
- High patches: within 30 days; standard change request
- Medium patches: within 90 days; tracked in POA&M
- Low patches: within 180 days; tracked in POA&M

**Patch deployment:**
- AWS EC2 (Web/App Servers): AWS Systems Manager Patch Manager; patches tested in staging before production deployment
- On-premises servers (RHEL): RHEL Satellite; patching in maintenance windows (Sunday 02:00–04:00 AM)
- Clinical endpoints (Windows): SCCM; patches deployed in phased rollout
- Nurses' tablets (iOS): MDM-enforced update policy; auto-update enabled
- Medical IoT: Vendor-managed patches; reviewed by SA before deployment; EOL devices tracked per SA-22

**Change management:** All patches processed through the Change Advisory Board (CAB) except Critical patches which use emergency change procedures with post-implementation CAB review.

**Evidence:** Patch management policy; SCCM/Satellite deployment reports; vulnerability scan reports; CAB meeting minutes; emergency change procedure documentation

**Status:** Implemented
**Responsible Party:** System Administrator (execution); ISSO (oversight)
**HIPAA Mapping:** §164.308(a)(1)(ii)(A) — Risk Analysis (addressing identified vulnerabilities)

---

### SI-4 — System Monitoring

**Control Requirement:** The organisation monitors the system to detect attacks and indicators of potential attacks, and monitors the system to identify unauthorised use.

**Implementation:**
NEXUS operates a layered system monitoring architecture combining cloud-native and on-premises tools:

**Cloud tier (AWS):**
- **AWS GuardDuty:** Machine-learning-based threat detection for EC2 instances and AWS API calls; alerts forwarded to SIEM
- **AWS WAF:** Web application firewall on ALB; blocks OWASP Top 10 attacks; logs all blocked and flagged requests
- **AWS CloudTrail:** Records all AWS API calls; forwarded to SIEM for correlation
- **VPC Flow Logs:** Network traffic logging for all EC2 instances

**On-premises tier:**
- **SIEM (on-premises):** Aggregates all logs from Audit Server, database servers, endpoints, VPN gateway, and IoT network; applies correlation rules and generates alerts
- **IDS:** Network-based IDS on hospital LAN segments
- **File Integrity Monitoring (FIM):** Tripwire/AIDE on all servers in the PHI data path; alerts on any unauthorised file modification

**SIEM Alert Rules (key):**
| Rule | Trigger | Response |
|---|---|---|
| Bulk PHI export | >100 patient records in 10 minutes by one user | ISSO notified; session reviewed |
| Failed auth surge | >5 failures per account in 60 seconds | Account locked; ISSO alerted |
| After-hours PHI access | PHI access by non-on-call clinical staff 23:00–06:00 | SOC review within 2 hours |
| FIM alert | Any modification to PHI-server system files | ISSO immediate notification |
| Replication lag | DB replication lag >5 minutes | DBA paged |
| Log server disk | >75% capacity | SA paged |

**Evidence:** GuardDuty configuration; WAF rule set; SIEM correlation rules; IDS configuration; FIM baseline and alert documentation; CloudTrail configuration; alert response log

**Status:** Implemented
**Responsible Party:** SOC Analyst (daily monitoring); ISSO (programme governance)
**HIPAA Mapping:** §164.308(a)(1)(ii)(D) — Information System Activity Review

---

### PT-2 / PT-7 — Authority to Process PII / Specific Categories of PII

**Control Requirement:** The organisation establishes the legal authority that permits the collection, use, maintenance, and sharing of PII. Applies additional processing conditions to specific categories of PII.

**Implementation:**
NEXUS processes PII under the following legal bases:

**Legal authority:** Treatment, payment, and healthcare operations under HIPAA §164.506. Patient authorisation obtained for uses beyond these purposes (HIPAA §164.508).

**Minimum necessary standard:** Access to PII/PHI is limited to the minimum necessary for each role to perform its function. This is enforced technically through RBAC (AC-3(7)) and operationally through the minimum necessary policy signed by all staff annually.

**All 18 HIPAA Safe Harbour identifiers are explicitly controlled (PT-7):**
The following identifiers present in NEXUS are classified as PHI and subject to full HIPAA safeguards — geographic data smaller than state; dates (except year); telephone numbers; email addresses; Social Security numbers (partial); medical record numbers; health plan beneficiary numbers; account numbers; device identifiers (IoT); IP addresses (audit logs); and all other unique identifying numbers or codes.

**Privacy Notice:** The HIPAA Notice of Privacy Practices is provided to all patients at first point of contact and posted on the patient portal. Updated notices are provided when material changes occur.

**Consent records:** Patient consent and authorisation records are maintained in NEXUS with a 10-year retention period.

**Evidence:** HIPAA Notice of Privacy Practices; minimum necessary policy; consent management module in NEXUS; PHI identifier inventory; legal basis documentation

**Status:** Implemented
**Responsible Party:** Privacy Officer
**HIPAA Mapping:** §164.520 — Notice of Privacy Practices; §164.506 — Treatment, Payment, Operations

---

## Section 8 — Interconnection Agreements

| Connected System / Party | Agreement Type | PHI Shared | Status |
|---|---|---|---|
| Amazon Web Services | Business Associate Agreement (BAA) + AWS Shared Responsibility Model | Yes (encrypted backup data) | Signed |
| External laboratory systems | Business Associate Agreement (BAA) | Yes (lab orders, results) | Signed |
| Insurance companies (billing) | Business Associate Agreement (BAA) | Yes (billing codes, diagnosis) | Signed |
| Referring physicians / external providers | Business Associate Agreement (BAA) | Yes (referral data, summaries) | Signed |
| IT support / managed service vendors | Confidentiality / NDA | No (audit logs only) | Signed |
| Medical IoT device manufacturers | BAA (where device data is stored) | Yes (vital signs → NEXUS DB) | Under review |
| Clinical research partners | Data Use Agreement (DUA) | De-identified only | N/A — case by case |

All BAAs are reviewed annually and updated when the scope of PHI sharing changes.

---

## Section 9 — Laws, Regulations, and Policies

| Requirement | Source | Applicability to NEXUS |
|---|---|---|
| ePHI administrative safeguards | HIPAA Security Rule §164.308 | All administrative controls — workforce, risk analysis, training, IR |
| ePHI physical safeguards | HIPAA Security Rule §164.310 | Facility access, endpoint controls, media disposal |
| ePHI technical safeguards | HIPAA Security Rule §164.312 | Access control, audit, integrity, authentication, transmission security |
| Breach notification | HIPAA Breach Notification Rule §164.400–414 | 60-day notification to HHS and individuals |
| PHI use and disclosure | HIPAA Privacy Rule §164.506 | Treatment, payment, operations basis |
| Individual rights | HIPAA Privacy Rule §164.524–528 | Patient access, amendment, accounting of disclosures |
| Enhanced enforcement | HITECH Act (2009) | Higher penalties; breach reporting obligations |
| Security and privacy controls | NIST SP 800-53 Rev 5 | HIGH baseline — all 20 control families |
| RMF process | NIST SP 800-37 Rev 2 | All 7 RMF steps |
| Minimum security requirements | FIPS 200 | HIGH impact system minimum requirements |

---

## Section 10 — Plan of Action and Milestones

The POA&M is initiated following the security assessment in Step 5. At SSP submission, no open critical or high findings exist from internal review. The following items have been identified internally and are tracked proactively:

| POA&M ID | Finding | Risk | Owner | Target Date | Status |
|---|---|---|---|---|---|
| PRE-001 | Medical IoT BAA under review for 3 device vendors | Low | ISSO | Q2 2025 | In Progress |
| PRE-002 | TLS 1.2 still present on 2 legacy clinical endpoint connections | Medium | SA | Q1 2025 | In Progress |
| PRE-003 | Annual penetration test not yet completed (first test scheduled) | Medium | ISSO | Q2 2025 | Scheduled |

Full POA&M will be populated following the Step 5 Security Assessment. See [06-authorise/poam.md](../06-authorise/poam.md).

---

*Document Reference: NEXUS-RMF-SSP-001 | Version 1.0 | Classification: Internal — Controlled*
*NEXUS EHR is a fictional system created for GRC portfolio demonstration purposes.*
