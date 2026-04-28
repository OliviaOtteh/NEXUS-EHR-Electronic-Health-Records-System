# Authorization Recommendation — Reference 8
## NEXUS Electronic Health Records System | Full ATO Package Compilation

---

```
╔══════════════════════════════════════════════════════════════════════════╗
║                                                                          ║
║         NEXUS ELECTRONIC HEALTH RECORDS SYSTEM                          ║
║         AUTHORIZATION RECOMMENDATION                                     ║
║         REFERENCE 8 — COMPLETE ATO SECURITY PACKAGE                     ║
║                                                                          ║
║         Document Reference : NEXUS-RMF-AUTH-003                         ║
║         Classification     : Internal — Controlled                       ║
║         Prepared By        : [ISSO Name], Lead Information               ║
║                              Security Analyst                            ║
║         Reviewed By        : [ISSM Name], Deputy CISO                   ║
║         Submitted To       : [AO Name], Chief Information Officer        ║
║         Date               : 2026                                    ║
║                                                                          ║
╚══════════════════════════════════════════════════════════════════════════╝
```

---

| Field | Detail |
|---|---|
| **Document Reference** | NEXUS-RMF-AUTH-003 — **Reference 8** |
| **Document Type** | Authorization Recommendation — Full ATO Package |
| **System Name** | NEXUS Electronic Health Records System |
| **System Abbreviation** | NEXUS EHR |
| **Version** | 1.0 — Final |
| **Classification** | Internal — Controlled |
| **FIPS 199 Impact Level** | HIGH — C: HIGH · I: HIGH · A: HIGH |
| **Control Baseline** | NIST SP 800-53 Rev 5 — HIGH |
| **Prepared By** | [ISSO Name], Lead Information Security Analyst |
| **Reviewed By** | [ISSM Name], Deputy Chief Information Security Officer |
| **Submitted To** | [AO Name], Chief Information Officer (Authorising Official) |
| **Date** | 2026|
| **References** | NIST SP 800-37 Rev 2; NIST SP 800-53 Rev 5; HIPAA Security Rule 45 CFR Part 164 |

---

## Table of Contents

1. [Purpose and Scope](#1-purpose-and-scope)
2. [System Overview](#2-system-overview)
3. [ATO Package — All Eight References](#3-ato-package--all-eight-references)
4. [Risk Posture Analysis](#4-risk-posture-analysis)
5. [Control Effectiveness Summary](#5-control-effectiveness-summary)
6. [Residual Risk Assessment](#6-residual-risk-assessment)
7. [HIPAA Compliance Status](#7-hipaa-compliance-status)
8. [Comparison to Peer Healthcare Systems](#8-comparison-to-peer-healthcare-systems)
9. [Authorization Options](#9-authorization-options)
10. [Formal Authorization Recommendation](#10-formal-authorization-recommendation)
11. [Conditions of Authorization](#11-conditions-of-authorization)
12. [Authorization Decision Record](#12-authorization-decision-record)



## 1. Purpose and Scope

### 1.1 Purpose

This Authorization Recommendation compiles the complete ATO security package for the NEXUS Electronic Health Records System across all eight references, synthesises the security posture evidence from all preceding RMF steps, and presents a formal authorization recommendation for the Authorising Official's consideration and decision.

This document serves as:
- The formal cover document for the complete NEXUS ATO package
- A structured risk posture analysis drawn from all assessment evidence
- The ISSO's professional recommendation to the AO
- Reference 8 in the NEXUS RMF documentation series

### 1.2 Regulatory Basis

| Authority | Requirement |
|---|---|
| NIST SP 800-37 Rev 2, §2.6 | Step 6 — Authorize: prepare authorization package; assess risk; authorize system |
| NIST SP 800-53 Rev 5, CA-6 | Authorization: obtain authorization to operate system |
| HIPAA Security Rule §164.308(a)(1) | Security Management Process: implement policies to prevent, detect, contain, and correct violations |
| HIPAA Security Rule §164.308(a)(8) | Evaluation: perform periodic technical and nontechnical evaluation |

### 1.3 Scope

This recommendation covers the full NEXUS system boundary as documented in the System Security Plan (NEXUS-RMF-SSP-001):
- AWS Cloud Zone (Security Stack, Public Subnet, Private Subnet)
- On-Premises Hospital Zone (Data Tier, Security and Audit, Hospital Endpoints)
- All documented interconnections and third-party connections


## 2. System Overview

### 2.1 System Description

NEXUS is a hybrid Electronic Health Records System supporting comprehensive day-to-day healthcare operations across a multi-site clinical environment. It enables healthcare providers to manage patient records, laboratory results, referrals, appointments, billing, and clinical documentation in a secure and centralised environment.

NEXUS processes, stores, and transmits **Protected Health Information (PHI)** and **Personally Identifiable Information (PII)** for **500,000+ active patient records**, serving approximately **2,000 daily clinical and administrative users** and **100,000+ registered patient portal users** across all hospital sites.

### 2.2 Mission Criticality

| Criticality Factor | Assessment |
|---|---|
| Patient safety dependency | CRITICAL — clinical staff rely on NEXUS at the point of care for medication records, allergy data, lab results, and care plans |
| Operational continuity | CRITICAL — 24/7/365 availability required; no viable manual fallback at operational scale |
| Regulatory necessity | MANDATORY — NEXUS is the system of record for all PHI; regulatory compliance depends on its integrity |
| Revenue dependency | HIGH — billing and revenue cycle processing depends on NEXUS availability |
| Multi-site impact | HIGH — a single NEXUS outage affects all clinical sites simultaneously |

### 2.3 Why This Authorization Decision Matters

Unlike most enterprise IT systems, the authorization decision for NEXUS carries patient safety implications. Denying the ATO means clinical staff operate with degraded information systems — increasing medication error risk, clinical decision-making delays, and documentation quality issues. Granting the ATO with inadequate controls means accepting PHI breach risk, HIPAA liability, and patient privacy harm.

The AO must balance two forms of harm: security risk (from granting ATO) and operational/patient safety risk (from denying or significantly delaying ATO).


## 3. ATO Package — All Eight References

The following table presents all eight references that constitute the complete NEXUS ATO package:

| Ref | Title | Document Ref | RMF Step | Key Content | Location |
|---|---|---|---|---|---|
| **Ref 1** | System Boundary Diagram | N/A | Step 1 — Prepare | Three-zone hybrid architecture: Internet Zone, AWS Cloud Zone, On-Premises Hospital Zone; all interconnections including VPN tunnel | [architecture-diagram.png](../architecture-diagram.png) |
| **Ref 2** | FIPS 199 Security Categorisation | NEXUS-RMF-CAT-001 | Step 2 — Categorise | System impact level: HIGH across all three objectives (C/I/A); 15 information types mapped to SP 800-60; full justification for each objective | [categorise/fips199-system-categorisation.md](../fips199-system-categorisation.md) |
| **Ref 3** | Control Baseline Summary | NEXUS-RMF-SEL-001 | Step 3 — Select | 221 controls selected from NIST SP 800-53 Rev 5 HIGH baseline; 21 tailoring decisions documented; HIPAA mapping; AWS inherited controls | [select/control-baseline-summary.md](../control-baseline-summary.md) |
| **Ref 4** | SSP Cover Page | NEXUS-RMF-SSP-001 | Step 4 — Implement | System identification; key personnel; applicable laws; version history; 10-section SSP index; 5-party approval block | [04-implement/ssp-cover-page.md](../04-implement/ssp-cover-page.md) |
| **Ref 5** | Risk Register | NEXUS-RMF-RA-002 | Risk Assessment | 28 risks identified; 4 Critical, 10 High, 11 Medium, 3 Low; NIST SP 800-30 methodology; MITRE ATT&CK mapping; healthcare-specific threat landscape | [risk-assessment/risk-register.md](../risk-assessment/risk-register.md) |
| **Ref 6** | SAR Findings Summary | NEXUS-RMF-SAR-001 | Step 5 — Assess | 221 controls assessed; 198 Satisfied (89.6%); 18 findings (0 Critical, 5 High, 9 Medium, 4 Low); pen test result; SCA recommendation to authorize | [05-assess/sar-findings-summary.md](../05-assess/sar-findings-summary.md) |
| **Ref 7** | POA&M Tracker | NEXUS-RMF-POAM-001 | Step 6 — Authorise | All 18 findings tracked with owners, milestones, target dates; P-004 closed pre-ATO; monthly review cycle established; escalation procedures | [06-authorise/poam-tracker.md](../06-authorise/poam-tracker.md) |
| **Ref 8** | Authorization Recommendation | NEXUS-RMF-AUTH-003 | Step 6 — Authorize | **This document** — Full risk posture synthesis; ISSO recommendation; authorization options; formal AO decision record | **This document** |

### 3.1 Package Completeness Verification

| Package Element | Required | Present | Complete |
|---|---|---|---|
| System Security Plan (SSP) | Yes | Yes | ✅ |
| Security Assessment Report (SAR) | Yes | Yes | ✅ |
| Plan of Action and Milestones (POA&M) | Yes | Yes | ✅ |
| Risk Assessment | Yes | Yes | ✅ |
| FIPS 199 Categorisation | Yes | Yes | ✅ |
| System Boundary Diagram | Yes | Yes | ✅ |
| Control Baseline Documentation | Yes | Yes | ✅ |
| SCA Independence Declaration | Yes | Yes | ✅ |
| Pre-ATO Condition Evidence (P-004) | Yes | Yes | ✅ |
| Authorization Recommendation | Yes | Yes | ✅ |

**Package status: COMPLETE — All required elements present**

---

## 4. Risk Posture Analysis

### 4.1 Overall Risk Posture Statement

Based on synthesis of all assessment evidence, NEXUS presents a **moderate-to-strong security posture** for a HIGH-impact healthcare system. The programme demonstrates maturity in critical control areas — authentication, encryption, audit logging, and incident response — with targeted gaps in process consistency, training culture, and automation completeness. No fundamental control failures were identified, and the organisation has demonstrated commitment to remediation through the pre-ATO closure of the MFA finding.

### 4.2 Risk Posture by Security Objective

#### Confidentiality Risk Posture — MODERATE

| Factor | Assessment |
|---|---|
| PHI access control (RBAC) | Strong — three-layer enforcement verified; no bypass found |
| Authentication | Strong — MFA enforced for all users; pre-ATO gap remediated |
| Encryption at rest | Strong — AES-256 with CMK on all PHI storage; FIPS 140-2 HSM |
| Encryption in transit | Moderate — TLS configuration strong on most paths; 2 legacy endpoints pending |
| Insider threat detection | Moderate — bulk access detection operational; slow exfiltration remains residual risk |
| Third-party PHI controls | Moderate — 3 IoT BAAs pending; process improvement in progress |
| Patient portal security | Strong — TLS, MFA, session timeout, HIPAA banner all verified |
| **Confidentiality posture** | **MODERATE — critical controls strong; targeted gaps under remediation** |

#### Integrity Risk Posture — MODERATE-STRONG

| Factor | Assessment |
|---|---|
| Audit logging | Strong — all PHI access events logged; dedicated Audit Server; hash chain verified |
| Log integrity protection | Moderate — hash chain implemented; automation gap being closed (P-002) |
| File integrity monitoring | Moderate — FIM deployed; baseline staleness found; being corrected (P-007) |
| Database integrity | Strong — PostgreSQL replication monitored; failover tested; FIM on DB servers |
| Application input validation | Strong — SQL injection and XSS blocked; verified in penetration test |
| Non-repudiation | Strong — unique IDs, MFA, hash chain; no shared accounts |
| Clinical record integrity | Strong — RBAC prevents unauthorised modification; audit trail complete |
| **Integrity posture** | **MODERATE-STRONG — logging infrastructure robust; FIM automation gap minor** |

#### Availability Risk Posture — MODERATE-STRONG

| Factor | Assessment |
|---|---|
| Redundancy (application tier) | Strong — dual EC2 servers; ALB failover in 28 seconds |
| Database failover | Strong — primary/secondary replication; failover in 14 minutes (RTO 30 min) |
| Backup and recovery | Strong — daily incremental, weekly full; Q4 test gap closed; RTO 3h 42m |
| DDoS protection | Strong — AWS Shield and WAF rate limiting verified |
| Contingency planning | Moderate — CP document outdated post-AZ change; being corrected (P-013) |
| Clinical downtime procedures | Strong — paper-based fallback documented and trained |
| SIEM monitoring | Moderate — monitoring comprehensive; after-hours alert fatigue being tuned (P-011) |
| **Availability posture** | **MODERATE-STRONG — redundancy and recovery strong; documentation gap minor** |

### 4.3 Threat Landscape Alignment

Drawing from the Risk Register (Reference 5), the following table maps the top risks to current control effectiveness:

| Risk | Risk Rating | Control Effectiveness | Residual Risk |
|---|---|---|---|
| R-001 Ransomware | Critical | High — backups, EDR, network segmentation, MFA | Medium — IoT lateral movement path remains |
| R-002 Insider PHI exfiltration | Critical | Moderate — RBAC, bulk access detection, access reviews | Medium-High — slow exfiltration below threshold |
| R-003 Credential stuffing | Critical | High — MFA verified resilient in all 15 test cases | Low — MFA fatigue awareness training in progress |
| R-004 IoT exploitation | Critical | Moderate — VLAN segmentation held in pen test | Medium — BAA gaps; micro-segmentation enhancement recommended |
| R-005 Unplanned clinical outage | High | High — dual servers, 14-min DB failover, tested backups | Low — multi-AZ deployment in progress |
| R-006 SQL injection | High | High — WAF + app-level validation blocked all test payloads | Low — annual pen test established |
| R-010 Endpoint malware | Medium | High — EDR, USB blocked, phishing training | Medium — 22% phishing click rate; training programme in progress |
| R-019 Third-party breach | Medium | Moderate — BAAs in place for most; 3 IoT vendor gaps | Medium — IoT BAA remediation in progress |

### 4.4 Security Programme Maturity Assessment

| Programme Area | Maturity Level | Evidence |
|---|---|---|
| Risk management | Defined (Level 3) | Annual risk assessment; Risk Register with 28 entries; MITRE ATT&CK mapping |
| Access control | Managed (Level 4) | Three-layer RBAC verified; quarterly reviews; automated deprovisioning (with recent gap corrected) |
| Vulnerability management | Defined (Level 3) | Weekly scans; CVE monitoring; remediation SLA (with 3 items found overdue — being corrected) |
| Incident response | Managed (Level 4) | IRP documented; SIEM automation; HIPAA breach notification; tabletop exercises; IR retainer |
| Audit and accountability | Managed (Level 4) | Dedicated Audit Server; hash chain; SIEM; WORM retention; bulk access detection verified |
| Training and awareness | Developing (Level 2) | Annual training; 22% phishing click rate indicates training needs improvement |
| Contingency planning | Defined (Level 3) | CP documented; tested quarterly; documentation gap found and being corrected |
| Third-party risk | Developing (Level 2) | BAA programme established; 3 IoT BAA gaps; annual supplier review in place |
| Encryption | Managed (Level 4) | AES-256 everywhere; CMK; FIPS 140-2; TLS 1.3; legacy endpoint gap being closed |

**Overall programme maturity: Level 3 — Defined/Managed**
*Consistent with a healthcare organisation at 2–3 years into a formal security programme*

---

## 5. Control Effectiveness Summary

### 5.1 Assessment Results Summary

| Metric | Value | Interpretation |
|---|---|---|
| Controls assessed | 221 | Full HIGH baseline |
| Controls Satisfied | 198 | 89.6% — strong overall posture |
| Other Than Satisfied | 23 | 10.4% — targeted gaps, not systemic failure |
| Critical findings | 0 | No catastrophic control absences |
| High findings | 5 | Significant but addressable; 1 closed pre-ATO |
| Medium findings | 9 | Moderate gaps; tracked in POA&M |
| Low findings | 4 | Minor; low operational impact |
| Pen test — critical/high | 0 | Architecture resilient to external attack |
| Backup RTO achieved | 3h 42m | Within 4-hour target |
| DB failover RTO | 14 minutes | Within 30-minute target |
| MFA bypass tests | 0/15 | MFA held in every test |
| Bulk PHI access detection | 4 minutes | Within 10-minute target |

### 5.2 Control Families with No Findings

The following control families received a **100% Satisfied** determination — demonstrating comprehensive implementation with no identified gaps:

| Family | Controls | Result | Notable Strength |
|---|---|---|---|
| CM — Configuration Management | 12 | ✅ All SAT | CIS benchmark compliance; CAB change control |
| IR — Incident Response | 10 | ✅ All SAT | HIPAA breach notification; 24/7 SOC; IR retainer |
| MA — Maintenance | 6 | ✅ All SAT | AWS-inherited; on-premises maintenance documented |
| MP — Media Protection | 8 | ✅ All SAT | USB disabled; DoD wipe; media tracking |
| PL — Planning | 4 | ✅ All SAT | SSP comprehensive; architecture documented |
| PM — Program Management | 9 | ✅ All SAT | ISSO/ISSM roles active; programme plan current |
| PS — Personnel Security | 9 | ✅ All SAT | Background checks; 24-hour deprovisioning SLA (with one period of non-compliance corrected) |
| SA — System Acquisition | 11 | ✅ All SAT | BAA programme; SDLC security integration |
| SR — Supply Chain Risk | 8 | ✅ All SAT | Vendor assessment; IoT inspection; notification agreements |

### 5.3 Strongest Individual Controls

Based on assessment testing, the following controls performed at the highest level — providing strong assurance for the AO:

| Control | Test Result | Why This Matters |
|---|---|---|
| IA-2(1)(2) — MFA | 15/15 bypass attempts blocked; break-glass alerted in 2 minutes | Credential compromise — the #1 healthcare breach vector — is effectively countered |
| AU-11 — Log Retention | S3 Object Lock deletion blocked even with root account credentials | Audit evidence is protected from tampering or deletion — critical for breach investigation |
| SC-28(1) — Encryption at Rest | AES-256 on all PHI storage; CMK; FIPS 140-2 HSM | If physical media is stolen or storage is accessed without authentication, PHI remains protected |
| CP-10 — Recovery | Scenario B DB failover: 14 minutes; Scenario A ALB failover: 28 seconds | Clinical operations can survive infrastructure failure without extended patient safety impact |
| SI-4 — System Monitoring | Bulk PHI access detection: 4 minutes alert; SOC response: 6 minutes | Insider exfiltration at scale is detectable and responded to within minutes |
| AU-9(2) — Audit Server | 6 months hash chain intact; dedicated server confirmed; non-ISSO deletion blocked | Audit trail integrity is verified — evidence for future investigations is protected |

---

## 6. Residual Risk Assessment

### 6.1 Residual Risk Register — Post-Control Application

After applying existing NEXUS controls, the following residual risks remain:

| Risk Area | Pre-Control Risk | Residual Risk | Key Compensating Control | POA&M |
|---|---|---|---|---|
| Ransomware | Critical (25) | Medium | Backups tested (3h 42m RTO); EDR; IoT VLAN segmentation; MFA | P-003, P-005 |
| Insider PHI exfiltration — slow | Critical (20) | Medium-High | Quarterly access reviews; AU-13 bulk detection; RBAC minimum necessary | P-009, P-011 |
| Credential compromise | Critical (20) | Low | MFA verified resilient; FIDO2 being extended to privileged accounts | P-009 |
| IoT lateral movement | Critical (20) | Medium | VLAN segmentation held in pen test; BAA gaps being closed | P-010 |
| Legacy TLS 1.2 on 2 endpoints | High (15) | Low-Medium | Hardware replacement in progress; TLS 1.2 is not broken | P-003 |
| Phishing susceptibility | Medium (12) | Medium | MFA prevents credential-only breach; training programme active | P-009 |
| Unpatched CVEs | High (15) | Low | All 3 High CVEs patched; process improvement in progress | P-005 |
| After-hours PHI access evasion | Medium (9) | Medium | Alert present; tuning in progress to reduce false positives | P-011 |
| Third-party IoT breach | Medium (8) | Low-Medium | IoT VLAN isolation; BAA programme active | P-010 |

### 6.2 Aggregate Residual Risk Rating

| Objective | Residual Risk Level | Basis |
|---|---|---|
| Confidentiality | **Medium** | MFA and RBAC strong; insider slow-exfiltration and IoT BAA gaps remain |
| Integrity | **Low-Medium** | Audit chain and FIM robust; FIM automation gap being closed |
| Availability | **Low** | Redundancy, failover, and backup all tested and within target |
| **Overall Residual Risk** | **Medium** | No critical residuals; all open items tracked in POA&M with owners and dates |

### 6.3 Risk Trajectory — Improving

The security programme shows a positive risk trajectory. Key indicators:

- **P-004 (MFA for 4 billing accounts)** — closed before ATO request, demonstrating organisational commitment to remediation
- **P-005 (3 High CVEs)** — all patches applied within 5 days of ATO grant
- **Three POA&M items fully closed** at time of this recommendation
- **Zero critical findings** in the first formal SCA assessment
- **First penetration test** completed with no critical or high exploitable findings
- Process improvements for deprovisioning automation, hash chain verification, and patch SLA monitoring are all active

The programme is maturing — not declining. The residual risks are consistent with a healthcare organisation that has implemented a formal security programme and is systematically closing identified gaps.

---

## 7. HIPAA Compliance Status

### 7.1 HIPAA Security Rule Compliance Assessment

| HIPAA Standard | 45 CFR Reference | Compliance Status | Evidence |
|---|---|---|---|
| Security Management Process | §164.308(a)(1) | ✅ Compliant | Annual risk assessment; SSP; policies implemented |
| Assigned Security Responsibility | §164.308(a)(2) | ✅ Compliant | ISSO formally assigned; ISSM in place |
| Workforce Security | §164.308(a)(3) | ✅ Compliant | Background checks; 24-hour deprovisioning; sanctions policy |
| Information Access Management | §164.308(a)(4) | ✅ Compliant | RBAC three-layer enforcement; minimum necessary verified |
| Security Awareness and Training | §164.308(a)(5) | ⚠️ Partial | Annual training in place; 22% phishing rate indicates gap; training enhancement active (P-009) |
| Security Incident Procedures | §164.308(a)(6) | ✅ Compliant | IRP with HIPAA breach notification; 60-day workflow documented; tested |
| Contingency Plan | §164.308(a)(7) | ⚠️ Partial | CP documented; backup tested; CP document outdated post-AZ change (P-013) |
| Evaluation | §164.308(a)(8) | ✅ Compliant | Annual SCA assessment; continuous monitoring; pen test |
| Business Associate Contracts | §164.308(b)(1) | ⚠️ Partial | Most BAAs in place; 3 IoT vendors pending (P-010) |
| Facility Access Controls | §164.310(a) | ✅ Compliant | Badge access; CCTV; visitor log; tested in assessment |
| Workstation Controls | §164.310(b)(c) | ✅ Compliant | Device lock; encryption; MDM; USB disabled |
| Device and Media Controls | §164.310(d) | ✅ Compliant | Media marking; DoD wipe; USB disabled; chain of custody |
| Access Control | §164.312(a) | ✅ Compliant | RBAC; automatic logoff; encryption; unique user IDs |
| Audit Controls | §164.312(b) | ✅ Compliant | Full PHI access logging; Audit Server; SIEM; 6-year WORM retention |
| Integrity | §164.312(c) | ✅ Compliant | Hash chain; FIM; input validation; non-repudiation |
| Person Authentication | §164.312(d) | ✅ Compliant | MFA all users; lockout; FIPS 140-2 crypto |
| Transmission Security | §164.312(e) | ⚠️ Partial | TLS 1.2+ on all paths; 2 legacy endpoints pending TLS 1.3 (P-003) |

**HIPAA compliance summary: 13 of 17 standards fully compliant; 4 partially compliant with active remediation plans**

### 7.2 HIPAA Partial Compliance Analysis

All four partially compliant standards have:
- A documented finding in the SAR (Reference 6)
- An active POA&M entry with owner and target date (Reference 7)
- No evidence of actual PHI breach or patient harm

The partial compliance items represent **implementation gaps** in an otherwise functional compliance programme — not fundamental programme failures. OCR enforcement practice distinguishes between organisations with documented, active remediation programmes and organisations that ignore identified gaps.

---

## 8. Comparison to Peer Healthcare Systems

### 8.1 Industry Benchmark Context

Based on published healthcare cybersecurity research and HHS OCR breach portal data, the following benchmarks contextualise NEXUS's posture:

| Metric | Industry Average (Healthcare) | NEXUS | Assessment |
|---|---|---|---|
| % controls satisfied in formal assessment | 75–85% | **89.6%** | Above average |
| Annual phishing click rate | 25–35% | **22%** | Below average (better) |
| Mean time to detect PHI breach | 329 days | **<10 min (bulk); varies (slow)** | Significantly better |
| Backup RTO target achievement | 60% of healthcare orgs | **PASSED (3h 42m)** | Better |
| MFA enforcement for all users | 45% of healthcare orgs | **Yes — verified** | Better |
| Formal annual pen test | 35% of healthcare orgs | **Yes — first test completed** | Better |
| Dedicated audit logging infrastructure | 40% of healthcare orgs | **Yes — separate Audit Server** | Better |
| Open Critical findings at time of ATO | N/A (benchmark: >2 common) | **0** | Better |
| Ransomware attack in past 12 months | 73% of healthcare orgs | **None** | Better |

**NEXUS compares favourably against peer healthcare organisations across all measured dimensions.** The 89.6% control satisfaction rate, zero critical findings, and verified backup/failover capability represent a security posture above the healthcare sector average.

---

## 9. Authorization Options

The AO has three possible authorization decisions under NIST SP 800-37 Rev 2:

### Option A — Full Authority to Operate (Recommended)

**Decision:** Grant ATO with conditions
**ATO Term:** 3 years (2025–2028)
**Rationale:** 198 of 221 controls satisfied; zero critical findings; critical controls (MFA, encryption, audit logging, backup, failover) all verified functional; pre-ATO condition (MFA for 4 accounts) met; SCA recommends ATO; residual risk is Medium and consistent with a mature, improving programme; clinical necessity of NEXUS makes denial highly detrimental to patient care

**Conditions attached:**
- P-001, P-002, P-003, P-005 remediated within 30 days
- P-010 (IoT BAA) resolved within 30 days
- Monthly POA&M reporting to AO
- Annual reassessment 2026

**Impact of this decision:** NEXUS continues operations under formal authorization with documented residual risk acceptance and active remediation programme

---

### Option B — Interim Authority to Operate

**Decision:** Grant 90-day interim ATO; convert to full ATO when High findings remediated
**ATO Term:** 90 days, with extension to 3 years upon High finding closure
**Rationale:** More conservative approach; ensures High findings closed before full 3-year term granted
**Conditions:** All High findings (P-001, P-002, P-003, P-005) closed within 30 days; evidence submitted to ISSO; ISSO confirms closure; AO grants full 3-year ATO

**Impact:** Creates administrative overhead; no additional security benefit since findings are already being actively remediated; clinical operations continue under interim authorization

---

### Option C — Denial of ATO (Not Recommended)

**Decision:** Deny ATO; require full remediation before resubmission
**Rationale:** Would be appropriate if critical findings existed, if fundamental control families were absent, or if the organisation demonstrated unwillingness to remediate
**Why not appropriate for NEXUS:** No critical findings; pre-ATO condition already met; SCA recommends ATO; clinical necessity makes denial directly harmful to patients; residual risk is Medium — consistent with sector norms

**Impact of this decision:** NEXUS operates without formal authorization; clinical operations cannot be suspended (patient safety); creates HIPAA compliance risk; does not improve security posture; not recommended

---

## 10. Formal Authorization Recommendation

### ISSO Recommendation

Having conducted the full RMF process across all seven steps, compiled all eight references into this complete ATO package, and synthesised the security posture evidence from the System Security Plan, Security Assessment Report, Risk Register, and POA&M, I submit the following recommendation to the Authorising Official:

---

```
╔══════════════════════════════════════════════════════════════════════╗
║                                                                      ║
║  ISSO AUTHORIZATION RECOMMENDATION                                   ║
║                                                                      ║
║  I recommend the Authorising Official GRANT FULL AUTHORITY TO       ║
║  OPERATE (Option A) for the NEXUS Electronic Health Records          ║
║  System for a 3-year term (2025–2028), subject to the conditions    ║
║  detailed in Section 11 of this document.                            ║
║                                                                      ║
║  Basis:                                                              ║
║  • 198/221 controls Satisfied (89.6%) — above healthcare average    ║
║  • 0 Critical findings — no catastrophic control absences           ║
║  • Critical controls verified: MFA, encryption, audit logging,      ║
║    backup recovery, database failover, SIEM monitoring               ║
║  • Pre-ATO condition met — P-004 MFA remediated and evidenced       ║
║  • Independent SCA recommends ATO                                    ║
║  • Residual risk: Medium — consistent with mature programme         ║
║  • Positive risk trajectory — programme improving, not declining    ║
║  • Clinical necessity — NEXUS denial would create patient safety     ║
║    risk greater than the residual security risk                      ║
║  • HIPAA compliance: 13/17 standards fully compliant; 4 with        ║
║    active, documented remediation plans                              ║
║                                                                      ║
║  Signed: [ISSO Name]                     Date: 2025                 ║
║          Lead Information Security Analyst                           ║
║                                                                      ║
╚══════════════════════════════════════════════════════════════════════╝
```

---

### ISSM Concurrence

```
╔══════════════════════════════════════════════════════════════════════╗
║                                                                      ║
║  ISSM CONCURRENCE                                                    ║
║                                                                      ║
║  I concur with the ISSO's recommendation. The NEXUS security        ║
║  package is complete and the risk posture supports authorization.    ║
║  The programme demonstrates appropriate controls for a HIGH-impact   ║
║  healthcare system, and the identified gaps are being actively       ║
║  remediated with appropriate urgency.                                ║
║                                                                      ║
║  Signed: [ISSM Name]                     Date: 2025                 ║
║          Deputy Chief Information Security Officer                   ║
║                                                                      ║
╚══════════════════════════════════════════════════════════════════════╝
```

---

## 11. Conditions of Authorization

The following conditions are attached to the ATO recommendation. The AO may accept, modify, or add conditions at their discretion:

### Mandatory Conditions — Failure May Trigger ATO Suspension

| ID | Condition | Owner | Deadline |
|---|---|---|---|
| C-001 | P-001: Account deprovisioning automation fully repaired and monitored for 30 days | SA / ISSO | ATO + 30 days |
| C-002 | P-002: Hash chain verification automated in SIEM; alert tested and confirmed | SOC / ISSO | ATO + 30 days |
| C-003 | P-003: 2 legacy workstations replaced; IoT cipher reconfigured; TLS re-scan confirms compliance | SA | ATO + 30 days |
| C-004 | P-005: Patch SLA monitoring automation implemented; no High CVE exceeds 30-day SLA at next quarterly scan | SA / ISSO | ATO + 30 days |
| C-005 | P-010: All 3 IoT vendor BAAs executed; or non-compliant devices disconnected from NEXUS | CPO / Legal | ATO + 30 days |

### Standard Conditions — Ongoing Requirements

| ID | Condition | Frequency |
|---|---|---|
| C-006 | Monthly POA&M status report submitted to AO | Monthly — by 5th of each month |
| C-007 | Continuous monitoring programme maintained per CA-7 | Continuous |
| C-008 | Any PHI security incident reported to AO within 4 hours of ISSO notification | Per incident |
| C-009 | Significant system changes submitted for security impact assessment before implementation | Per change |
| C-010 | Annual security reassessment by independent SCA — 2026 assessment to begin Q1 2026 | Annual |
| C-011 | Annual risk assessment completed on time (within 2 weeks of anniversary) | Annual |
| C-012 | Phishing simulation click rate at or below 15% by Q4 2025 simulation | Quarterly check |

---

## 12. Authorization Decision Record

### AO Decision

Having reviewed the complete NEXUS ATO security package (References 1–8), considered the ISSO and ISSM recommendations, and weighed the residual risks against the operational and clinical necessity of NEXUS, I record the following authorization decision:

| Field | Detail |
|---|---|
| **System Name** | NEXUS Electronic Health Records System |
| **Authorization Decision** | ✅ **AUTHORITY TO OPERATE — GRANTED** |
| **Authorization Type** | Full ATO — Option A |
| **ATO Term** | 3 years |
| **Effective Date** | 2025 |
| **Expiry Date** | 2028 |
| **Conditions** | As listed in Section 11 — all conditions accepted |
| **Residual Risk Accepted** | Medium — consistent with HIGH-impact healthcare system; all critical controls verified; no patient safety events from identified gaps |
| **Basis for Decision** | 198/221 controls satisfied; 0 critical findings; MFA pre-condition met; SCA recommendation reviewed; clinical necessity; positive risk trajectory; HIPAA programme functional |
| **Next Review** | Annual security status review; full reassessment 2026 |

### Risk Acceptance Statement

> *"I, [AO Name], in my capacity as Authorising Official for the NEXUS Electronic Health Records System, have reviewed the complete security authorization package (References 1–8). I accept the residual risk of operating NEXUS as documented in this authorization recommendation, subject to the conditions detailed in Section 11. I understand that this authorization covers the system boundary defined in the System Security Plan (NEXUS-RMF-SSP-001) and that significant changes to that boundary require a new security impact assessment and potential reauthorisation. I accept responsibility for this risk decision on behalf of Nexus Health System."*

### Signatures

| Role | Name | Title | Signature | Date |
|---|---|---|---|---|
| Prepared By | [ISSO Name] | Lead Information Security Analyst | _________________________ | 2025 |
| Reviewed By | [ISSM Name] | Deputy Chief Information Security Officer | _________________________ | 2025 |
| System Owner Acknowledgement | [SO Name] | Director of Clinical Informatics | _________________________ | 2025 |
| **Authorising Official Decision** | **[AO Name]** | **Chief Information Officer** | _________________________ | **2025** |

---

## 13. GitHub Portfolio Integration

### Repository Location

```
nexus-ehr-rmf/
├── README.md                              ← Root portfolio overview
├── architecture-diagram.png               ← Ref 1 — System Boundary Diagram
├── 01-prepare/                            ← Step 1
├── 02-categorise/                         ← Ref 2 — FIPS 199
├── 03-select/                             ← Ref 3 — Control Baseline
├── 04-implement/                          ← Ref 4 — SSP Cover Page
├── risk-assessment/                       ← Ref 5 — Risk Register
├── 05-assess/                             ← Ref 6 — SAR Findings
├── 06-authorise/                          ← Ref 7 — POA&M Tracker
├── authorization/                         ← THIS FOLDER
│   ├── README.md
│   ├── authorization-recommendation.md    ← Ref 8 — THIS DOCUMENT
│   ├── ato-package-index.md
│   └── executive-risk-summary.md
└── 07-monitor/                            ← Step 7
```

### Upload Instructions

1. Go to your `nexus-ehr-rmf` repository on GitHub
2. Click **Add file → Create new file**
3. Type the path: `authorization/authorization-recommendation.md`
4. Paste the full contents of this document
5. Commit message: `Authorization: Add Authorization Recommendation (Ref 8) — ATO granted — NEXUS EHR`

### Root README Final Update

```markdown
| Auth | [Authorization](./authorization/) | ✅ Complete | Ref 8 · Full ATO Package · ATO Granted 2025 · 3-Year Term |
```

### LinkedIn Portfolio Post (Final)

> 🎯 **NEXUS EHR RMF Portfolio — Complete**
>
> I've built a complete end-to-end NIST RMF implementation for NEXUS, a fictional HIPAA-regulated hybrid EHR system, across 8 formal references:
>
> ✅ Ref 1 — System Boundary Diagram (3-zone hybrid architecture)
> ✅ Ref 2 — FIPS 199 HIGH categorisation (C/I/A all HIGH)
> ✅ Ref 3 — NIST 800-53 Rev 5 HIGH baseline (221 controls, 21 tailoring decisions)
> ✅ Ref 4 — System Security Plan (10 sections, 219/221 controls implemented)
> ✅ Ref 5 — Risk Register (28 risks, MITRE ATT&CK mapped, multi-site healthcare context)
> ✅ Ref 6 — SAR Findings Summary (221 controls assessed, 18 findings, pen test completed)
> ✅ Ref 7 — POA&M Tracker (18 items tracked, ATO conditions managed)
> ✅ Ref 8 — Authorization Recommendation (ATO granted, risk posture analysis)
>
> The project covers real-world GRC skills: HIPAA compliance mapping, threat modelling, control tailoring, security assessment methodology, risk acceptance decisions, and continuous monitoring programme design.
>
> 🔗 [GitHub Repository Link]
>
> #GRC #NIST #RMF #HIPAA #Cybersecurity #HealthcareSecurity #InfoSec

---

*Document Reference: NEXUS-RMF-AUTH-003 — Reference 8 | Version 1.0 — Final | Classification: Internal — Controlled*
*NEXUS EHR is a fictional system created for a GRC portfolio demonstration. All names, data, and system details are illustrative only.*
