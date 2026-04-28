# FIPS 199 System Categorisation
## NEXUS Electronic Health Records System

---

| Field | Detail |
|---|---|
| **Document Reference** | NEXUS-RMF-CAT-001 |
| **Document Type** | System Categorisation — FIPS 199 |
| **System Name** | NEXUS Electronic Health Records System |
| **System Abbreviation** | NEXUS EHR |
| **Version** | 1.0 |
| **Classification** | Internal — Controlled |
| **Prepared By** | Chioma Otthe, Lead Information Security Analyst |
| **Reviewed By** | Jack Taylor, Director of Clinical Informatics |
| **Approved By** | Ben jackson, Chief Information Officer |
| **Date** | 2026 |
| **References** | FIPS Publication 199 · NIST SP 800-60 Vol 1 Rev 1 · NIST SP 800-60 Vol 2 Rev 1 · NIST SP 800-37 Rev 2 · HIPAA Security Rule 45 CFR Part 164 |

---

## Table of Contents

1. [Purpose and Scope](#1-purpose-and-scope)
2. [System Overview](#2-system-overview)
3. [FIPS 199 Framework Summary](#3-fips-199-framework-summary)
4. [Information Types Inventory — NIST SP 800-60](#4-information-types-inventory--nist-sp-800-60)
5. [FIPS 199 Categorisation Table](#5-fips-199-categorisation-table)
6. [Security Objective Analysis](#6-security-objective-analysis)
7. [Overall System Categorisation Result](#7-overall-system-categorisation-result)
8. [Implications of HIGH Categorisation](#8-implications-of-high-categorisation)
9. [Relationship to HIPAA Security Rule](#9-relationship-to-hipaa-security-rule)
10. [Approval and Sign-off](#10-approval-and-sign-off)


---

## 1. Purpose and Scope

### 1.1 Purpose

This document establishes the formal security categorisation of the NEXUS Electronic Health Records System in accordance with:

- **FIPS Publication 199** — *Standards for Security Categorisation of Federal Information and Information Systems*
- **NIST SP 800-60 Volume 1, Rev 1** — *Guide for Mapping Types of Information and Information Systems to Security Categories*
- **NIST SP 800-60 Volume 2, Rev 1** — *Appendices to Guide for Mapping Types of Information and Information Systems to Security Categories*
- **NIST SP 800-37 Rev 2** — *Risk Management Framework for Information Systems and Organisations*

The categorisation result determines the security impact level of NEXUS and directly drives the selection of the appropriate NIST SP 800-53 Rev 5 control baseline in RMF Step 3.

### 1.2 Scope

This categorisation covers **all components** of the NEXUS system boundary as defined in the System Characterisation document (NEXUS-RMF-PREP-001), including:

- AWS Cloud Zone (Security Stack, Public Subnet, Private Subnet)
- On-Premises Hospital Zone (Data Tier, Security & Audit, Hospital Endpoints)
- All data processed, stored, and transmitted across the hybrid environment
- All interconnections between zones (VPN tunnel, HTTPS, internal LAN)

### 1.3 System Description

NEXUS is a hybrid Electronic Health Records (EHR) System designed to support comprehensive day-to-day healthcare operations across multi-site clinical environments. The system enables healthcare providers to manage:

- Patient health records and clinical documentation
- Laboratory results, referrals, and appointments
- Billing, revenue cycle, and administrative workflows
- Medication management and prescriptions
- Medical IoT device integration for vital signs capture

NEXUS processes, stores, and transmits **Protected Health Information (PHI)** and **Personally Identifiable Information (PII)** for an estimated 500,000+ active patient records, serving approximately 2,000 daily clinical and administrative users across all hospital sites. Security and compliance with HIPAA, HITECH, and applicable federal and state health information laws are a critical priority.

---

## 2. System Overview

### 2.1 Architecture Summary

| Zone | Key Components | Data Handled |
|---|---|---|
| **Internet Zone** | External users, patients, internet gateway | HTTPS traffic only — no PHI stored |
| **AWS — Security Stack** | AWS Shield, AWS WAF, Application Load Balancer | Filtered/inspected traffic |
| **AWS — Public Subnet** | Web/App Server 1 & 2 (redundant) | Application logic, session data |
| **AWS — Private Subnet** | AWS Backup Vault, Amazon S3 | Encrypted PHI backups |
| **On-Premises — Data Tier** | Primary PostgreSQL DB, Secondary Failover DB | All PHI/PII at rest (primary store) |
| **On-Premises — Security & Audit** | Audit Logging Server, SIEM Monitoring Server | Audit logs, telemetry |
| **On-Premises — Endpoints** | Admin workstations, clinician laptops, nurses' tablets, medical IoT devices | PHI access at point of care |

### 2.2 Connectivity

| Connection | Protocol | Security Control |
|---|---|---|
| External users → AWS | HTTPS / TLS 1.2+ | AWS Shield, WAF, ALB, Firewall/SG |
| AWS Cloud ↔ On-Premises | IPSec VPN | AES-256, certificate-based mutual auth |
| Primary DB ↔ Secondary DB | PostgreSQL SSL replication | TLS 1.2+, encrypted channel |
| SIEM ↔ All components | Syslog / TLS | Read-only audit credentials |
| IoT Devices → Hospital LAN | Encrypted proprietary protocol | Device certificates, network segmentation |

---

## 3. FIPS 199 Framework Summary

### 3.1 Security Objectives

FIPS 199 evaluates information systems against three security objectives:

| Security Objective | FIPS 199 Definition |
|---|---|
| **Confidentiality** | Preserving authorised restrictions on information access and disclosure, including means for protecting personal privacy and proprietary information |
| **Integrity** | Guarding against improper information modification or destruction, and ensuring information non-repudiation and authenticity |
| **Availability** | Ensuring timely and reliable access to and use of information and the information system |

### 3.2 Impact Level Definitions

| Impact Level | Definition | Adverse Effect Description |
|---|---|---|
| **LOW** | Limited adverse effect | Minor degradation in mission capability; minor financial loss; minor harm to individuals |
| **MODERATE** | Serious adverse effect | Significant degradation in mission capability; significant financial loss; significant harm to individuals that does not involve loss of life or serious injury |
| **HIGH** | Severe or catastrophic adverse effect | Severe degradation or loss of mission capability; major financial loss; severe or catastrophic harm to individuals involving loss of life or serious life-threatening injuries |

### 3.3 High-Water Mark Principle

Per FIPS 199, the overall system categorisation is determined by the **highest impact level** assigned across all information types for each security objective. The system's overall impact level is the highest of all three objectives.

```
SC System = {(Confidentiality, impact), (Integrity, impact), (Availability, impact)}
Overall Impact = MAX(Confidentiality, Integrity, Availability)
```

---

## 4. Information Types Inventory — NIST SP 800-60

The following information types processed by NEXUS have been identified and mapped to NIST SP 800-60 Vol 2 identifiers. Default impact levels are drawn from SP 800-60 Appendices and adjusted where the NEXUS operational context creates higher potential impact than the default contemplates.

### 4.1 Information Type Mapping Table

| # | Information Type | SP 800-60 ID | Default C | Default I | Default A | NEXUS C | NEXUS I | NEXUS A | Adjusted? |
|---|---|---|---|---|---|---|---|---|---|
| 1 | Health Care Delivery Services | C.2.8.1 | Moderate | Moderate | Moderate | **High** | **High** | **High** | Yes — See §4.2 |
| 2 | Patient Health Records (PHI) | C.2.8.1 / D.14 | Moderate | Moderate | Low | **High** | **High** | **High** | Yes — See §4.2 |
| 3 | Patient Identity / PII | D.14 | Moderate | Moderate | Low | **High** | **High** | **High** | Yes — See §4.2 |
| 4 | Billing and Financial Records | D.12 | Moderate | Moderate | Low | **High** | **High** | Moderate | Yes — C/I adjusted |
| 5 | Laboratory Results | C.2.8.1 | Moderate | High | Moderate | **High** | **High** | **High** | Yes — C adjusted |
| 6 | Prescriptions and Medications | C.2.8.1 | Moderate | High | Moderate | **High** | **High** | **High** | Yes — C adjusted |
| 7 | Medical Device / IoT Data | C.2.8.1 | Moderate | Moderate | Moderate | **High** | **High** | **High** | Yes — all adjusted |
| 8 | Referrals and Appointments | C.2.8.1 | Low | Moderate | Moderate | Moderate | **High** | **High** | Yes — I/A adjusted |
| 9 | Clinical Documentation / Notes | C.2.8.1 | Moderate | High | Moderate | **High** | **High** | **High** | Yes — C adjusted |
| 10 | Medication Administration Records | C.2.8.1 | Moderate | High | Moderate | **High** | **High** | **High** | Yes — C/A adjusted |
| 11 | Audit and Accountability Records | D.20 | Moderate | High | Moderate | **High** | **High** | Moderate | Yes — C adjusted |
| 12 | System / Application Configuration | D.21 | Moderate | High | Moderate | Moderate | **High** | Moderate | No change |
| 13 | Patient Consent Records | C.2.8.1 | Moderate | Moderate | Low | **High** | **High** | Moderate | Yes — C/I adjusted |
| 14 | Insurance / Benefits Information | D.12 | Moderate | Moderate | Low | **High** | **High** | Moderate | Yes — C/I adjusted |
| 15 | Vital Signs (real-time IoT feed) | C.2.8.1 | Moderate | High | High | **High** | **High** | **High** | Yes — C adjusted |

**C = Confidentiality · I = Integrity · A = Availability**

### 4.2 Adjustment Justifications

All upward adjustments from SP 800-60 default levels are justified on the following grounds:

**Confidentiality adjustments (Moderate → High):**
NEXUS operates in a regulated healthcare environment where any unauthorised disclosure of PHI constitutes a HIPAA breach. The consequences — regulatory penalties up to $1.9M per violation category, criminal liability, direct patient harm through stigmatisation or discrimination, and irreversible reputational damage — meet the FIPS 199 definition of "severe or catastrophic" at the organisational and individual level. The multi-site, centralised nature of NEXUS means a single breach has the potential to affect hundreds of thousands of patients simultaneously.

**Integrity adjustments (Moderate → High for clinical data):**
NEXUS data is used at the point of clinical care. Corrupted, altered, or deleted clinical records — including diagnoses, allergy records, prescriptions, lab results, and vital signs — can directly cause patient harm, misdiagnosis, or medication errors. This meets the FIPS 199 threshold of "severe or catastrophic harm to individuals involving loss of life or serious life-threatening injuries."

**Availability adjustments (Low/Moderate → High for clinical data):**
NEXUS supports active, real-time clinical care across all hospital sites. A centralised system outage simultaneously affects all sites with no viable short-term manual alternative at operational scale (~50,000 transactions/day). Unavailability during an active clinical shift — particularly in emergency, surgical, or ICU contexts — constitutes a direct patient safety risk.

---

## 5. FIPS 199 Categorisation Table

This is the formal FIPS 199 categorisation table for NEXUS, as required by Reference 2 of the system categorisation requirement.

### 5.1 FIPS 199 Categorisation Table — NEXUS EHR

| Security Objective | Information Type | SP 800-60 Default | NEXUS Adjusted Level | Justification Summary |
|---|---|---|---|---|
| **CONFIDENTIALITY** | Patient Health Records (PHI) | Moderate | **HIGH** | HIPAA breach liability; patient privacy harm; mass exposure risk |
| **CONFIDENTIALITY** | Patient Identity (PII) | Moderate | **HIGH** | Identity theft; insurance fraud; patient dignity |
| **CONFIDENTIALITY** | Lab Results | Moderate | **HIGH** | Sensitive diagnoses (HIV, cancer, mental health) — stigma and discrimination risk |
| **CONFIDENTIALITY** | Prescriptions / Medications | Moderate | **HIGH** | Controlled substance records; sensitive condition indicators |
| **CONFIDENTIALITY** | Clinical Notes | Moderate | **HIGH** | Contains full narrative PHI — most sensitive record type |
| **CONFIDENTIALITY** | Billing Records | Moderate | **HIGH** | PHI embedded in billing codes (diagnosis, procedure) |
| **CONFIDENTIALITY** | Audit Logs | Moderate | **HIGH** | Contain access metadata; exposure reveals system architecture |
| **CONFIDENTIALITY** | Vital Signs | Moderate | **HIGH** | Real-time patient data; condition-identifying |
| | | | | |
| **INTEGRITY** | Patient Health Records (PHI) | Moderate | **HIGH** | Altered records → wrong clinical decisions → patient harm or death |
| **INTEGRITY** | Lab Results | High | **HIGH** | Falsified results → misdiagnosis; incorrect treatment |
| **INTEGRITY** | Prescriptions / Medications | High | **HIGH** | Altered dosage or drug → medication error; overdose risk |
| **INTEGRITY** | Medication Admin Records (MAR) | High | **HIGH** | Tampered MAR → administration of wrong medication |
| **INTEGRITY** | Vital Signs | High | **HIGH** | Falsified vitals → missed deterioration; treatment failure |
| **INTEGRITY** | Clinical Notes | High | **HIGH** | Altered notes → incorrect care plan; legal liability |
| **INTEGRITY** | Audit Logs | High | **HIGH** | Tampered logs → inability to detect breach; HIPAA violation |
| **INTEGRITY** | System Configuration | High | **HIGH** | Altered config → unauthorised access; security bypass |
| | | | | |
| **AVAILABILITY** | Patient Health Records (PHI) | Low | **HIGH** | Real-time clinical dependency; no viable manual alternative at scale |
| **AVAILABILITY** | Lab Results | Moderate | **HIGH** | Delayed results → delayed diagnosis; treatment decisions blocked |
| **AVAILABILITY** | Prescriptions / Medications | Moderate | **HIGH** | Unavailable records → missed doses; prescribing errors |
| **AVAILABILITY** | Vital Signs | High | **HIGH** | Real-time monitoring — unavailability = undetected patient deterioration |
| **AVAILABILITY** | Clinical Notes | Moderate | **HIGH** | Clinicians cannot access care history; treatment continuity broken |
| **AVAILABILITY** | Referrals / Appointments | Moderate | **HIGH** | Multi-site scheduling collapse; care coordination failure |
| **AVAILABILITY** | Health Care Delivery Services | Moderate | **HIGH** | System-wide outage affects all clinical operations simultaneously |

### 5.2 Consolidated Impact by Security Objective

| Security Objective | Highest Applicable Level | Determined From |
|---|---|---|
| **Confidentiality** | **HIGH** | PHI/PII — HIPAA breach liability; patient harm; multi-site mass exposure |
| **Integrity** | **HIGH** | Clinical data — patient safety at point of care; audit trail requirements |
| **Availability** | **HIGH** | Active clinical care dependency; real-time patient monitoring; no short-term manual fallback |

---

## 6. Security Objective Analysis

### 6.1 Confidentiality — HIGH

**Scenario: Unauthorised disclosure of NEXUS data**

A confidentiality breach affecting NEXUS would have **severe or catastrophic** adverse effects for the following reasons:

**Regulatory consequences:**
The Health Insurance Portability and Accountability Act (HIPAA) and the HITECH Act impose civil monetary penalties of $100–$50,000 per violation, up to $1,919,173 per violation category per year. Criminal penalties under 42 U.S.C. §1320d-6 can result in imprisonment of up to 10 years. A breach affecting a centralised EHR serving 500,000+ patients would place Nexus Health System in the highest penalty tier.

**Patient-level harm:**
- Disclosure of diagnoses (HIV status, mental health conditions, substance use disorders, cancer) causes stigmatisation, employment discrimination, insurance discrimination, and psychological harm
- Disclosure of PII (SSN, DOB, address, insurance ID) enables identity theft and healthcare fraud — PHI-based identity theft is among the most damaging forms because it corrupts medical records and insurance histories
- Patients may avoid seeking care if they lose confidence that their records are private — a public health harm beyond the individual

**Organisational consequences:**
- Irreversible reputational damage; loss of patient trust at a community health level
- Regulatory investigation; potential suspension of operating authority
- Class-action litigation from affected patients
- Mandatory public breach notification to all affected individuals and HHS

**FIPS 199 Determination:** The potential for HIPAA criminal penalties, direct patient harm, and catastrophic reputational consequences meets the **HIGH** impact threshold.

---

### 6.2 Integrity — HIGH

**Scenario: Unauthorised modification or destruction of NEXUS data**

An integrity breach affecting NEXUS would have **severe or catastrophic** adverse effects for the following reasons:

**Direct patient safety risk:**
NEXUS is used at the active point of clinical care. Clinical staff rely on NEXUS data to make life-affecting decisions in real time:
- A falsified allergy record could cause a clinician to administer a drug the patient is allergic to
- An altered medication dosage in the MAR could result in overdose or under-treatment
- A manipulated lab result could lead to a delayed cancer diagnosis or incorrect surgical decision
- Corrupted vital signs data from IoT integration could mask patient deterioration in an ICU

Any of these outcomes can directly cause death or serious physical harm to patients — the highest possible individual-level consequence under FIPS 199.

**Legal and regulatory integrity:**
Clinical documentation carries medico-legal weight. Tampered or destroyed records:
- Eliminate the organisation's ability to defend against malpractice claims
- Constitute a federal offence under 18 U.S.C. §1519 (destruction of records)
- Violate HIPAA audit control requirements (45 CFR §164.312(b))
- Invalidate all audit evidence needed for breach investigation and regulatory response

**Cascading replication effect:**
NEXUS uses real-time PostgreSQL streaming replication between the primary and secondary database. A corrupted record propagated to the secondary server simultaneously affects all clinical sites — there is no clean copy to restore from without activating full backup recovery.

**FIPS 199 Determination:** The potential for direct patient harm including death, cascading data corruption, and destruction of the legal record base meets the **HIGH** impact threshold.

---

### 6.3 Availability — HIGH

**Scenario: Disruption of access to NEXUS**

An availability failure affecting NEXUS would have **severe or catastrophic** adverse effects for the following reasons:

**Active clinical care dependency:**
Clinical staff across all hospital sites use NEXUS as the primary system of record for patient care. During a system outage, clinicians cannot access:
- Current medication lists (medication errors become likely)
- Patient allergy records (anaphylaxis risk)
- Lab results and diagnostic imaging orders
- Active care plans and discharge instructions
- Emergency patient history

**No viable manual alternative at scale:**
While paper-based downtime procedures exist, they are not sustainable at the volume NEXUS supports (~50,000 daily transactions across multiple sites). Extended downtime creates documentation backlogs, increases error rates, and degrades care quality system-wide.

**Emergency and time-critical care:**
NEXUS supports emergency department workflows, surgical scheduling, ICU monitoring, and real-time vital signs integration. A system outage during an active emergency or surgical procedure — where patient history, allergy records, and medication data must be instantly accessible — constitutes a direct patient safety event.

**Multi-site simultaneous impact:**
Because NEXUS is centralised, a single availability failure affects all clinical sites simultaneously. There is no fallback to a local site-level system.

**Recovery complexity:**
Restoring NEXUS requires coordinated recovery across the hybrid AWS and on-premises environment — a complex, time-consuming process that extends the impact duration.

**FIPS 199 Determination:** The potential for direct patient harm across all sites, with no viable short-term manual fallback, meets the **HIGH** impact threshold.

---

## 7. Overall System Categorisation Result

### 7.1 Final Categorisation

Applying the **high-water mark principle** as defined in FIPS 199:

```
┌─────────────────────────────────────────────────────────────────────┐
│                                                                     │
│   SC NEXUS EHR =                                                    │
│   {(Confidentiality, HIGH), (Integrity, HIGH), (Availability, HIGH)}│
│                                                                     │
│   ══════════════════════════════════════════                        │
│   OVERALL SYSTEM IMPACT LEVEL:  H I G H                            │
│   ══════════════════════════════════════════                        │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

### 7.2 Categorisation Summary Card

| Attribute | Value |
|---|---|
| **System Name** | NEXUS Electronic Health Records System |
| **System Type** | Hybrid Major Application |
| **Confidentiality Impact** | 🔴 HIGH |
| **Integrity Impact** | 🔴 HIGH |
| **Availability Impact** | 🔴 HIGH |
| **Overall Impact Level** | 🔴 **HIGH** |
| **Applicable Control Baseline** | NIST SP 800-53 Rev 5 — HIGH Baseline |
| **Categorisation Authority** | FIPS 199; NIST SP 800-60 Vol 1 & 2 |
| **Date of Categorisation** | 2025 |
| **Next Review Date** | 2026 (or upon significant system change) |

### 7.3 Categorisation Decision Rationale

All three security objectives independently reach the HIGH impact level without reliance on the high-water mark rule. This is one of the strongest possible categorisation outcomes and reflects the clinical criticality of NEXUS:

| Objective | Could it be MODERATE? | Why not |
|---|---|---|
| Confidentiality | No | HIPAA criminal penalties + mass PHI exposure = catastrophic at any scale |
| Integrity | No | Clinical data integrity failures can directly cause patient death |
| Availability | No | Real-time active clinical care has no adequate manual fallback at operational scale |

---

## 8. Implications of HIGH Categorisation

| Implication | Requirement | NEXUS Impact |
|---|---|---|
| **Control Baseline** | NIST SP 800-53 Rev 5 HIGH baseline (all 20 control families) | Maximum control set applied |
| **Assessment Frequency** | Annual security assessment minimum; continuous monitoring required | Annual SCA assessment + daily/weekly monitoring |
| **Authorisation Type** | Full ATO required; granted by AO | CIO as AO; formal ATO decision |
| **POA&M Management** | All HIGH/Critical findings tracked with 30-day remediation | Monthly ISSO POA&M review |
| **Incident Response** | HIGH-severity IR plan; 24/7 SOC coverage required | SOC Manager on-call; 60-day breach notification |
| **Penetration Testing** | Strongly recommended annually in addition to vulnerability scanning | Annual third-party pen test |
| **Backup and Recovery** | RTO/RPO must reflect clinical care dependency | RTO < 4 hours; RPO < 1 hour |
| **Supply Chain Risk** | All third-party components and integrations must be assessed | BAA required for all PHI-handling vendors |
| **Vulnerability Scanning** | Weekly minimum; critical patches within 30 days | AWS Inspector + Nessus weekly scans |
| **Access Control** | Least privilege; MFA required for all privileged and remote access | RBAC + MFA enforced across all user types |

---

## 9. Relationship to HIPAA Security Rule

The FIPS 199 HIGH categorisation aligns directly with HIPAA Security Rule requirements for a covered entity processing ePHI. The table below maps the categorisation to applicable HIPAA standards:

| FIPS 199 Objective | HIPAA Standard | 45 CFR Reference | Required Safeguard |
|---|---|---|---|
| Confidentiality | Access Control | §164.312(a)(1) | Unique user IDs; automatic logoff; encryption |
| Confidentiality | Transmission Security | §164.312(e)(1) | Encryption of ePHI in transit (TLS 1.2+) |
| Confidentiality | Workforce Training | §164.308(a)(5) | Security awareness; PHI handling |
| Integrity | Audit Controls | §164.312(b) | Activity logs for all PHI access events |
| Integrity | Integrity Controls | §164.312(c)(1) | Electronic mechanisms to corroborate data is not altered |
| Integrity | Authentication | §164.312(d) | Verify person/entity seeking ePHI access |
| Availability | Contingency Planning | §164.308(a)(7) | Data backup; disaster recovery; emergency mode |
| Availability | Facility Access Controls | §164.310(a)(1) | Physical access to systems housing ePHI |
| All | Risk Analysis | §164.308(a)(1)(ii)(A) | Accurate and thorough assessment of risks |
| All | Risk Management | §164.308(a)(1)(ii)(B) | Implement measures to reduce risks to reasonable level |

> **Key point for portfolio:** The FIPS 199 HIGH categorisation is not just an RMF exercise for NEXUS — it is the mechanism through which the organisation formally acknowledges its HIPAA obligations and determines the appropriate level of safeguards. A Moderate categorisation for a system handling PHI at this scale would be a compliance gap.

---

## 10. Approval and Sign-off

This categorisation has been reviewed and approved by the following authorised individuals:

| Role | Name | Title | Signature | Date |
|---|---|---|---|---|
| Prepared By | [ISSO Name] | Lead Information Security Analyst | _________________________ | 2026 |
| Reviewed By | [System Owner Name] | Director of Clinical Informatics | _________________________ | 2026 |
| Reviewed By | [ISSM Name] | Deputy Chief Information Security Officer | _________________________ | 2026|
| Reviewed By | [Privacy Officer Name] | Chief Privacy Officer | _________________________ | 2026|
| **Approved By** | **[AO Name]** | **Chief Information Officer (Authorising Official)** | _________________________ | **2026** |

### Review Schedule

| Trigger | Action Required |
|---|---|
| Annually | Full categorisation review — assess whether impact levels remain accurate |
| Significant system change | Re-evaluate affected information types within 30 days |
| Regulatory change (HIPAA/HITECH) | Immediate review of confidentiality impact level |
| New information type introduced | Add to SP 800-60 mapping table and re-evaluate overall level |
| Security incident | Post-incident review of affected security objective |

---

## 
