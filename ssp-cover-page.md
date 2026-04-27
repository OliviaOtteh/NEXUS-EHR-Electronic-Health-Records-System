# SYSTEM SECURITY PLAN
# NEXUS Electronic Health Records System

---

```
╔══════════════════════════════════════════════════════════════════════════════╗
║                                                                              ║
║              SYSTEM SECURITY PLAN (SSP)                                      ║
║                                                                              ║
║              NEXUS ELECTRONIC HEALTH RECORDS SYSTEM                          ║
║                                                                              ║
║              NEXUS-RMF-SSP-001                                               ║
║                                                                              ║
╚══════════════════════════════════════════════════════════════════════════════╝
```

---

## COVER PAGE — REFERENCE 4

| Field | Detail |
|---|---|
| **Document Title** | System Security Plan (SSP) |
| **Document Reference** | NEXUS-RMF-SSP-001 |
| **System Name** | NEXUS Electronic Health Records System |
| **System Abbreviation** | NEXUS EHR |
| **Version** | 1.0 — Final |
| **Document Status** | Final — Submitted for Assessment |
| **Classification** | Internal — Controlled |
| **Date Prepared** | 2025 |
| **Date Submitted** | 2025 |
| **Next Review Date** | 2026 (Annual) or upon significant system change |

---

## System Identification

| Attribute | Value |
|---|---|
| **System Name** | NEXUS Electronic Health Records System |
| **System Abbreviation** | NEXUS EHR |
| **System Owner** | [Name], Director of Clinical Informatics, Nexus Health System |
| **Authorising Official (AO)** | [Name], Chief Information Officer, Nexus Health System |
| **Information System Security Officer (ISSO)** | [Name], Lead Information Security Analyst |
| **Information System Security Manager (ISSM)** | [Name], Deputy Chief Information Security Officer |
| **Privacy Officer** | [Name], Chief Privacy Officer |
| **System Administrator** | [Name], IT Infrastructure Lead |
| **Database Administrator** | [Name], Senior Database Administrator |
| **Operational Status** | Operational |
| **System Type** | Major Application |
| **Deployment Model** | Hybrid — AWS Cloud + On-Premises Hospital Infrastructure |
| **Operating Environment** | Multi-site clinical hospital network |
| **FIPS 199 Impact Level** | HIGH — Confidentiality: HIGH, Integrity: HIGH, Availability: HIGH |
| **Control Baseline** | NIST SP 800-53 Rev 5 — HIGH Impact Baseline |
| **ATO Status** | Pending — Awaiting Step 5 Assessment |
| **System Location (Cloud)** | AWS us-east-1 (Primary); AWS us-east-2 (Backup) |
| **System Location (On-Premises)** | Hospital Data Centre — Site A (Primary); Site B (Secondary) |

---

## Applicable Laws, Regulations, and Standards

| Regulation / Standard | Version / Reference | Applicability |
|---|---|---|
| NIST SP 800-37 | Rev 2 | RMF process — all 7 steps |
| NIST SP 800-53 | Rev 5 | Security and privacy controls — HIGH baseline |
| NIST SP 800-60 | Vol 1 & 2, Rev 1 | Information type categorisation |
| FIPS 199 | Current | Security categorisation |
| FIPS 200 | Current | Minimum security requirements |
| HIPAA Security Rule | 45 CFR Part 164, Subpart C | ePHI protection — administrative, physical, technical safeguards |
| HIPAA Privacy Rule | 45 CFR Part 164, Subparts A & E | PHI use and disclosure |
| HIPAA Breach Notification Rule | 45 CFR Part 164, Subpart D | Breach notification — 60-day requirement |
| HITECH Act | 2009 | Enhanced HIPAA enforcement; breach notification |
| NIST CSF | 2.0 | Cybersecurity framework alignment |
| AWS Shared Responsibility Model | Current | Cloud control inheritance boundary |
| State Health Information Laws | [Insert applicable state] | State-level PHI protection |

---

## Document Control

| Version | Date | Author | Change Description |
|---|---|---|---|
| 0.1 | 2025 | ISSO | Initial draft — System Identification and Categorisation (Steps 1–2) |
| 0.2 | 2025 | ISSO | Control Selection added — all 20 families (Step 3) |
| 0.3 | 2025 | ISSO | Control Implementation Statements added (Step 4 draft) |
| 1.0 | 2025 | ISSO | Final SSP — all sections complete; submitted for SCA assessment |

---

## Formal Approval and Sign-Off

> *By signing below, the named officials confirm they have reviewed the NEXUS System Security Plan and accept their responsibilities as defined herein.*

| Role | Name | Title | Signature | Date |
|---|---|---|---|---|
| **System Owner** | [Name] | Director of Clinical Informatics | _________________________ | 2025 |
| **ISSO** | [Name] | Lead Information Security Analyst | _________________________ | 2025 |
| **ISSM** | [Name] | Deputy Chief Information Security Officer | _________________________ | 2025 |
| **Privacy Officer** | [Name] | Chief Privacy Officer | _________________________ | 2025 |
| **Authorising Official** | [Name] | Chief Information Officer | _________________________ | 2025 |

---

## SSP Section Index

| Section | Title | RMF Step | Status |
|---|---|---|---|
| 1 | System Identification | Step 1 — Prepare | ✅ Complete |
| 2 | System Description and Architecture | Step 1 — Prepare | ✅ Complete |
| 3 | System Environment | Step 1 — Prepare | ✅ Complete |
| 4 | Security Categorisation (FIPS 199) | Step 2 — Categorise | ✅ Complete |
| 5 | Information Types (SP 800-60) | Step 2 — Categorise | ✅ Complete |
| 6 | Control Baseline and Tailoring | Step 3 — Select | ✅ Complete |
| 7 | Control Implementation Statements | Step 4 — Implement | ✅ Complete |
| 8 | Interconnection Agreements | Step 4 — Implement | ✅ Complete |
| 9 | Laws, Regulations, and Policies | All Steps | ✅ Complete |
| 10 | Plan of Action and Milestones (POA&M) | Step 6 — Authorise | 🔄 Pending Assessment |

---

## Related Documents

| Document | Reference | Location |
|---|---|---|
| System Characterisation | NEXUS-RMF-PREP-001 | [01-prepare/system-characterisation.md](../01-prepare/system-characterisation.md) |
| Roles and Responsibilities | NEXUS-RMF-PREP-002 | [01-prepare/roles-and-responsibilities.md](../01-prepare/roles-and-responsibilities.md) |
| Risk Tolerance Statement | NEXUS-RMF-PREP-003 | [01-prepare/risk-tolerance-statement.md](../01-prepare/risk-tolerance-statement.md) |
| FIPS 199 Categorisation (Ref 2) | NEXUS-RMF-CAT-001 | [02-categorise/fips199-system-categorisation.md](../02-categorise/fips199-system-categorisation.md) |
| Data Inventory | NEXUS-RMF-CAT-002 | [02-categorise/data-inventory.md](../02-categorise/data-inventory.md) |
| Control Baseline Summary (Ref 3) | NEXUS-RMF-SEL-001 | [03-select/control-baseline-summary.md](../03-select/control-baseline-summary.md) |
| Tailoring Decisions Log | NEXUS-RMF-SEL-002 | [03-select/tailoring-decisions.md](../03-select/tailoring-decisions.md) |
| Control Selection Worksheet | NEXUS-RMF-SEL-003 | [03-select/control-selection-worksheet.md](../03-select/control-selection-worksheet.md) |
| System Boundary Diagram | N/A | [architecture-diagram.png](../architecture-diagram.png) |

---

*Document Reference: NEXUS-RMF-SSP-001 | Version 1.0 | Classification: Internal — Controlled*
*NEXUS EHR is a fictional system created for GRC portfolio demonstration purposes.*
