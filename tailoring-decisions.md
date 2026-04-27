# Tailoring Decisions Log
## NEXUS Electronic Health Records System | Step 3 — Select Controls

| Field | Detail |
|---|---|
| **Document Reference** | NEXUS-RMF-SEL-002 |
| **Document Type** | Tailoring Decisions Log |
| **Version** | 1.0 |
| **Classification** | Internal — Controlled |
| **Prepared By** | [ISSO Name] |
| **Approved By** | [AO Name] |
| **Date** | 2025 |

---

> **Purpose:** This log formally records every deviation from the NIST SP 800-53 Rev 5 HIGH baseline — including additions, parameter modifications, and scope-outs — with documented justification for each decision. Per NIST SP 800-37 Rev 2 §2.3, all tailoring decisions must be approved by the Authorising Official and documented in the SSP.

---

## Tailoring Decision Types

| Type | Definition |
|---|---|
| **ADD** | Control added beyond the HIGH baseline requirement |
| **ENHANCE** | Control parameter strengthened beyond baseline default |
| **SCOPE-OUT** | Control removed from baseline with justification |
| **INHERIT** | Control implementation inherited from AWS (common control) |
| **MODIFY** | Control parameter adjusted to NEXUS operational context |

---

## Tailoring Decisions Table

| Decision ID | Control | Type | Decision | Justification | Approved By | Date |
|---|---|---|---|---|---|---|
| TD-001 | IA-2(2) | ADD | Extend MFA to all clinical staff (not just privileged accounts) | Clinical staff access PHI directly; credential compromise is top healthcare breach vector; HIPAA minimum necessary principle requires authentication commensurate with data sensitivity | AO | 2025 |
| TD-002 | AU-11 | ADD | Set audit log retention to 6 years minimum | HIPAA requires 6-year retention of security-relevant documentation (§164.316(b)(2)(i)); HIGH baseline default does not specify healthcare-specific duration | ISSO | 2025 |
| TD-003 | AU-9(2) | ADD | Require dedicated, separate Audit Logging Server | PHI breach detection depends on log integrity; co-locating audit logs with application or database servers creates risk that a compromised system destroys its own evidence | ISSO | 2025 |
| TD-004 | AU-13 | ADD | Add SIEM rule set for bulk PHI export detection | Insider threat scenario: authorised user exfiltrates patient records in bulk; standard AU-2 logging captures events but does not include detection logic | ISSO | 2025 |
| TD-005 | SC-8(1) | ENHANCE | Require TLS 1.3 preferred; explicitly disable TLS 1.0 and 1.1 | TLS 1.0 and 1.1 are deprecated; known vulnerabilities (POODLE, BEAST); HIGH baseline requires encryption but does not specify version; NEXUS IoT finding identified TLS 1.0 exposure | ISSO | 2025 |
| TD-006 | SC-28(1) | ADD | Require customer-managed encryption keys (CMK) in AWS KMS | AWS-managed keys would give AWS technical access to encrypted PHI; HIPAA BAA and minimum necessary principle require customer control of PHI encryption keys | AO | 2025 |
| TD-007 | IR-6 | ENHANCE | Add HIPAA breach notification procedures to IR-6 | HITECH Act requires notification to HHS and affected individuals within 60 days of breach discovery; HIGH baseline IR-6 covers incident reporting but does not include healthcare-specific breach notification workflow | ISSO | 2025 |
| TD-008 | IR-6(1) | ADD | Automated SIEM alert escalation to ISSO within 1 hour of detected PHI event | 60-day HIPAA notification clock starts at discovery; early detection shortens the investigation window and reduces regulatory exposure | ISSO | 2025 |
| TD-009 | CA-8 | ADD | Annual third-party penetration test | HIGH baseline recommends penetration testing; NEXUS hybrid architecture and PHI sensitivity make this mandatory; internal vulnerability scanning cannot replace external adversarial testing | AO | 2025 |
| TD-010 | AC-2(7) | ADD | Separate privileged accounts required for all system administrators | Dual-use accounts (regular + admin in one account) increase blast radius of credential compromise; best practice for all HIGH systems | ISSO | 2025 |
| TD-011 | RA-10 | ADD | Quarterly threat hunting exercises via SIEM | Standard monitoring is reactive; proactive threat hunting identifies adversary presence before breach occurs; healthcare is a top-targeted sector | ISSO | 2025 |
| TD-012 | PM-16 | ADD | H-ISAC membership for healthcare threat intelligence | NEXUS operates in a healthcare-specific threat environment; H-ISAC (Health Information Sharing and Analysis Center) provides sector-specific threat intelligence not available in general feeds | ISSO | 2025 |
| TD-013 | PT-7 | ADD | Explicit control over all 18 HIPAA Safe Harbour identifiers | HIPAA de-identification requires all 18 identifiers to be controlled; standard PT family does not enumerate healthcare-specific PII categories | Privacy Officer | 2025 |
| TD-014 | SI-19 | ADD | De-identification procedures for research data sharing | Hospital may share NEXUS data for clinical research; de-identification must be documented and verified before any data leaves the NEXUS boundary for research purposes | Privacy Officer | 2025 |
| TD-015 | CP-9(1) | ADD | Quarterly backup restoration test with results reported to ISSO | Untested backups are not recoverable backups; RTO < 4 hours requires verified, tested restoration procedures; quarterly cadence aligned with clinical care dependency | ISSO | 2025 |
| TD-016 | SI-7(1) | ADD | Automated File Integrity Monitoring (FIM) alerts on PHI-handling systems | Integrity control for database servers and application servers holding PHI; automated FIM detects unauthorised file modifications in near real-time vs manual audit | ISSO | 2025 |
| TD-017 | SA-22 | ADD | End-of-life component inventory; no unsupported OS in PHI data path | Legacy/EOL components are a known attack vector (EternalBlue/WannaCry affected NHS EHR systems); HIGH baseline does not mandate EOL tracking; healthcare precedents make this essential | ISSO | 2025 |
| TD-018 | SC-20 | ADD | DNSSEC for external-facing NEXUS domains | Patient portal is external-facing; DNS hijacking could redirect patients to phishing site harvesting credentials; DNSSEC prevents this attack vector | ISSO | 2025 |
| TD-019 | PE-1 to PE-20 (cloud) | INHERIT | Physical and environmental controls inherited from AWS | AWS data centres are SOC 2 Type II and ISO 27001 certified; physical controls are AWS responsibility under shared responsibility model; NEXUS verifies via annual AWS compliance report review | ISSO | 2025 |
| TD-020 | MA-1 to MA-6 (cloud) | INHERIT | Maintenance controls for cloud infrastructure inherited from AWS | AWS is responsible for underlying infrastructure maintenance; NEXUS responsible for OS and application layer maintenance | ISSO | 2025 |
| TD-021 | SA-11(6) | SCOPE-OUT | Development methodology testing scoped out | NEXUS does not have a formal in-house software development programme; application updates are vendor-managed; SA-11 base control and other enhancements apply to vendor assessment instead | AO | 2025 |

---

## Summary Statistics

| Tailoring Type | Count |
|---|---|
| ADD (controls added beyond HIGH baseline) | 14 |
| ENHANCE (parameters strengthened) | 3 |
| INHERIT (AWS common controls) | 2 groups |
| SCOPE-OUT (not applicable) | 1 |
| **Total tailoring actions** | **20** |

---

## Review and Approval

All tailoring decisions in this log have been reviewed by the ISSO and approved by the Authorising Official. Scope-out decisions (TD-021) have been documented with full justification and will be re-evaluated at each annual review.

| Role | Name | Signature | Date |
|---|---|---|---|
| ISSO | [Name] | _________________________ | 2025 |
| System Owner | [Name] | _________________________ | 2025 |
| **Authorising Official** | **[Name]** | _________________________ | **2025** |

---

*Document Reference: NEXUS-RMF-SEL-002 | Version 1.0 | Classification: Internal — Controlled*
