# System Security Plan — Draft
### NEXUS Electronic Health Records System | Step 2 — Categorise

| Field | Value |
|---|---|
| **Document Type** | System Security Plan (SSP) — Draft |
| **System Name** | NEXUS Electronic Health Records System |
| **Version** | 0.1 — Draft (updated with each RMF step) |
| **Classification** | Internal — Controlled |
| **Prepared By** | ISSO |
| **Date** | 2025 |
| **Status** | Draft — Sections 1–4 complete; Sections 5–9 pending Steps 3 and 4 |

> **Note:** The SSP is a living document. This draft is initiated at Step 2 and updated progressively through Steps 3 (control selection), 4 (implementation), and finalised before the Step 5 assessment. The completed SSP is located in [04-implement/ssp-final.md](../04-implement/ssp-final.md).

---

## Section 1 — System Identification

| Attribute | Value |
|---|---|
| System Name | NEXUS Electronic Health Records System |
| System Abbreviation | NEXUS EHR |
| System Owner | [Name], Director of Clinical Informatics |
| Authorising Official | [Name], Chief Information Officer |
| ISSO | [Name], Lead Information Security Analyst |
| Assignment | Production — Operational |
| System Type | Major Application |
| Deployment | Hybrid (AWS Cloud + On-Premises) |
| FIPS 199 Impact Level | HIGH |
| Control Baseline | NIST SP 800-53 Rev 5 — HIGH |
| Operational Status | Operational |
| Date of Last Review | 2025 |

---

## Section 2 — System Description

NEXUS Electronic Health Records System is a hybrid EHR platform designed to support comprehensive day-to-day healthcare operations across multi-site clinical environments. The system enables healthcare providers to manage patient records, lab results, referrals, appointments, billing, and clinical documentation in a secure and centralised environment.

NEXUS processes, stores, and transmits sensitive health information including Protected Health Information (PHI) and Personally Identifiable Information (PII). The system serves approximately 2,000 daily active clinical and administrative users, 100,000 registered patient portal users, and integrates with medical IoT devices at the point of care.

See [01-prepare/system-characterisation.md](../01-prepare/system-characterisation.md) for the full system characterisation, including architecture overview, interconnections, and user types.

---

## Section 3 — System Environment

### 3.1 Architecture Zones

| Zone | Components | Managed By |
|---|---|---|
| Internet Zone | External users, internet gateway | N/A (untrusted) |
| AWS Cloud Zone — Security Stack | AWS Shield, AWS WAF, Application Load Balancer | Nexus IS Team + AWS |
| AWS Cloud Zone — Public Subnet | Web/App Server 1, Web/App Server 2 | Nexus IS Team |
| AWS Cloud Zone — Private Subnet | AWS Backup Vault, Amazon S3 | Nexus IS Team + AWS |
| On-Premises — Data Tier | Primary PostgreSQL DB, Secondary Failover DB | Nexus DBA Team |
| On-Premises — Security and Audit | Audit Logging Server, SIEM Monitoring Server | Nexus SOC |
| On-Premises — Hospital Endpoints | Admin workstations, clinician laptops, nurses' tablets, medical IoT devices | Nexus IT Team |

### 3.2 Network Connections

All external connections to NEXUS traverse HTTPS on Port 443 with TLS 1.2 minimum. The AWS Cloud Zone and On-Premises Hospital Zone are connected exclusively via an IPSec VPN tunnel with certificate-based mutual authentication. No unencrypted network paths are permitted.

See [02-categorise/data-inventory.md](./data-inventory.md) Section 7 for the full encryption-in-transit summary.

---

## Section 4 — Security Categorisation

This section documents the FIPS 199 security categorisation result for NEXUS.

### 4.1 Categorisation Result

```
SC NEXUS = {(Confidentiality, HIGH), (Integrity, HIGH), (Availability, HIGH)}

Overall System Impact Level: HIGH
```

### 4.2 Summary Justification

| Objective | Level | One-line Justification |
|---|---|---|
| Confidentiality | HIGH | Unauthorised disclosure of PHI/PII causes regulatory penalty, patient harm, and loss of trust |
| Integrity | HIGH | Corrupted clinical data directly threatens patient safety at the point of care |
| Availability | HIGH | System downtime disrupts active clinical care across all sites simultaneously |

See [02-categorise/fips199-worksheet.md](./fips199-worksheet.md) for the full categorisation analysis.

---

## Section 5 — Security Controls (Pending — Step 3)

> This section will be completed in Step 3 following control selection and tailoring.
> See [03-select/control-selection-worksheet.md](../03-select/control-selection-worksheet.md)

---

## Section 6 — Control Implementation Statements (Pending — Step 4)

> This section will be completed in Step 4 following control implementation.
> See [04-implement/control-implementation-statements.md](../04-implement/control-implementation-statements.md)

---

## Section 7 — Interconnection Agreements (Summary)

| Connected System | Agreement Type | Status |
|---|---|---|
| Amazon Web Services | Business Associate Agreement (BAA) + Shared Responsibility Model | Signed |
| External laboratory systems | Business Associate Agreement (BAA) | Signed |
| Insurance company billing interfaces | Business Associate Agreement (BAA) | Signed |
| External referring providers | Business Associate Agreement (BAA) | Signed |
| IT support vendors | Confidentiality / Non-Disclosure Agreement | Signed |

---

## Section 8 — Laws, Regulations, and Policies

| Requirement | Source |
|---|---|
| PHI protection — administrative, physical, technical safeguards | HIPAA Security Rule, 45 CFR Part 164 Subpart C |
| PHI use and disclosure | HIPAA Privacy Rule, 45 CFR Part 164 Subparts A, E |
| Breach notification | HIPAA Breach Notification Rule; HITECH Act |
| Security controls | NIST SP 800-53 Rev 5 |
| RMF process | NIST SP 800-37 Rev 2 |
| Minimum security requirements | FIPS 200 |
| Categorisation | FIPS 199; NIST SP 800-60 |

---

## Section 9 — Plan of Action and Milestones (Pending — Step 6)

> The POA&M will be initiated following the security assessment in Step 5.
> See [06-authorise/poam.md](../06-authorise/poam.md)

---

## Document Control

| Version | Date | Author | Change Description |
|---|---|---|---|
| 0.1 | 2025 | ISSO | Initial draft — Sections 1–4 complete (Steps 1 and 2) |
| 0.2 | TBD | ISSO | Add Section 5 — Control Selection (Step 3) |
| 0.3 | TBD | ISSO | Add Section 6 — Implementation Statements (Step 4) |
| 1.0 | TBD | ISSO | Final SSP — all sections complete; submitted for assessment |

---

*Document Owner: ISSO | Approved by: AO | Classification: Internal — Controlled*
