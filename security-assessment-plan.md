# Security Assessment Plan (SAP)
## NEXUS Electronic Health Records System | Step 5 — Assess Controls

| Field | Detail |
|---|---|
| **Document Reference** | NEXUS-RMF-SAP-001 |
| **Document Type** | Security Assessment Plan |
| **System Name** | NEXUS Electronic Health Records System |
| **Version** | 1.0 |
| **Classification** | Internal — Controlled |
| **Methodology** | NIST SP 800-53A Rev 5 |
| **Prepared By** | [SCA Name / Firm], Security Control Assessor |
| **Reviewed By** | [ISSO Name], Lead Information Security Analyst |
| **Approved By** | [AO Name], Chief Information Officer |
| **Assessment Period** | [Start Date] — [End Date], 2025 |
| **SAP Approval Date** | 2025 |

---

## Table of Contents

1. [Purpose and Scope](#1-purpose-and-scope)
2. [Assessor Independence](#2-assessor-independence)
3. [Assessment Methodology](#3-assessment-methodology)
4. [Controls to Be Assessed](#4-controls-to-be-assessed)
5. [Assessment Schedule](#5-assessment-schedule)
6. [Assessment Team and Roles](#6-assessment-team-and-roles)
7. [Information and Evidence Requirements](#7-information-and-evidence-requirements)
8. [Rules of Engagement](#8-rules-of-engagement)
9. [Reporting Requirements](#9-reporting-requirements)
10. [Approval](#10-approval)

---

## 1. Purpose and Scope

### 1.1 Purpose

This Security Assessment Plan establishes the scope, methodology, schedule, team, and rules of engagement for the annual security control assessment of the NEXUS Electronic Health Records System. The assessment will determine whether the 221 selected security and privacy controls are:

- **Implemented correctly** — the control exists and is in place
- **Operating as intended** — the control functions the way it was designed
- **Producing the desired outcome** — the control achieves its security objective

The findings will be documented in the Security Assessment Report (NEXUS-RMF-SAR-001), which the Authorising Official will use to make the ATO decision in Step 6.

### 1.2 Scope

**In scope — all components within the NEXUS system boundary:**

| Component | Assessment Focus |
|---|---|
| AWS Cloud Zone — Security Stack | WAF rules, Shield config, ALB TLS policy |
| AWS Cloud Zone — Web/App Servers (EC2) | Patch status, hardening, logging config |
| AWS Cloud Zone — S3 and Backup Vault | Encryption config, CMK policy, Object Lock, access control |
| On-Premises — Primary PostgreSQL DB | Encryption, access control, replication, backup |
| On-Premises — Secondary DB | Replication health, failover readiness |
| On-Premises — Audit Logging Server | Log completeness, integrity, access restriction |
| On-Premises — SIEM | Alert rules, coverage, response procedures |
| On-Premises — VPN Gateway | Configuration, certificate validity, logging |
| Clinical Endpoints — Workstations and Laptops | Patch status, EDR, disk encryption, GPO compliance |
| Clinical Endpoints — Nurses' Tablets | MDM enrollment, encryption, lock policy |
| Medical IoT Devices | Network segmentation, VLAN isolation, device inventory |
| Policies and Procedures | All NEXUS security policies — currency and completeness |
| Personnel | ISSO, SA, DBA, SOC Analyst, Privacy Officer — interviews |

**Out of scope:**
- AWS infrastructure below the hypervisor layer (AWS responsibility — verified via AWS SOC 2 Type II)
- Non-NEXUS hospital systems
- Physical security of non-data-centre hospital areas (assessed separately)

---

## 2. Assessor Independence

The assessment is conducted by an independent Security Control Assessor (SCA) team with no operational responsibility for NEXUS:

| Assessor | Organisation | Independence Basis |
|---|---|---|
| Lead SCA | [Third-Party Assessor Firm] | External firm — no NEXUS operational role |
| Technical Assessor (Cloud) | [Third-Party Assessor Firm] | External — no AWS access prior to assessment |
| Technical Assessor (On-Premises) | Internal Audit Team | Internal audit function — independent of IT operations |
| Penetration Tester | [Pen Test Firm] | External — first engagement with NEXUS environment |

**Independence declaration:** All assessors have signed an independence declaration confirming: no prior involvement in NEXUS control implementation, no conflicts of interest, and commitment to objective assessment. Declarations are retained with the SAP.

**ISSO role during assessment:** The ISSO facilitates access, provides documentation, and responds to SCA questions. The ISSO does not participate in assessment decisions or findings determinations.

---

## 3. Assessment Methodology

### 3.1 NIST SP 800-53A Rev 5 Assessment Methods

All controls will be assessed using one or more of the three methods defined in NIST SP 800-53A:

| Method | Definition | NEXUS Application |
|---|---|---|
| **Examine** | Review of relevant documentation, mechanisms, and activities | Policy documents, configuration exports, scan reports, log samples, architecture diagrams |
| **Interview** | Discussions with personnel responsible for implementing or using controls | ISSO, SA, DBA, SOC Analyst, Privacy Officer, clinical staff |
| **Test** | Exercise of mechanisms and activities to verify implementation and operation | Technical scans, configuration tests, penetration test, backup restoration, MFA challenge |

### 3.2 Assessment Determination Levels

Each control is assigned one of four determination levels per NIST SP 800-53A:

| Determination | Definition | SAR Notation |
|---|---|---|
| **Satisfied** | Control is implemented correctly, operating as intended, producing the desired outcome | ✅ SAT |
| **Other Than Satisfied — Low** | Minor deficiency; compensating control in place; low risk | 🟢 OTS-L |
| **Other Than Satisfied — Medium** | Moderate deficiency; partial implementation; medium risk | 🟡 OTS-M |
| **Other Than Satisfied — High** | Significant deficiency; control not implemented or not effective; high risk | 🟠 OTS-H |
| **Other Than Satisfied — Critical** | Control completely absent; catastrophic risk | 🔴 OTS-C |

### 3.3 Penetration Testing Approach

The annual penetration test (CA-8) is conducted as part of the Step 5 assessment:

| Test Type | Scope | Methodology |
|---|---|---|
| External penetration test | Internet-facing NEXUS components (ALB, WAF, patient portal) | OWASP Testing Guide v4; PTES |
| Internal penetration test | On-premises hospital network → NEXUS components | Assumed breach scenario |
| Web application test | NEXUS application — SQL injection, XSS, auth bypass | OWASP Top 10 |
| Social engineering (phishing simulation) | Clinical staff email phishing test | Targeted spear-phishing simulation |
| Wireless assessment | Hospital Wi-Fi access to NEXUS | WPA2 security assessment |

**Rules of engagement:** Penetration testing is conducted in a defined maintenance window with ISSO and AO written approval. No destructive testing. No exfiltration of real PHI. Production database is read-only during testing. ISSO has a kill switch to halt testing at any time.

---

## 4. Controls to Be Assessed

All 221 selected controls are assessed. The following table shows the assessment method(s) applied to each control family:

| Family | Controls | Examine | Interview | Test | Priority |
|---|---|---|---|---|---|
| AC — Access Control | 23 | ✅ | ✅ | ✅ | Critical |
| AT — Awareness and Training | 6 | ✅ | ✅ | — | High |
| AU — Audit and Accountability | 16 | ✅ | ✅ | ✅ | Critical |
| CA — Assessment and Monitoring | 9 | ✅ | ✅ | ✅ | Critical |
| CM — Configuration Management | 12 | ✅ | ✅ | ✅ | High |
| CP — Contingency Planning | 13 | ✅ | ✅ | ✅ | Critical |
| IA — Identification and Authentication | 13 | ✅ | ✅ | ✅ | Critical |
| IR — Incident Response | 10 | ✅ | ✅ | ✅ | Critical |
| MA — Maintenance | 6 | ✅ | ✅ | — | Moderate |
| MP — Media Protection | 8 | ✅ | ✅ | ✅ | High |
| PE — Physical and Environmental | 9 | ✅ | ✅ | ✅ | Moderate |
| PL — Planning | 4 | ✅ | — | — | Moderate |
| PM — Program Management | 9 | ✅ | ✅ | — | High |
| PS — Personnel Security | 9 | ✅ | ✅ | — | High |
| PT — PII Processing | 8 | ✅ | ✅ | — | Critical |
| RA — Risk Assessment | 10 | ✅ | ✅ | ✅ | Critical |
| SA — System Acquisition | 11 | ✅ | ✅ | — | High |
| SC — System and Comms Protection | 19 | ✅ | ✅ | ✅ | Critical |
| SI — System and Info Integrity | 18 | ✅ | ✅ | ✅ | Critical |
| SR — Supply Chain Risk | 8 | ✅ | ✅ | — | Moderate |

---

## 5. Assessment Schedule

| Phase | Activity | Duration | Participants |
|---|---|---|---|
| Phase 1 — Preparation | Document collection; SCA environment setup; SAP approval | Week 1 | SCA, ISSO |
| Phase 2 — Document Review (Examine) | Review all SSP sections, policies, procedures, prior scan reports, architecture | Weeks 2–3 | SCA team |
| Phase 3 — Interviews | ISSO, SA, DBA, SOC Analyst, Privacy Officer, clinical staff interviews | Week 4 | SCA, all named personnel |
| Phase 4 — Technical Testing | Configuration testing, scan review, backup test, MFA test | Weeks 5–6 | Technical assessors, SA, DBA |
| Phase 5 — Penetration Testing | External, internal, web application, phishing simulation | Week 7 | Pen test team, ISSO (standby) |
| Phase 6 — Analysis and Draft SAR | Findings analysis, draft SAR, ISSO review of factual accuracy | Week 8 | SCA, ISSO |
| Phase 7 — Final SAR Delivery | Final SAR and Findings Summary (Ref 6) delivered to AO | Week 9 | SCA → AO |

---

## 6. Assessment Team and Roles

| Role | Name | Organisation | Responsibility |
|---|---|---|---|
| Lead SCA | [Name] | [Firm] | Assessment lead; findings determination; SAR author |
| Cloud Technical Assessor | [Name] | [Firm] | AWS configuration testing; cloud control assessment |
| On-Premises Technical Assessor | [Name] | Internal Audit | On-premises server and endpoint assessment |
| Penetration Test Lead | [Name] | [Pen Test Firm] | External and internal penetration testing |
| NEXUS ISSO (Facilitator) | [Name] | Nexus Health System | Document provision; access facilitation; factual review |
| System Administrator (Interviewee) | [Name] | Nexus Health System | Technical interview subject |
| DBA (Interviewee) | [Name] | Nexus Health System | Database interview subject |
| SOC Manager (Interviewee) | [Name] | Nexus Health System | Incident response interview subject |
| Privacy Officer (Interviewee) | [Name] | Nexus Health System | Privacy control interview subject |

---

## 7. Information and Evidence Requirements

| Evidence Category | Documents / Artefacts Required | Provided By |
|---|---|---|
| System documentation | SSP, System Characterisation, Architecture Diagram, Data Inventory | ISSO |
| Policy documents | All NEXUS security policies (AC, AU, IR, CP, IA, etc.) | ISSO |
| Configuration exports | AWS Security Group rules, IAM policies, AD GPO exports, MDM profiles | SA |
| Scan reports | Last 3 months of Nessus and AWS Inspector reports | ISSO / SA |
| Access review records | Last 2 quarterly access review reports | ISSO |
| Backup and recovery | Last 2 quarterly restoration test reports | DBA |
| Training records | LMS completion report — all NEXUS users — last 12 months | HR / ISSO |
| Incident response | IR tabletop exercise report; any actual incident reports (last 12 months) | ISSO / SOC |
| Audit log samples | 30-day sample of audit logs (anonymised for PHI) | ISSO |
| SIEM configuration | SIEM alert rule export | SOC |
| BAA register | List of all BAAs with status and last review date | ISSO / Privacy Officer |
| Penetration test history | Prior pen test results (if any) | ISSO |

---

## 8. Rules of Engagement

| Rule | Detail |
|---|---|
| PHI protection | No real PHI to be accessed or extracted during assessment; test data used for application testing |
| Production safety | No changes to production systems during assessment without written ISSO approval |
| Testing window | Technical testing and penetration testing: 22:00–06:00 to minimise clinical impact |
| Kill switch | ISSO may halt any assessment activity immediately if patient safety is at risk |
| Confidentiality | All assessment findings are confidential; not to be disclosed outside the NEXUS ATO package |
| Vulnerability disclosure | Any critical finding discovered during penetration test → notified to ISSO within 1 hour |
| Evidence handling | All evidence collected digitally; encrypted at rest; destroyed after SAR delivery |
| No social engineering of patients | Phishing simulation targets only staff — not patients or patient portal users |

---

## 9. Reporting Requirements

| Report | Recipient | Timeline |
|---|---|---|
| Weekly status update | ISSO | Every Friday during assessment |
| Critical finding notification | ISSO + AO | Within 1 hour of discovery |
| Draft SAR (factual review) | ISSO | End of Week 8 |
| Final SAR | AO, ISSO, System Owner | End of Week 9 |
| SAR Findings Summary (Ref 6) | AO | Delivered with Final SAR |
| Penetration test detailed report | ISSO (only) | Within 5 days of pen test completion |

---

## 10. Approval

| Role | Name | Signature | Date |
|---|---|---|---|
| Lead SCA | [Name] | _________________________ | 2025 |
| ISSO | [Name] | _________________________ | 2025 |
| System Owner | [Name] | _________________________ | 2025 |
| **Authorising Official** | **[Name]** | _________________________ | **2025** |

---

*Document Reference: NEXUS-RMF-SAP-001 | Version 1.0 | Classification: Internal — Controlled*
