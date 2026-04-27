# Control Baseline Summary — Reference 3
## NEXUS Electronic Health Records System | Step 3 — Select Controls

| Field | Detail |
|---|---|
| **Document Reference** | NEXUS-RMF-SEL-001 |
| **Document Type** | Control Baseline Summary (Ref 3) |
| **System Name** | NEXUS Electronic Health Records System |
| **Version** | 1.0 |
| **Classification** | Internal — Controlled |
| **Baseline Applied** | NIST SP 800-53 Rev 5 — HIGH Impact Baseline |
| **Tailoring Authority** | ISSO / System Owner / Authorising Official |
| **Prepared By** | [Chioma Otteh], Lead Information Security Analyst |
| **Reviewed By** | [Jack Taylor], Director of Clinical Informatics |
| **Approved By** | [Ben JAckson], Chief Information Officer |
| **Date** | 2026|
| **References** | NIST SP 800-53 Rev 5 · NIST SP 800-37 Rev 2 · FIPS 199 · HIPAA Security Rule 45 CFR Part 164 |

---

## Table of Contents

1. [Purpose and Scope](#1-purpose-and-scope)
2. [Baseline Selection Rationale](#2-baseline-selection-rationale)
3. [Tailoring Overview](#3-tailoring-overview)
4. [Control Baseline Summary Table — All 20 Families](#4-control-baseline-summary-table--all-20-families)
5. [Priority Controls Detail — Critical Families for NEXUS](#5-priority-controls-detail--critical-families-for-nexus)
6. [Inherited Controls — AWS Shared Responsibility](#6-inherited-controls--aws-shared-responsibility)
7. [HIPAA Security Rule to NIST SP 800-53 Control Mapping](#7-hipaa-security-rule-to-nist-sp-800-53-control-mapping)
8. [Control Ownership Matrix](#8-control-ownership-matrix)
9. [Approval and Sign-off](#9-approval-and-sign-off)
   



## 1. Purpose and Scope

### 1.1 Purpose

This Control Baseline Summary documents the complete set of security and privacy controls selected for the NEXUS Electronic Health Records System in accordance with NIST SP 800-37 Rev 2 Step 3. It constitutes **Reference 3: Control Baseline Summary** for the NEXUS RMF package.

The document:
- Confirms the HIGH impact baseline as the starting point
- Records all tailoring decisions with justifications
- Maps controls to HIPAA Security Rule requirements
- Identifies controls inherited from AWS (common controls)
- Assigns implementation responsibility for each control family
- Provides the foundation for Step 4 (Implementation) and Step 5 (Assessment)

### 1.2 System Context

NEXUS is a hybrid EHR platform processing PHI and PII across a multi-site clinical environment. Its unique characteristics drive specific tailoring decisions:

| NEXUS Characteristic | Tailoring Implication |
|---|---|
| HIPAA-regulated PHI/PII | HIPAA-specific control enhancements added |
| Hybrid AWS + on-premises | AWS inherited controls documented; gaps filled by NEXUS |
| Medical IoT device integration | IoT-specific controls added (SC, SI families) |
| Multi-site clinical dependency | Availability and contingency controls strengthened |
| Active clinical care (patient safety) | Integrity controls elevated; zero tolerance for data corruption |
| 500,000+ patient records | Privacy controls (PT family) applied in full |


## 2. Baseline Selection Rationale

### 2.1 FIPS 199 Drives Baseline

The NIST SP 800-53 Rev 5 control baseline is determined directly by the FIPS 199 categorisation result:

| FIPS 199 Level | Required Baseline |
|---|---|
| LOW | LOW baseline |
| MODERATE | MODERATE baseline |
| HIGH | **HIGH baseline** ← NEXUS |

NEXUS was categorised as HIGH across all three objectives. The HIGH baseline is therefore **mandatory** and represents the minimum acceptable control posture.

### 2.2 HIGH Baseline Scope

The HIGH baseline represents the complete set of security controls in NIST SP 800-53 Rev 5 applicable to HIGH impact systems. It includes:
- All controls in the LOW baseline
- All additional controls in the MODERATE baseline
- Additional HIGH-specific controls and control enhancements
- All 20 control families

### 2.3 Tailoring Authority

Per NIST SP 800-37 Rev 2 §2.3, the following officials authorise tailoring decisions:

| Decision Type | Authorising Official |
|---|---|
| Add controls beyond baseline | ISSO with AO approval |
| Modify control parameters | ISSO with System Owner approval |
| Scope out controls (with justification) | ISSO with AO approval |
| Document inherited controls | ISSO |


## 3. Tailoring Overview

### 3.1 Tailoring Actions Applied to NEXUS

| Tailoring Action | Number of Controls | Examples |
|---|---|---|
| **Selected as-is from HIGH baseline** | Majority | AC-2, AU-2, IA-5, SI-2 |
| **Enhanced beyond HIGH baseline** | 18 controls | AC-2(7), IA-2(1)(2), AU-9(2), IR-6(1) |
| **Added — HIPAA-specific** | 12 controls | AC-3(7), AU-11, SC-28(1), IR-6 |
| **Added — Healthcare/IoT context** | 8 controls | SC-8(1), SI-3(2), SA-9(2), SC-20 |
| **Inherited from AWS** | 22 controls | PE-1 through PE-20, MA-1 through MA-6 |
| **Scoped out (not applicable)** | 3 controls | SA-11(6) — not applicable (no formal dev programme) |

### 3.2 Tailoring Principles Applied

1. **HIPAA floor:** No control may be scoped out if it maps to a required HIPAA Security Rule standard
2. **Patient safety priority:** Integrity and availability controls are elevated where patient care is directly affected
3. **AWS shared responsibility:** AWS inherits physical, environmental, and hypervisor-level controls; NEXUS is responsible for controls within the cloud environment
4. **Least privilege:** All access control parameters set to minimum necessary for role function
5. **Defence in depth:** Multiple overlapping controls applied for PHI protection



## 4. Control Baseline Summary Table — All 20 Families

> **Legend:**
> - ✅ Selected (HIGH baseline)
> - ➕ Enhanced or added beyond baseline
> - 🔵 Inherited from AWS
> - ⬜ Scoped out (not applicable — with justification)
> - 🔴 Critical priority for NEXUS
> - 🟡 High priority for NEXUS
> - 🟢 Moderate priority for NEXUS


### AC — Access Control 🔴 Critical

| Control | Control Name | Status | HIPAA Mapping | NEXUS Notes |
|---|---|---|---|---|
| AC-1 | Access Control Policy and Procedures | ✅ | §164.308(a)(1) | Policy covers all NEXUS user roles |
| AC-2 | Account Management | ✅ ➕ | §164.308(a)(3)(ii)(C) | Enhanced: automated provisioning/de-provisioning; quarterly reviews |
| AC-2(1) | Account Management — Automated System Account Management | ➕ | §164.308(a)(3) | Active Directory automation required |
| AC-2(3) | Account Management — Disable Inactive Accounts | ✅ | §164.308(a)(3)(ii)(C) | 90-day inactivity threshold |
| AC-2(7) | Account Management — Privileged User Accounts | ➕ | §164.308(a)(3) | Added: separate privileged accounts for all admins |
| AC-3 | Access Enforcement | ✅ | §164.308(a)(4) | RBAC enforced: Clinical, Admin, Billing, Auditor, SA roles |
| AC-3(7) | Access Enforcement — Role-Based Access Control | ➕ | §164.308(a)(4)(i) | Added: explicit RBAC policy with minimum necessary standard |
| AC-4 | Information Flow Enforcement | ✅ | §164.312(e)(1) | VPN tunnel enforces AWS ↔ on-premises flow |
| AC-5 | Separation of Duties | ✅ | §164.308(a)(3) | No single person controls PHI access + audit log |
| AC-6 | Least Privilege | ✅ | §164.308(a)(4)(ii)(B) | Minimum necessary — each role limited to required PHI |
| AC-6(1) | Least Privilege — Authorise Access to Security Functions | ➕ | §164.308(a)(4) | Security function access restricted to ISSO/ISSM |
| AC-6(5) | Least Privilege — Privileged Accounts | ✅ | §164.308(a)(4) | Privileged access reviewed quarterly |
| AC-6(9) | Least Privilege — Log Use of Privileged Functions | ➕ | §164.312(b) | All privileged actions logged to Audit Server |
| AC-7 | Unsuccessful Login Attempts | ✅ | §164.312(d) | 5 attempts; 30-minute lockout |
| AC-8 | System Use Notification | ✅ | §164.308(a)(1) | HIPAA warning banner on all login screens |
| AC-11 | Device Lock | ✅ | §164.312(a)(2)(iii) | 15-minute auto-lock on all clinical endpoints |
| AC-12 | Session Termination | ✅ | §164.312(a)(2)(iii) | Automatic session termination after 30 minutes idle |
| AC-14 | Permitted Actions Without Identification | ✅ | §164.312(a)(1) | No PHI accessible without authentication |
| AC-17 | Remote Access | ✅ | §164.312(e)(1) | VPN + MFA required for all remote clinical access |
| AC-18 | Wireless Access | ✅ | §164.312(e)(1) | Wireless endpoints subject to same controls as wired |
| AC-19 | Access Control for Mobile Devices | ✅ | §164.312(a)(2)(iv) | MDM enforced on nurses' tablets; device encryption required |
| AC-20 | Use of External Systems | ✅ | §164.308(b)(1) | BAA required before PHI access from external system |
| AC-22 | Publicly Accessible Content | ✅ | §164.308(a)(1) | Patient portal reviewed — no unauthorised PHI exposure |



### AT — Awareness and Training 🟡 High

| Control | Control Name | Status | HIPAA Mapping | NEXUS Notes |
|---|---|---|---|---|
| AT-1 | Awareness and Training Policy | ✅ | §164.308(a)(5)(i) | Annual HIPAA security training policy |
| AT-2 | Literacy Training and Awareness | ✅ | §164.308(a)(5)(ii)(A) | Annual mandatory training for all NEXUS users |
| AT-2(2) | Literacy Training — Insider Threat | ➕ | §164.308(a)(5) | Added: insider threat awareness — PHI misuse scenarios |
| AT-3 | Role-Based Training | ✅ | §164.308(a)(5)(ii)(A) | Clinical, admin, IT roles each receive tailored training |
| AT-4 | Training Records | ✅ | §164.308(a)(5) | Training completion tracked in HR system; retained 6 years |
| AT-6 | Training Feedback | ✅ | §164.308(a)(1) | Annual review of training effectiveness |

---

### AU — Audit and Accountability 🔴 Critical

| Control | Control Name | Status | HIPAA Mapping | NEXUS Notes |
|---|---|---|---|---|
| AU-1 | Audit and Accountability Policy | ✅ | §164.312(b) | Covers all NEXUS components including AWS and on-premises |
| AU-2 | Event Logging | ✅ | §164.312(b) | All PHI access, modification, deletion, and login events logged |
| AU-3 | Content of Audit Records | ✅ | §164.312(b) | User ID, timestamp, event type, patient record accessed, outcome |
| AU-4 | Audit Log Storage Capacity | ✅ | §164.312(b) | On-premises Audit Server sized for 6-year retention |
| AU-5 | Response to Audit Processing Failures | ✅ | §164.312(b) | ISSO alerted immediately on logging failure |
| AU-6 | Audit Record Review, Analysis, and Reporting | ✅ | §164.308(a)(1)(ii)(D) | SIEM daily automated review; manual review weekly |
| AU-6(1) | Audit Record Review — Automated Process Integration | ➕ | §164.312(b) | SIEM integration — real-time anomaly alerting |
| AU-7 | Audit Record Reduction and Report Generation | ✅ | §164.308(a)(1)(ii)(D) | SIEM reporting dashboard |
| AU-8 | Time Stamps | ✅ | §164.312(b) | NTP synchronisation across all components |
| AU-9 | Protection of Audit Information | ✅ | §164.312(b) | Audit logs write-only; deletion restricted to ISSO role |
| AU-9(2) | Protection of Audit Information — Store on Separate System | ➕ | §164.312(b) | Added: dedicated on-premises Audit Logging Server; no co-location with primary DB |
| AU-10 | Non-Repudiation | ✅ | §164.312(c)(2) | Digital signatures on all clinical documentation events |
| AU-11 | Audit Record Retention | ➕ | §164.308(a)(1) | Added: 6-year minimum retention — HIPAA requirement exceeds baseline |
| AU-12 | Audit Record Generation | ✅ | §164.312(b) | All NEXUS components generate logs; forwarded to Audit Server |
| AU-13 | Monitoring for Information Disclosure | ➕ | §164.308(a)(1)(ii)(D) | Added: SIEM rules for bulk PHI export detection |
| AU-14 | Session Audit | ✅ | §164.312(b) | Full session recording for privileged users |



### CA — Assessment, Authorisation, and Monitoring 🔴 Critical

| Control | Control Name | Status | HIPAA Mapping | NEXUS Notes |
|---|---|---|---|---|
| CA-1 | Policy and Procedures | ✅ | §164.308(a)(1) | RMF process policy documented |
| CA-2 | Control Assessments | ✅ | §164.308(a)(8) | Annual SCA-led assessment; Step 5 of NEXUS RMF |
| CA-2(1) | Control Assessments — Independent Assessors | ➕ | §164.308(a)(8) | Third-party assessor for annual review |
| CA-3 | Information Exchange | ✅ | §164.308(b)(1) | All interconnections documented; BAAs in place |
| CA-5 | Plan of Action and Milestones | ✅ | §164.308(a)(8) | POA&M maintained and reviewed monthly by ISSO |
| CA-6 | Authorisation | ✅ | §164.308(a)(1) | Formal ATO from CIO (AO); reviewed annually |
| CA-7 | Continuous Monitoring | ✅ | §164.308(a)(8) | SIEM + vulnerability scanning + log review programme |
| CA-8 | Penetration Testing | ➕ | §164.308(a)(8) | Added: annual third-party penetration test |
| CA-9 | Internal System Connections | ✅ | §164.312(e)(1) | VPN tunnel and internal connections documented |



### CM — Configuration Management 🟡 High

| Control | Control Name | Status | HIPAA Mapping | NEXUS Notes |
|---|---|---|---|---|
| CM-1 | Configuration Management Policy | ✅ | §164.308(a)(1) | Covers AWS and on-premises components |
| CM-2 | Baseline Configuration | ✅ | §164.308(a)(1) | CIS Benchmarks applied to all servers and endpoints |
| CM-2(2) | Baseline Configuration — Automation | ➕ | — | AWS Systems Manager for cloud; SCCM for on-premises |
| CM-3 | Configuration Change Control | ✅ | §164.308(a)(1) | Change Advisory Board (CAB) approval for all changes |
| CM-4 | Impact Analysis | ✅ | §164.308(a)(1) | Security impact review before all changes |
| CM-5 | Access Restrictions for Change | ✅ | §164.308(a)(3) | Change access limited to authorised personnel |
| CM-6 | Configuration Settings | ✅ | §164.308(a)(1) | CIS Level 2 benchmarks; deviations documented |
| CM-7 | Least Functionality | ✅ | §164.308(a)(1) | Unnecessary services disabled on all components |
| CM-8 | System Component Inventory | ✅ | §164.308(a)(1) | Full asset inventory including IoT devices |
| CM-9 | Configuration Management Plan | ✅ | §164.308(a)(1) | Documented and maintained by IT Admin |
| CM-10 | Software Usage Restrictions | ✅ | §164.308(a)(1) | Software allowlist enforced on all endpoints |
| CM-12 | Information Location | ➕ | §164.308(a)(1) | Added: PHI data flow mapping maintained |



### CP — Contingency Planning 🔴 Critical

| Control | Control Name | Status | HIPAA Mapping | NEXUS Notes |
|---|---|---|---|---|
| CP-1 | Contingency Planning Policy | ✅ | §164.308(a)(7)(i) | Clinical downtime procedures included |
| CP-2 | Contingency Plan | ✅ | §164.308(a)(7)(ii)(B) | Covers AWS outage, VPN failure, DB failure scenarios |
| CP-2(1) | Contingency Plan — Coordinate with Related Plans | ➕ | §164.308(a)(7) | Coordinated with hospital emergency operations plan |
| CP-3 | Contingency Training | ✅ | §164.308(a)(7)(ii)(A) | Annual downtime drill for clinical staff |
| CP-4 | Contingency Plan Testing | ✅ | §164.308(a)(7)(ii)(D) | Annual tabletop + annual full failover test |
| CP-6 | Alternate Storage Site | ✅ | §164.308(a)(7)(ii)(B) | AWS S3 + Backup Vault (geographically separated) |
| CP-7 | Alternate Processing Site | ✅ | §164.308(a)(7)(ii)(C) | AWS multi-AZ; secondary on-premises DB at Site B |
| CP-8 | Telecommunications Services | ✅ | §164.308(a)(7)(ii)(B) | Redundant VPN paths; secondary internet circuit |
| CP-9 | System Backup | ✅ | §164.308(a)(7)(ii)(A) | Daily incremental; weekly full backup; tested quarterly |
| CP-9(1) | System Backup — Testing for Reliability | ➕ | §164.308(a)(7)(ii)(A) | Quarterly backup restoration test; results reported to ISSO |
| CP-10 | System Recovery and Reconstitution | ✅ | §164.308(a)(7)(ii)(C) | RTO < 4 hours; RPO < 1 hour |
| CP-11 | Alternate Communications Protocols | ✅ | §164.308(a)(7) | Backup communication path for inter-site connectivity |
| CP-13 | Alternative Security Mechanisms | ➕ | §164.308(a)(7) | Paper-based downtime procedures activated during outage |



### IA — Identification and Authentication 🔴 Critical

| Control | Control Name | Status | HIPAA Mapping | NEXUS Notes |
|---|---|---|---|---|
| IA-1 | Identification and Authentication Policy | ✅ | §164.312(d) | Covers all user types including patient portal |
| IA-2 | Identification and Authentication (Organisational Users) | ✅ | §164.312(d) | Unique user ID required for all staff |
| IA-2(1) | MFA — Network Access to Privileged Accounts | ✅ ➕ | §164.312(d) | MFA mandatory for all privileged accounts |
| IA-2(2) | MFA — Network Access to Non-Privileged Accounts | ➕ | §164.312(d) | Extended: MFA required for ALL clinical staff — not just privileged |
| IA-2(6) | MFA — Access to Accounts — Separate Device | ➕ | §164.312(d) | Hardware token or authenticator app required |
| IA-2(8) | MFA — Access to Accounts — Replay Resistant | ✅ | §164.312(d) | TOTP-based MFA; replay-resistant |
| IA-3 | Device Identification and Authentication | ✅ | §164.312(d) | IoT device certificates; MAC address registration |
| IA-4 | Identifier Management | ✅ | §164.312(d) | Unique identifiers; no shared accounts |
| IA-5 | Authenticator Management | ✅ | §164.312(a)(2)(i) | 90-day password rotation; complexity enforced |
| IA-5(1) | Authenticator Management — Password-Based Authentication | ✅ | §164.312(a)(2)(i) | Min 15 chars; complexity; no reuse of last 24 |
| IA-6 | Authentication Feedback | ✅ | §164.312(d) | Passwords masked on all interfaces |
| IA-7 | Cryptographic Module Authentication | ✅ | §164.312(e)(2)(ii) | FIPS 140-2 validated cryptographic modules |
| IA-8 | Identification and Authentication (Non-Organisational Users) | ✅ | §164.312(d) | Patient portal — separate authentication scheme |



### IR — Incident Response 🔴 Critical

| Control | Control Name | Status | HIPAA Mapping | NEXUS Notes |
|---|---|---|---|---|
| IR-1 | Incident Response Policy | ✅ | §164.308(a)(6)(i) | HIPAA breach response procedures included |
| IR-2 | Incident Response Training | ✅ | §164.308(a)(6)(ii) | Annual IR training; tabletop exercises |
| IR-3 | Incident Response Testing | ✅ | §164.308(a)(6) | Annual tabletop and simulated breach exercise |
| IR-4 | Incident Handling | ✅ | §164.308(a)(6)(ii) | 24/7 SOC; escalation to ISSO and CPO for PHI events |
| IR-4(1) | Incident Handling — Automated Incident Handling Processes | ➕ | §164.308(a)(6) | SIEM automated alerting; IR ticket creation |
| IR-5 | Incident Monitoring | ✅ | §164.308(a)(1)(ii)(D) | SIEM continuous monitoring; daily log review |
| IR-6 | Incident Reporting | ✅ ➕ | §164.308(a)(6)(ii) | Enhanced: HIPAA 60-day breach notification; HHS reporting |
| IR-6(1) | Incident Reporting — Automated Reporting | ➕ | §164.308(a)(6) | Automated escalation to ISSO within 1 hour of detection |
| IR-7 | Incident Response Assistance | ✅ | §164.308(a)(6) | IR retainer with third-party forensics firm |
| IR-8 | Incident Response Plan | ✅ | §164.308(a)(6)(ii) | HIPAA breach notification plan integrated |


### MP — Media Protection 🟡 High

| Control | Control Name | Status | HIPAA Mapping | NEXUS Notes |
|---|---|---|---|---|
| MP-1 | Media Protection Policy | ✅ | §164.310(d)(1) | Covers physical and digital media |
| MP-2 | Media Access | ✅ | §164.310(d)(1) | Restricted to authorised personnel |
| MP-3 | Media Marking | ✅ | §164.310(d)(1) | PHI-containing media labelled and tracked |
| MP-4 | Media Storage | ✅ | §164.310(d)(1) | Locked storage for removable media |
| MP-5 | Media Transport | ✅ | §164.310(d)(2)(i) | Encrypted transport; chain of custody documented |
| MP-6 | Media Sanitisation | ✅ | §164.310(d)(2)(i) | DoD 5220.22-M wipe or physical destruction before disposal |
| MP-7 | Media Use | ✅ | §164.310(d)(1) | USB storage disabled on clinical endpoints via MDM |
| MP-8 | Media Downgrading | ✅ | §164.310(d)(2) | Formal downgrade process before any media re-use |



### PE — Physical and Environmental Protection 🟢 Moderate

| Control | Control Name | Status | HIPAA Mapping | NEXUS Notes |
|---|---|---|---|---|
| PE-1 | Physical and Environmental Protection Policy | 🔵 AWS | §164.310(a)(1) | AWS-inherited for cloud zone |
| PE-2 | Physical Access Authorisations | 🔵 AWS / ✅ | §164.310(a)(2)(i) | AWS for cloud; NEXUS for on-premises data centres |
| PE-3 | Physical Access Control | 🔵 AWS / ✅ | §164.310(a)(2)(iii) | Badge access; CCTV at on-premises data centres |
| PE-6 | Monitoring Physical Access | 🔵 AWS / ✅ | §164.310(a)(2)(ii) | CCTV; access logs reviewed monthly |
| PE-8 | Visitor Access Records | ✅ | §164.310(a)(2)(ii) | Visitor log maintained at data centre entrance |
| PE-9 | Power Equipment and Cabling | 🔵 AWS / ✅ | §164.310(a)(1) | UPS at on-premises sites; AWS-managed for cloud |
| PE-10 | Emergency Shutoff | ✅ | §164.310(a)(1) | Emergency shutoff tested annually |
| PE-11 | Emergency Power | 🔵 AWS / ✅ | §164.310(a)(1) | Generator backup at on-premises data centres |
| PE-12 | Emergency Lighting | ✅ | §164.310(a)(1) | Emergency lighting at server rooms |
| PE-13 | Fire Protection | 🔵 AWS / ✅ | §164.310(a)(1) | FM-200 suppression at on-premises; AWS-managed for cloud |
| PE-14 | Environmental Controls | 🔵 AWS / ✅ | §164.310(a)(1) | HVAC; humidity monitoring at on-premises data centres |
| PE-15 | Water Damage Protection | 🔵 AWS / ✅ | §164.310(a)(1) | Raised floors; water detectors at on-premises |
| PE-16 | Delivery and Removal | ✅ | §164.310(d)(2) | Equipment intake and removal procedures |
| PE-17 | Alternate Work Site | ✅ | §164.308(a)(7) | Remote work VPN controls aligned with AC-17 |



### PL — Planning 🟢 Moderate

| Control | Control Name | Status | HIPAA Mapping | NEXUS Notes |
|---|---|---|---|---|
| PL-1 | Planning Policy and Procedures | ✅ | §164.308(a)(1) | RMF planning policy |
| PL-2 | System Security and Privacy Plans | ✅ | §164.308(a)(1) | SSP — this RMF package |
| PL-4 | Rules of Behaviour | ✅ | §164.308(a)(5)(ii)(C) | HIPAA acceptable use policy signed annually |
| PL-8 | Security and Privacy Architectures | ✅ | §164.308(a)(1) | System boundary diagram; data flow documentation |



### PM — Program Management 🟡 High

| Control | Control Name | Status | HIPAA Mapping | NEXUS Notes |
|---|---|---|---|---|
| PM-1 | Information Security Program Plan | ✅ | §164.308(a)(1) | Organisation-wide IS programme |
| PM-2 | Information Security Program Leadership Roles | ✅ | §164.308(a)(2) | CISO; ISSO; ISSM assigned |
| PM-3 | Information Security and Privacy Resources | ✅ | §164.308(a)(1) | Security budget allocated for NEXUS |
| PM-5 | System Inventory | ✅ | §164.308(a)(1) | Full system inventory maintained |
| PM-9 | Risk Management Strategy | ✅ | §164.308(a)(1)(ii)(B) | Enterprise risk management; RMF process |
| PM-10 | Authorisation Process | ✅ | §164.308(a)(1) | ATO process documented |
| PM-14 | Testing, Training, and Monitoring | ✅ | §164.308(a)(8) | Continuous monitoring programme |
| PM-15 | Contacts with Security Groups | ✅ | §164.308(a)(1) | ISAC membership; CISA liaison |
| PM-16 | Threat Awareness Program | ➕ | §164.308(a)(1) | Added: healthcare-specific threat intelligence (H-ISAC) |



### PS — Personnel Security 🟡 High

| Control | Control Name | Status | HIPAA Mapping | NEXUS Notes |
|---|---|---|---|---|
| PS-1 | Personnel Security Policy | ✅ | §164.308(a)(3)(i) | Workforce security policy |
| PS-2 | Position Risk Designation | ✅ | §164.308(a)(3)(ii)(A) | PHI-handling roles classified as high-risk positions |
| PS-3 | Personnel Screening | ✅ | §164.308(a)(3)(ii)(A) | Background check required before PHI access |
| PS-4 | Personnel Termination | ✅ | §164.308(a)(3)(ii)(C) | Account disabled within 24 hours of departure |
| PS-5 | Personnel Transfer | ✅ | §164.308(a)(3)(ii)(C) | Role change triggers access review and re-provisioning |
| PS-6 | Access Agreements | ✅ | §164.308(a)(3) | HIPAA confidentiality agreement signed at onboarding |
| PS-7 | External Personnel Security | ✅ | §164.308(b)(1) | Vendor/contractor PHI access governed by BAA |
| PS-8 | Personnel Sanctions | ✅ | §164.308(a)(1)(ii)(C) | HIPAA violation — disciplinary policy in place |
| PS-9 | Position Descriptions | ✅ | §164.308(a)(3) | Security responsibilities included in all job descriptions |



### PT — PII Processing and Transparency 🔴 Critical

| Control | Control Name | Status | HIPAA Mapping | NEXUS Notes |
|---|---|---|---|---|
| PT-1 | Policy and Procedures | ✅ | §164.520 | HIPAA Privacy Notice policy |
| PT-2 | Authority to Process PII | ✅ | §164.506 | Treatment, payment, operations basis documented |
| PT-3 | Personally Identifiable Information Processing Purposes | ✅ | §164.514 | PHI use limited to stated clinical purposes |
| PT-4 | Consent for PII Processing | ✅ | §164.508 | Patient authorisation records maintained |
| PT-5 | Privacy Notice | ✅ | §164.520 | Notice of Privacy Practices displayed and provided |
| PT-6 | System of Records Notice | ✅ | §164.501 | Patient record categories documented |
| PT-7 | Specific Categories of PII | ➕ | §164.514(b)(2) | Added: all 18 HIPAA Safe Harbour identifiers controlled |
| PT-8 | Computer Matching Requirements | ✅ | §164.514 | Data matching governed by minimum necessary standard |



### RA — Risk Assessment 🔴 Critical

| Control | Control Name | Status | HIPAA Mapping | NEXUS Notes |
|---|---|---|---|---|
| RA-1 | Risk Assessment Policy | ✅ | §164.308(a)(1)(ii)(A) | Annual formal risk assessment |
| RA-2 | Security Categorisation | ✅ | §164.308(a)(1)(ii)(A) | FIPS 199 — HIGH (this document package) |
| RA-3 | Risk Assessment | ✅ | §164.308(a)(1)(ii)(A) | Annual risk assessment; results feed POA&M |
| RA-3(1) | Risk Assessment — Supply Chain Risk Assessment | ➕ | — | Added: annual vendor/supply chain risk review |
| RA-5 | Vulnerability Monitoring and Scanning | ✅ | §164.308(a)(8) | Weekly vulnerability scans; critical patches within 30 days |
| RA-5(2) | Vulnerability Monitoring — Update Vulnerabilities | ➕ | §164.308(a)(8) | Automated NVD/CVE feed integration |
| RA-5(5) | Vulnerability Monitoring — Privileged Access | ➕ | §164.308(a)(8) | Credentialed scans for full vulnerability visibility |
| RA-7 | Risk Response | ✅ | §164.308(a)(1)(ii)(B) | Findings → POA&M within 5 business days |
| RA-9 | Criticality Analysis | ✅ | §164.308(a)(1) | PHI subsystems identified as critical |
| RA-10 | Threat Hunting | ➕ | §164.308(a)(1)(ii)(D) | Added: quarterly threat hunting exercises via SIEM |



### SA — System and Services Acquisition 🟡 High

| Control | Control Name | Status | HIPAA Mapping | NEXUS Notes |
|---|---|---|---|---|
| SA-1 | Policy and Procedures | ✅ | §164.308(b)(1) | Acquisition policy includes security and HIPAA requirements |
| SA-2 | Allocation of Resources | ✅ | §164.308(a)(1) | Security budget allocated in NEXUS programme |
| SA-3 | System Development Life Cycle | ✅ | §164.308(a)(1) | Security integrated into SDLC for NEXUS enhancements |
| SA-4 | Acquisition Process | ✅ | §164.308(b)(1) | Security and HIPAA requirements in all procurement |
| SA-5 | System Documentation | ✅ | §164.308(a)(1) | Architecture and configuration documentation maintained |
| SA-8 | Security and Privacy Engineering Principles | ✅ | §164.308(a)(1) | Privacy by design; defence in depth |
| SA-9 | External System Services | ✅ | §164.308(b)(1) | All third-party services assessed; BAA required |
| SA-9(2) | External System Services — Identification of Functions | ➕ | §164.308(b)(1) | Added: AWS service inventory with PHI-touching services identified |
| SA-10 | Developer Configuration Management | ✅ | §164.308(a)(1) | Vendor patch management requirements |
| SA-11 | Developer Testing and Evaluation | ✅ | §164.308(a)(8) | Security testing required for all NEXUS updates |
| SA-22 | Unsupported System Components | ➕ | §164.308(a)(1) | Added: EOL component inventory; no unsupported OS in PHI path |



### SC — System and Communications Protection 🔴 Critical

| Control | Control Name | Status | HIPAA Mapping | NEXUS Notes |
|---|---|---|---|---|
| SC-1 | Policy and Procedures | ✅ | §164.312(e)(1) | Communications security policy |
| SC-2 | Separation of System and User Functionality | ✅ | §164.308(a)(3) | Admin functions separated from clinical user functions |
| SC-3 | Security Function Isolation | ✅ | §164.308(a)(1) | Security functions isolated from application logic |
| SC-4 | Information in Shared System Resources | ✅ | §164.312(a)(2)(iv) | Memory cleared between sessions |
| SC-5 | Denial-of-Service Protection | ✅ | §164.308(a)(7) | AWS Shield; WAF rate limiting |
| SC-7 | Boundary Protection | ✅ | §164.312(e)(1) | Firewall/SG at all NEXUS boundaries |
| SC-7(3) | Boundary Protection — Access Points | ✅ | §164.312(e)(1) | Limited access points; all documented |
| SC-8 | Transmission Confidentiality and Integrity | ✅ | §164.312(e)(2)(ii) | TLS 1.2+ on all PHI transmission paths |
| SC-8(1) | Transmission — Cryptographic Protection | ➕ | §164.312(e)(2)(ii) | Added: TLS 1.3 preferred; TLS 1.0/1.1 explicitly disabled |
| SC-10 | Network Disconnect | ✅ | §164.312(a)(2)(iii) | VPN session termination after idle timeout |
| SC-12 | Cryptographic Key Establishment | ✅ | §164.312(a)(2)(iv) | AWS KMS for cloud; on-premises HSM |
| SC-13 | Cryptographic Protection | ✅ | §164.312(a)(2)(iv) | FIPS 140-2 validated modules; AES-256 |
| SC-17 | Public Key Infrastructure Certificates | ✅ | §164.312(d) | Internal PKI for VPN and device certificates |
| SC-18 | Mobile Code | ✅ | §164.308(a)(1) | Mobile code policy; patient portal reviewed |
| SC-20 | Secure Name/Address Resolution Service | ➕ | — | Added: DNSSEC for external-facing NEXUS domains |
| SC-23 | Session Authenticity | ✅ | §164.312(d) | Session tokens; CSRF protection |
| SC-28 | Protection of Information at Rest | ✅ | §164.312(a)(2)(iv) | AES-256 on all PHI storage |
| SC-28(1) | Protection at Rest — Cryptographic Protection | ➕ | §164.312(a)(2)(iv) | Added: customer-managed keys (CMK) in AWS KMS |
| SC-39 | Process Isolation | ✅ | §164.308(a)(1) | Application processes isolated per function |



### SI — System and Information Integrity 🔴 Critical

| Control | Control Name | Status | HIPAA Mapping | NEXUS Notes |
|---|---|---|---|---|
| SI-1 | Policy and Procedures | ✅ | §164.312(c)(1) | Integrity policy — covers PHI and system integrity |
| SI-2 | Flaw Remediation | ✅ | §164.308(a)(1)(ii)(A) | Critical patches within 30 days; High within 60 days |
| SI-2(2) | Flaw Remediation — Automated Patch Management | ➕ | §164.308(a)(1) | AWS Systems Manager Patch Manager; WSUS on-premises |
| SI-3 | Malicious Code Protection | ✅ | §164.308(a)(5)(ii)(B) | AV on all endpoints; EDR on servers |
| SI-3(2) | Malicious Code — Automatic Updates | ✅ | §164.308(a)(5)(ii)(B) | AV signatures auto-updated hourly |
| SI-4 | System Monitoring | ✅ | §164.308(a)(1)(ii)(D) | SIEM continuous monitoring; anomaly detection |
| SI-4(2) | System Monitoring — Automated Tools | ➕ | §164.308(a)(1)(ii)(D) | AWS GuardDuty for cloud; SIEM for on-premises |
| SI-4(4) | System Monitoring — Inbound/Outbound Traffic | ✅ | §164.312(e)(1) | WAF + IDS monitoring inbound; DLP monitoring outbound |
| SI-4(16) | System Monitoring — Correlate Monitoring Information | ➕ | §164.308(a)(1)(ii)(D) | SIEM correlation across all NEXUS components |
| SI-5 | Security Alerts, Advisories, and Directives | ✅ | §164.308(a)(1) | CISA alerts subscribed; H-ISAC membership |
| SI-6 | Security and Privacy Function Verification | ✅ | §164.308(a)(8) | Security function testing during maintenance windows |
| SI-7 | Software, Firmware, and Information Integrity | ✅ | §164.312(c)(1) | File integrity monitoring on all servers |
| SI-7(1) | Software Integrity — Integrity Checks | ➕ | §164.312(c)(1) | Added: automated FIM alerts on PHI-handling systems |
| SI-10 | Information Input Validation | ✅ | §164.312(c)(1) | Input validation on all NEXUS web forms |
| SI-12 | Information Management and Retention | ✅ | §164.308(a)(1) | 10-year retention; HIPAA minimum 6 years |
| SI-16 | Memory Protection | ✅ | §164.308(a)(1) | ASLR; DEP enabled on all servers |
| SI-18 | PII Quality Operations | ➕ | §164.308(a)(1) | Added: data quality controls for PHI accuracy |
| SI-19 | De-identification | ➕ | §164.514(b) | Added: de-identification procedures for data shared for research |



### SR — Supply Chain Risk Management 🟢 Moderate

| Control | Control Name | Status | HIPAA Mapping | NEXUS Notes |
|---|---|---|---|---|
| SR-1 | Policy and Procedures | ✅ | §164.308(b)(1) | Supply chain risk policy |
| SR-2 | Supply Chain Risk Management Plan | ✅ | §164.308(b)(1) | Covers AWS, IoT device vendors, software suppliers |
| SR-3 | Supply Chain Controls and Processes | ✅ | §164.308(b)(1) | Security requirements in all procurement contracts |
| SR-5 | Acquisition Strategies | ✅ | §164.308(b)(1) | Preferred vendors assessed; BAA required |
| SR-6 | Supplier Assessments and Reviews | ✅ | §164.308(b)(1) | Annual third-party vendor security review |
| SR-8 | Notification Agreements | ✅ | §164.308(b)(1) | Vendors required to notify of breaches affecting NEXUS |
| SR-10 | Inspection of Systems | ✅ | §164.308(b)(1) | IoT devices inspected before deployment |
| SR-11 | Component Authenticity | ✅ | §164.308(b)(1) | Hardware components verified through trusted suppliers |



## 5. Priority Controls Detail — Critical Families for NEXUS

This section provides additional detail on the highest-priority controls specific to the NEXUS healthcare context.

### 5.1 Access Control — AC-2: Account Management (Enhanced)

**Why critical for NEXUS:** Every NEXUS user account has the potential to access PHI. Unmanaged accounts — particularly orphaned accounts from departed employees — represent one of the highest-probability breach vectors in healthcare.

**NEXUS implementation requirement:**
- Accounts provisioned through Active Directory with RBAC group membership
- Accounts de-provisioned within **24 hours** of employee departure (HR-triggered automated workflow)
- Quarterly access reviews — ISSO reviews all accounts and certifies necessity
- Separate privileged accounts for all system administrators (no dual-use accounts)
- Service accounts inventoried and reviewed annually
- Patient portal accounts expire after 24 months of inactivity

---

### 5.2 Audit and Accountability — AU-2 / AU-9 / AU-11

**Why critical for NEXUS:** HIPAA §164.312(b) requires covered entities to implement hardware, software, and procedural mechanisms that record and examine activity in information systems containing ePHI. Audit logs are also the primary forensic tool for breach investigation.

**NEXUS implementation requirement:**
- Log ALL events: login/logout, failed authentication, PHI record view, PHI record modification, PHI record deletion, user account changes, privilege use, system configuration changes
- Logs forwarded in real-time to the dedicated on-premises **Audit Logging Server** (separate from Primary DB)
- SIEM analyses logs daily; ISSO reviews SIEM reports weekly
- Logs protected from deletion — only ISSO role can modify log retention settings
- Minimum retention: **6 years** (HIPAA minimum)
- Logs include: user ID, timestamp (NTP-synchronised), event type, patient record ID accessed, source IP, outcome (success/failure)


### 5.3 Identification and Authentication — IA-2 MFA Extensions

**Why critical for NEXUS:** Credential compromise is the leading cause of healthcare data breaches. Extending MFA beyond just privileged accounts to all clinical staff significantly reduces PHI exposure risk.

**NEXUS tailoring decision:** The HIGH baseline requires MFA for privileged accounts (IA-2(1)). NEXUS extends this to **all clinical staff** (IA-2(2)) — a tailoring addition justified by the sensitivity of PHI accessible at the clinical staff role level.

**NEXUS implementation requirement:**
- MFA enforced for: all privileged accounts, all clinical staff, all remote access
- Accepted MFA methods: TOTP authenticator app, hardware security key
- SMS OTP not accepted (SIM-swapping vulnerability)
- Patient portal: MFA offered; strongly encouraged but not yet mandatory


### 5.4 System and Communications Protection — SC-8/SC-28: Encryption

**Why critical for NEXUS:** HIPAA requires encryption of ePHI in transit (addressable) and at rest (addressable) — though given the sensitivity of NEXUS data, both are treated as required.

**NEXUS implementation requirement:**
- **In transit:** TLS 1.2 minimum on all paths; TLS 1.3 preferred; TLS 1.0 and 1.1 explicitly disabled
- **At rest:** AES-256 on all PHI storage (Primary DB, Secondary DB, S3, Backup Vault)
- **Key management:** AWS KMS with customer-managed keys (CMK) for cloud; on-premises HSM for database encryption keys
- **VPN:** IPSec with AES-256 and certificate-based mutual authentication
- **IoT:** Device-level encryption on all medical IoT data transmissions


### 5.5 Incident Response — IR-6: Breach Notification (HIPAA-Enhanced)

**Why critical for NEXUS:** The HITECH Act (amending HIPAA) requires covered entities to notify HHS and affected individuals within **60 days** of discovering a breach of unsecured PHI. Failure to notify carries penalties and reputational consequences.

**NEXUS tailoring addition:** The HIGH baseline IR-6 covers incident reporting. NEXUS adds HIPAA-specific breach notification procedures as a control enhancement.

**NEXUS implementation requirement:**
- Breach discovered → ISSO notified within **1 hour** (automated SIEM alert)
- ISSO notifies Privacy Officer and AO within **4 hours**
- Privacy Officer determines breach scope and notification obligation within **5 business days**
- Affected individuals notified within **60 days** of discovery
- HHS notified within **60 days** of discovery (OCR breach portal)
- If 500+ individuals affected: media notice in affected state required
- All breach investigations documented and retained for 6 years



## 6. Inherited Controls — AWS Shared Responsibility

The following controls are fully or partially inherited from Amazon Web Services under the AWS Shared Responsibility Model. NEXUS must verify these controls via AWS compliance documentation (SOC 2 Type II report, AWS Compliance Center).

| Control Family | Controls Inherited | Inherited From | NEXUS Responsibility |
|---|---|---|---|
| Physical and Environmental (PE) | PE-1 through PE-6, PE-9 through PE-15 | AWS data centres | Verify via AWS SOC 2 report annually |
| Maintenance (MA) | MA-1 through MA-6 | AWS infrastructure | Verify via AWS SOC 2 report annually |
| Media Protection — Physical (MP) | MP-1, MP-4, MP-6 (physical media) | AWS data centres | Verify via AWS SOC 2 report annually |
| Contingency — Data Centre (CP) | CP-6 (alternate storage), CP-7 (alternate processing) partial | AWS multi-AZ | NEXUS configures; AWS provides infrastructure |
| Identification — Hypervisor (IA) | IA-3 (device identification — hypervisor layer) | AWS | NEXUS responsible for OS and above |

**Important:** Inherited controls reduce NEXUS's implementation burden but do not eliminate NEXUS's responsibility to:
1. Verify the control is functioning (via AWS compliance reports)
2. Document the inheritance in the SSP
3. Ensure the inherited control actually covers the NEXUS use case



## 7. HIPAA Security Rule to NIST SP 800-53 Control Mapping

| HIPAA Security Rule Standard | 45 CFR Reference | Primary NIST 800-53 Controls |
|---|---|---|
| Security Management Process | §164.308(a)(1) | RA-3, PM-9, SI-2, CA-7 |
| Assigned Security Responsibility | §164.308(a)(2) | PM-2 |
| Workforce Security | §164.308(a)(3) | PS-3, PS-4, PS-5, AC-2 |
| Information Access Management | §164.308(a)(4) | AC-3, AC-6, AC-2 |
| Security Awareness and Training | §164.308(a)(5) | AT-2, AT-3 |
| Security Incident Procedures | §164.308(a)(6) | IR-4, IR-6, IR-8 |
| Contingency Plan | §164.308(a)(7) | CP-2, CP-9, CP-10 |
| Evaluation | §164.308(a)(8) | CA-2, CA-7 |
| Business Associate Contracts | §164.308(b)(1) | SA-9, PS-7, CA-3 |
| Facility Access Controls | §164.310(a) | PE-2, PE-3, PE-6 |
| Workstation Use | §164.310(b) | AC-11, AC-12, CM-7 |
| Workstation Security | §164.310(c) | PE-3, AC-19 |
| Device and Media Controls | §164.310(d) | MP-4, MP-6, MP-7 |
| Access Control | §164.312(a)(1) | AC-2, AC-3, AC-6, IA-2 |
| Audit Controls | §164.312(b) | AU-2, AU-3, AU-9, AU-11 |
| Integrity | §164.312(c) | SI-7, AU-10, SI-10 |
| Person Authentication | §164.312(d) | IA-2, IA-4, IA-5 |
| Transmission Security | §164.312(e) | SC-8, AC-17, AC-4 |



## 8. Control Ownership Matrix

| Control Family | Primary Owner | Secondary Owner | AWS Inherited |
|---|---|---|---|
| AC — Access Control | ISSO | System Administrator | No |
| AT — Awareness and Training | ISSO | HR / Training Lead | No |
| AU — Audit and Accountability | ISSO | SOC Analyst | No |
| CA — Assessment and Monitoring | ISSO / SCA | ISSM | No |
| CM — Configuration Management | System Administrator | ISSO | Partial |
| CP — Contingency Planning | ISSO | DBA / IT Admin | Partial |
| IA — Identification and Authentication | ISSO | System Administrator | No |
| IR — Incident Response | SOC Manager | Privacy Officer / ISSO | No |
| MA — Maintenance | System Administrator | ISSO | Partial (cloud) |
| MP — Media Protection | System Administrator | ISSO | Partial (cloud) |
| PE — Physical and Environmental | Facilities / IT Admin | ISSO | Partial (cloud) |
| PL — Planning | ISSO | System Owner | No |
| PM — Program Management | ISSM | ISSO | No |
| PS — Personnel Security | HR | ISSO | No |
| PT — PII Processing | Privacy Officer | ISSO | No |
| RA — Risk Assessment | ISSO | ISSM | No |
| SA — System Acquisition | System Owner | ISSO | No |
| SC — System and Comms Protection | ISSO | System Administrator / DBA | Partial (cloud infra) |
| SI — System and Info Integrity | ISSO | System Administrator | Partial (cloud) |
| SR — Supply Chain Risk | System Owner | ISSO | No |



## 9. Approval and Sign-off

| Role | Name | Signature | Date |
|---|---|---|---|
| Prepared By | [Chioma Otteh] | _________________________ | 2026 |
| Reviewed By | [Jack Taylor] | _________________________ | 2026|
| Reviewed By | [Jack Taylor] | _________________________ | 2026 |
| **Approved By** | **[Ben Jackson]** | _________________________ | **2026** |

---

## 
