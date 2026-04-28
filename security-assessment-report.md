# Security Assessment Report (SAR)
## NEXUS Electronic Health Records System | Step 5 — Assess Controls

| Field | Detail |
|---|---|
| **Document Reference** | NEXUS-RMF-SAR-001 |
| **Document Type** | Security Assessment Report — Full |
| **Version** | 1.0 — Final |
| **Classification** | Internal — Controlled — Restricted Distribution |
| **Prepared By** | [Lead SCA Name], [Assessor Firm] |
| **Approved By** | [AO Name], Chief Information Officer |
| **Assessment Period** | 2025 (9-week assessment) |
| **Findings Summary** | [sar-findings-summary.md](./sar-findings-summary.md) — Reference 6 |

> **Note:** This document provides the full Security Assessment Report. The **SAR Findings Summary (Reference 6)** is at [sar-findings-summary.md](./sar-findings-summary.md). The detailed test-by-test evidence is at [assessment-test-results.md](./assessment-test-results.md).

---

## Section 1 — Assessment Overview

### 1.1 System Under Assessment

NEXUS Electronic Health Records System — a hybrid EHR platform processing PHI and PII for 500,000+ patients across a multi-site clinical environment. FIPS 199 Impact Level: HIGH. Control Baseline: NIST SP 800-53 Rev 5 HIGH (221 controls).

### 1.2 Assessment Authority

This assessment was directed by the Authorising Official and conducted by an independent SCA team under the authority of the approved Security Assessment Plan (NEXUS-RMF-SAP-001). The SCA has no operational responsibility for NEXUS and has signed an independence declaration.

### 1.3 Assessment Objectives

| Objective | Achieved |
|---|---|
| Determine whether all 221 controls are implemented correctly | ✅ Yes |
| Determine whether controls are operating as intended | ✅ Yes |
| Determine whether controls produce the desired security outcomes | ✅ Yes |
| Identify control deficiencies and rate by severity | ✅ Yes — 18 findings |
| Conduct annual penetration test | ✅ Yes |
| Conduct phishing simulation | ✅ Yes |
| Conduct backup restoration test | ✅ Yes |
| Provide ATO recommendation to AO | ✅ Yes — Recommend ATO |

---

## Section 2 — Assessment Results by Control Family

### 2.1 AC — Access Control

| Control | Assessment Method | Result | Finding |
|---|---|---|---|
| AC-1 | Examine | ✅ SAT | Policy current, distributed, signed |
| AC-2 | Examine, Test | 🟠 OTS-H | F-001 — 3 accounts deprovisioned late |
| AC-2(1) | Examine, Test | ✅ SAT | Automation functional for 97% of cases |
| AC-2(3) | Test | ✅ SAT | 90-day inactivity rule verified firing correctly |
| AC-2(7) | Examine | ✅ SAT | Privileged account register current; dual-account verified |
| AC-3 | Test | ✅ SAT | Three-layer RBAC verified — bypass attempts blocked |
| AC-3(7) | Test | ✅ SAT | Role permissions matrix matches implementation |
| AC-4 | Test | ✅ SAT | Flow enforcement verified — cross-zone traffic blocked |
| AC-5 | Test | ✅ SAT | Separation confirmed — no account crosses PHI + audit access |
| AC-6 | Examine | ✅ SAT | Minimum necessary enforced by role |
| AC-6(1) | Test | ✅ SAT | Security function access restricted to ISSO/ISSM |
| AC-6(5) | Examine | ✅ SAT | Privileged account quarterly review records found |
| AC-6(9) | Test | ✅ SAT | Privileged actions logged — verified in Audit Server |
| AC-7 | Test | ✅ SAT | Lockout confirmed at 5 attempts; 30-min lock verified |
| AC-8 | Test | 🟢 OTS-L | F-017 — Banner missing on admin console only |
| AC-11 | Test | ✅ SAT | 15-min device lock confirmed on Windows and iOS |
| AC-12 | Test | ✅ SAT | 30-min NEXUS session timeout confirmed |
| AC-14 | Test | ✅ SAT | No PHI accessible pre-authentication |
| AC-17 | Test | ✅ SAT | Only 2 authorised pathways confirmed; all others blocked |
| AC-18 | Examine | ✅ SAT | 802.1X verified; wireless policy current |
| AC-19 | Test | ✅ SAT | MDM enrollment required — unenrolled device blocked |
| AC-20 | Examine | ✅ SAT | BAA register reviewed; external system authorisation policy found |
| AC-22 | Test | ✅ SAT | Patient portal public content reviewed — no pre-auth PHI |
| **AC Summary** | | **22 SAT / 1 OTS-H / 0 OTS-M / 1 OTS-L** | F-001, F-017 |

---

### 2.2 AT — Awareness and Training

| Control | Assessment Method | Result | Finding |
|---|---|---|---|
| AT-1 | Examine | ✅ SAT | Training policy current and distributed |
| AT-2 | Examine, Test | 🟡 OTS-M | F-009 — 22% phishing click rate; F-016 — 3 incomplete |
| AT-2(2) | Examine | ✅ SAT | Insider threat module confirmed in training content |
| AT-3 | Examine | 🟢 OTS-L | F-018 — Removable media missing from training |
| AT-4 | Examine | ✅ SAT | LMS records retained; 6-year retention confirmed |
| AT-6 | Examine | ✅ SAT | Feedback survey and annual review evidenced |
| **AT Summary** | | **4 SAT / 0 OTS-H / 1 OTS-M / 1 OTS-L** | F-009, F-016, F-018 |

---

### 2.3 AU — Audit and Accountability

| Control | Assessment Method | Result | Finding |
|---|---|---|---|
| AU-1 | Examine | ✅ SAT | Audit policy current |
| AU-2 | Examine, Test | ✅ SAT | All event types verified logging to Audit Server |
| AU-3 | Examine, Test | ✅ SAT | All required fields present in log samples |
| AU-4 | Examine | ✅ SAT | Storage capacity report shows 34% utilised; alert at 75% configured |
| AU-5 | Test | ✅ SAT | Syslog failure test triggered alert in 3 minutes |
| AU-6 | Examine, Interview | ✅ SAT | Daily SIEM report produced and reviewed |
| AU-6(1) | Test | 🟡 OTS-M | F-011 — After-hours alert generating excess false positives |
| AU-7 | Test | ✅ SAT | Log search and report generation functional |
| AU-8 | Test | ✅ SAT | NTP sync verified; all components within ±1 second |
| AU-9 | Test | ✅ SAT | Non-ISSO deletion attempt blocked — access denied |
| AU-9(2) | Examine, Test | 🟠 OTS-H | F-002 — Hash chain verification not automated |
| AU-10 | Examine | ✅ SAT | Unique IDs; MFA; hash chain all support non-repudiation |
| AU-11 | Test | ✅ SAT | S3 Object Lock verified — deletion attempt blocked |
| AU-12 | Test | ✅ SAT | All components forwarding logs — verified in SIEM |
| AU-13 | Test | ✅ SAT | Bulk access test triggered SIEM alert in 4 minutes |
| AU-14 | Examine | 🟡 OTS-M | F-012 — Privileged session review not documented monthly |
| **AU Summary** | | **13 SAT / 1 OTS-H / 2 OTS-M / 0 OTS-L** | F-002, F-011, F-012 |

---

### 2.4 CA — Assessment, Authorisation, and Monitoring

| Control | Assessment Method | Result | Finding |
|---|---|---|---|
| CA-1 | Examine | ✅ SAT | RMF policy documented |
| CA-2 | Examine | ✅ SAT | This assessment satisfies CA-2 |
| CA-2(1) | Examine | ✅ SAT | Independent SCA engaged and verified |
| CA-3 | Examine | ✅ SAT | All interconnections documented; BAAs reviewed |
| CA-5 | Examine | ✅ SAT | POA&M maintained; monthly review evidenced |
| CA-6 | Examine | ✅ SAT | ATO process documented |
| CA-7 | Examine, Interview | ✅ SAT | Continuous monitoring programme verified operational |
| CA-8 | Examine | 🟡 OTS-M | F-008 — First pen test (no prior baseline) |
| CA-9 | Examine | ✅ SAT | Internal connections documented in SSP |
| **CA Summary** | | **8 SAT / 0 OTS-H / 1 OTS-M / 0 OTS-L** | F-008 |

---

### 2.5 CM — Configuration Management

| Control | Assessment Method | Result | Finding |
|---|---|---|---|
| CM-1 | Examine | ✅ SAT | Configuration management policy current |
| CM-2 | Examine, Test | ✅ SAT | CIS Benchmark compliance verified via Nessus |
| CM-2(2) | Examine | ✅ SAT | AWS SSM and WSUS/RHEL Satellite both operational |
| CM-3 | Examine | ✅ SAT | CAB minutes reviewed; all production changes have CAB record |
| CM-4 | Examine | ✅ SAT | Security impact analysis documented for reviewed changes |
| CM-5 | Test | ✅ SAT | Change access restriction verified |
| CM-6 | Test | ✅ SAT | CIS Level 2 configuration spot-checked on 5 servers — compliant |
| CM-7 | Test | ✅ SAT | Unnecessary services scan — only required services running |
| CM-8 | Examine | ✅ SAT | Asset inventory current including IoT devices |
| CM-9 | Examine | ✅ SAT | Configuration management plan documented |
| CM-10 | Test | ✅ SAT | Software allowlist enforced; unlisted software blocked |
| CM-12 | Examine | ✅ SAT | PHI data flow mapping maintained and current |
| **CM Summary** | | **12 SAT / 0 OTS-H / 0 OTS-M / 0 OTS-L** | No findings |

---

### 2.6 CP — Contingency Planning

| Control | Assessment Method | Result | Finding |
|---|---|---|---|
| CP-1 | Examine | ✅ SAT | Contingency planning policy current |
| CP-2 | Examine | 🟡 OTS-M | F-013 — Plan not updated after AZ architecture change |
| CP-2(1) | Examine | ✅ SAT | Hospital EOP coordination documented |
| CP-3 | Examine | ✅ SAT | Annual downtime drill evidenced |
| CP-4 | Test | ✅ SAT | Annual tabletop and failover test evidenced |
| CP-6 | Examine | ✅ SAT | S3 alternate storage confirmed geographically separated |
| CP-7 | Examine | ✅ SAT | Alternate processing (AWS us-east-2) documented |
| CP-8 | Examine | ✅ SAT | Redundant VPN path documented |
| CP-9 | Examine, Test | ✅ SAT | Backup schedule and encryption verified |
| CP-9(1) | Examine | 🟡 OTS-M | F-006 — Q4 restoration test not completed |
| CP-10 | Test | ✅ SAT | Scenario A (28 sec), Scenario B (11 min) — both within RTO |
| CP-11 | Examine | ✅ SAT | Backup communication path documented |
| CP-13 | Examine | ✅ SAT | Paper-based downtime procedure binder verified current |
| **CP Summary** | | **11 SAT / 0 OTS-H / 2 OTS-M / 0 OTS-L** | F-006, F-013 |

---

### 2.7 IA — Identification and Authentication

| Control | Assessment Method | Result | Finding |
|---|---|---|---|
| IA-1 | Examine | ✅ SAT | IA policy current |
| IA-2 | Test | ✅ SAT | Unique user IDs verified — no shared accounts found |
| IA-2(1) | Test | ✅ SAT | MFA verified on all privileged accounts — 15 of 15 tests passed |
| IA-2(2) | Test | 🟠 OTS-H | F-004 — 4 admin accounts without MFA enrolled |
| IA-2(6) | Examine | ✅ SAT | TOTP app and FIDO2 key both accepted; SMS rejected |
| IA-2(8) | Test | ✅ SAT | Replay attack test — TOTP token rejected after use |
| IA-3 | Examine | ✅ SAT | IoT device certificate authentication verified |
| IA-4 | Examine | ✅ SAT | Identifier management process documented |
| IA-5 | Test | ✅ SAT | Password policy enforced — minimum 15 chars; complexity verified |
| IA-5(1) | Test | ✅ SAT | Password history (24) and 90-day rotation verified |
| IA-6 | Test | ✅ SAT | Password masked in all interfaces tested |
| IA-7 | Examine | ✅ SAT | FIPS 140-2 validation certificates on file |
| IA-8 | Test | ✅ SAT | Patient portal separate authentication scheme verified |
| **IA Summary** | | **12 SAT / 1 OTS-H / 0 OTS-M / 0 OTS-L** | F-004 |

---

### 2.8 IR — Incident Response

| Control | Assessment Method | Result | Finding |
|---|---|---|---|
| IR-1 | Examine | ✅ SAT | IR policy current |
| IR-2 | Examine | ✅ SAT | Annual IR training evidenced |
| IR-3 | Examine, Test | ✅ SAT | Tabletop exercise report found; HIPAA breach scenario included |
| IR-4 | Interview | ✅ SAT | SOC Manager confirmed escalation procedures; verified with SIEM test |
| IR-4(1) | Test | ✅ SAT | Automated SIEM → IR ticket creation verified |
| IR-5 | Examine | ✅ SAT | Continuous SIEM monitoring confirmed |
| IR-6 | Examine, Interview | ✅ SAT | HIPAA breach notification procedures documented; Privacy Officer aware |
| IR-6(1) | Test | ✅ SAT | Test alert triggered ISSO notification in 4 minutes (SLA: 1 hour) |
| IR-7 | Examine | ✅ SAT | IR retainer contract with third-party forensics firm on file |
| IR-8 | Examine | ✅ SAT | IRP current; HIPAA integration confirmed |
| **IR Summary** | | **10 SAT / 0 OTS-H / 0 OTS-M / 0 OTS-L** | No findings — strongest family |

---

### 2.9 SC — System and Communications Protection

| Control | Assessment Method | Result | Finding |
|---|---|---|---|
| SC-1 | Examine | ✅ SAT | Communications security policy current |
| SC-2 | Test | ✅ SAT | Admin functions separated from clinical user functions |
| SC-3 | Test | ✅ SAT | Security function isolation verified |
| SC-4 | Examine | ✅ SAT | Memory clearing between sessions configured |
| SC-5 | Test | ✅ SAT | AWS Shield and WAF rate-limiting verified |
| SC-7 | Test | ✅ SAT | Boundary protection — all non-authorised ports blocked |
| SC-7(3) | Test | ✅ SAT | Only 2 authorised access points confirmed |
| SC-8 | Test | ✅ SAT | TLS enforced on all connections — no plaintext paths found |
| SC-8(1) | Test | 🟠 OTS-H | F-003 — TLS 1.2 on 2 legacy endpoints; weak cipher on IoT |
| SC-10 | Test | ✅ SAT | VPN session timeout confirmed |
| SC-12 | Examine | ✅ SAT | AWS KMS CMK and on-premises HSM both verified |
| SC-13 | Test | ✅ SAT | AES-256 and FIPS 140-2 modules verified |
| SC-17 | Examine | ✅ SAT | PKI certificates current; ACM auto-renewal active |
| SC-18 | Examine | ✅ SAT | Mobile code policy documented |
| SC-20 | Test | ✅ SAT | DNSSEC verified for external-facing domains |
| SC-23 | Test | ✅ SAT | Session tokens; CSRF protection verified |
| SC-28 | Test | ✅ SAT | AES-256 at rest confirmed on all storage locations |
| SC-28(1) | Test | ✅ SAT | CMK verified; deletion attempt blocked (30-day window) |
| SC-39 | Examine | ✅ SAT | Process isolation confirmed |
| **SC Summary** | | **18 SAT / 1 OTS-H / 0 OTS-M / 0 OTS-L** | F-003 |

---

### 2.10 SI — System and Information Integrity

| Control | Assessment Method | Result | Finding |
|---|---|---|---|
| SI-1 | Examine | ✅ SAT | SI policy current |
| SI-2 | Examine | 🟠 OTS-H | F-005 — 3 High CVEs beyond 30-day SLA |
| SI-2(2) | Examine | ✅ SAT | Automated patch tools operational |
| SI-3 | Test | ✅ SAT | EDR verified on all servers and endpoints |
| SI-3(2) | Test | ✅ SAT | AV signature updates verified (hourly) |
| SI-4 | Test | ✅ SAT | SIEM monitoring operational; bulk access test passed |
| SI-4(2) | Examine | ✅ SAT | GuardDuty and SIEM both active |
| SI-4(4) | Test | ✅ SAT | WAF inbound filtering verified; DLP outbound active |
| SI-4(16) | Test | ✅ SAT | SIEM correlation across all sources verified |
| SI-5 | Examine | ✅ SAT | CISA and H-ISAC subscriptions confirmed active |
| SI-6 | Examine | ✅ SAT | Security function testing during maintenance windows evidenced |
| SI-7 | Test | ✅ SAT | FIM deployed and alerting on changes |
| SI-7(1) | Examine, Test | 🟡 OTS-M | F-007 — FIM baseline stale for 2 change tickets |
| SI-10 | Test | ✅ SAT | Input validation verified — SQLi and XSS payloads blocked by app |
| SI-12 | Examine | ✅ SAT | 10-year retention policy; 6-year minimum verified |
| SI-16 | Examine | ✅ SAT | ASLR and DEP enabled on all servers |
| SI-18 | Examine | ✅ SAT | PHI data quality controls documented |
| SI-19 | Examine | ✅ SAT | De-identification procedure documented |
| **SI Summary** | | **16 SAT / 1 OTS-H / 1 OTS-M / 0 OTS-L** | F-005, F-007 |

---

### 2.11 RA — Risk Assessment

| Control | Assessment Method | Result | Finding |
|---|---|---|---|
| RA-1 | Examine | ✅ SAT | Risk assessment policy current |
| RA-2 | Examine | ✅ SAT | FIPS 199 categorisation (HIGH) documented |
| RA-3 | Examine | 🟡 OTS-M | F-014 — Annual assessment 6 weeks overdue |
| RA-3(1) | Examine | ✅ SAT | Supply chain risk assessment evidenced |
| RA-5 | Examine, Test | 🟠 OTS-H | F-005 — Also linked here; 3 High CVEs open |
| RA-5(2) | Examine | ✅ SAT | Automated NVD/CVE feed integration verified |
| RA-5(5) | Test | ✅ SAT | Credentialed scans verified producing full results |
| RA-7 | Examine | ✅ SAT | Risk response documented; POA&M entries created |
| RA-9 | Examine | ✅ SAT | PHI subsystems identified as critical |
| RA-10 | Examine | ✅ SAT | Quarterly threat hunting exercises documented |
| **RA Summary** | | **7 SAT / 1 OTS-H / 1 OTS-M / 0 OTS-L** | F-005 (shared), F-014 |

---

### 2.12 Remaining Families Summary

| Family | Controls | SAT | OTS-H | OTS-M | OTS-L | Findings |
|---|---|---|---|---|---|---|
| MA — Maintenance | 6 | 6 | 0 | 0 | 0 | None |
| MP — Media Protection | 8 | 8 | 0 | 0 | 0 | None |
| PE — Physical and Environmental | 9 | 8 | 0 | 0 | 1 | F-015 (visitor log) |
| PL — Planning | 4 | 4 | 0 | 0 | 0 | None |
| PM — Program Management | 9 | 9 | 0 | 0 | 0 | None |
| PS — Personnel Security | 9 | 9 | 0 | 0 | 0 | None |
| PT — PII Processing | 8 | 7 | 0 | 1 | 0 | F-010 (IoT BAA gaps) |
| SA — System Acquisition | 11 | 11 | 0 | 0 | 0 | None |
| SR — Supply Chain Risk | 8 | 8 | 0 | 0 | 0 | None |

---

## Section 3 — Overall Results Summary

### 3.1 Control Determination by Family

| Family | Controls | SAT | OTS-H | OTS-M | OTS-L |
|---|---|---|---|---|---|
| AC | 23 | 22 | 1 | 0 | 1 |
| AT | 6 | 4 | 0 | 1 | 1 |
| AU | 16 | 13 | 1 | 2 | 0 |
| CA | 9 | 8 | 0 | 1 | 0 |
| CM | 12 | 12 | 0 | 0 | 0 |
| CP | 13 | 11 | 0 | 2 | 0 |
| IA | 13 | 12 | 1 | 0 | 0 |
| IR | 10 | 10 | 0 | 0 | 0 |
| MA | 6 | 6 | 0 | 0 | 0 |
| MP | 8 | 8 | 0 | 0 | 0 |
| PE | 9 | 8 | 0 | 0 | 1 |
| PL | 4 | 4 | 0 | 0 | 0 |
| PM | 9 | 9 | 0 | 0 | 0 |
| PS | 9 | 9 | 0 | 0 | 0 |
| PT | 8 | 7 | 0 | 1 | 0 |
| RA | 10 | 7 | 1 | 1 | 0 |
| SA | 11 | 11 | 0 | 0 | 0 |
| SC | 19 | 18 | 1 | 0 | 0 |
| SI | 18 | 16 | 1 | 1 | 0 |
| SR | 8 | 8 | 0 | 0 | 0 |
| **TOTAL** | **221** | **198** | **5** | **9** | **4** |

### 3.2 ATO Recommendation

**The SCA recommends the AO grant Authority to Operate (ATO)** for the NEXUS Electronic Health Records System, subject to:
- F-004 (MFA enrolment) remediated within 7 days — prior to ATO grant
- All High findings (F-001, F-002, F-003, F-005) remediated within 30 days of ATO grant
- All Medium and Low findings tracked in POA&M with monthly ISSO reporting to AO
- Annual reassessment in 2026

---

## Section 4 — GitHub Portfolio Integration

### Repository Structure

```
nexus-ehr-rmf/
├── 05-assess/
│   ├── README.md                         ← Step 5 overview
│   ├── security-assessment-plan.md       ← SAP — NEXUS-RMF-SAP-001
│   ├── sar-findings-summary.md           ← SAR Findings Summary (Ref 6)
│   ├── security-assessment-report.md     ← Full SAR — NEXUS-RMF-SAR-001
│   └── assessment-test-results.md        ← Detailed test evidence
```

### Upload Instructions

| Type this in GitHub filename box | Paste content from |
|---|---|
| `05-assess/README.md` | Step 5 README |
| `05-assess/security-assessment-plan.md` | SAP document |
| `05-assess/sar-findings-summary.md` | SAR Findings Summary (Ref 6) |
| `05-assess/security-assessment-report.md` | This document |

### Commit Messages

```
Step 5: Add Security Assessment Plan (SAP) — NEXUS EHR
Step 5: Add SAR Findings Summary (Ref 6) — 18 findings — NEXUS EHR
Step 5: Add Security Assessment Report (SAR) — 221 controls assessed — NEXUS EHR
```

### Root README Update

```markdown
| 5 | [Assess](./05-assess/) | ✅ Complete | SAR · Ref 6 Findings Summary · 18 findings · ATO recommended |
```

---

*Document Reference: NEXUS-RMF-SAR-001 | Version 1.0 — Final | Classification: Internal — Controlled*
*NEXUS EHR is a fictional system created for a GRC portfolio demonstration.*
