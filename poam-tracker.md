# Plan of Action and Milestones (POA&M) Tracker — Reference 7
## NEXUS Electronic Health Records System | Step 6 — Authorise

| Field | Detail |
|---|---|
| **Document Reference** | NEXUS-RMF-POAM-001 — **Reference 7** |
| **Document Type** | Plan of Action and Milestones (POA&M) Tracker |
| **System Name** | NEXUS Electronic Health Records System |
| **Version** | 1.2 — Current |
| **Classification** | Internal — Controlled |
| **ISSO** | [Name], Lead Information Security Analyst |
| **System Owner** | [Name], Director of Clinical Informatics |
| **Authorising Official** | [Name], Chief Information Officer |
| **ATO Grant Date** | 2026 |
| **POA&M Initiated** | 2026 (post-SAR) |
| **Last Updated** | 2026 |
| **Next Monthly Review** | [Date] |
| **References** | NIST SP 800-37 Rev 2; SAR Findings Summary (NEXUS-RMF-SAR-001); Risk Register (NEXUS-RMF-RA-002); OMB Memorandum M-02-01 |

---

## POA&M Purpose and Authority

The Plan of Action and Milestones (POA&M) is a formal management tool used to document the corrective actions planned for security weaknesses and deficiencies identified during the Step 5 security assessment. It is a living document maintained by the ISSO and reviewed monthly with the System Owner.

**Regulatory basis:**
- NIST SP 800-37 Rev 2 requires POA&M as part of Step 6 (Authorise) and Step 7 (Monitor)
- HIPAA Security Rule §164.308(a)(8) requires periodic evaluation and corrective action
- OMB Memorandum M-02-01 established POA&M as a federal requirement for security programmes

**ISSO responsibility:** The ISSO is responsible for maintaining this tracker, assigning items to owners, tracking milestones, and reporting monthly status to the AO. No POA&M item may be closed without documented evidence of remediation reviewed by the ISSO.

---

## POA&M Status Definitions

| Status | Definition |
|---|---|
| 🔴 **Overdue** | Target date has passed without completion; escalation required |
| 🟠 **Open** | Not yet started; within target date |
| 🔄 **In Progress** | Remediation activities underway; milestone achieved or on track |
| ✅ **Closed** | Remediation complete; evidence reviewed and accepted by ISSO |
| ⏸️ **Deferred** | AO-approved delay with revised target date; compensating control in place |
| ➕ **Risk Accepted** | AO formally accepted residual risk; item remains open with monitoring |

---

## Severity Definitions and Deadlines

| Severity | Finding Score | Remediation SLA | Escalation |
|---|---|---|---|
| 🔴 Critical | OTS-C | Immediate — system shutdown if unmitigated | AO + ISSO immediate |
| 🟠 High | OTS-H | 30 days from ATO grant date | AO notification within 24 hours of finding |
| 🟡 Medium | OTS-M | 90 days from ATO grant date | ISSO tracks; monthly AO report |
| 🟢 Low | OTS-L | 180 days from ATO grant date | Quarterly AO summary |

---

## POA&M Tracker — All 18 Items

---

### P-001 — Account Deprovisioning Automation Failure

| Field | Detail |
|---|---|
| **POA&M ID** | P-001 |
| **Finding Ref** | F-001 (SAR) |
| **Severity** | 🟠 High |
| **Control** | AC-2 — Account Management |
| **Finding Summary** | 3 terminated employee accounts were not disabled within the 24-hour SLA due to a silent failure in the ServiceNow–Active Directory integration. Two accounts had PHI access during the exposure window of 3–7 days. No evidence of unauthorised access was found, but the vulnerability existed. |
| **System / Component Affected** | Active Directory; ServiceNow HR-IT integration; All NEXUS PHI access roles |
| **Weakness Type** | Process failure — automation gap |
| **Risk Level if Unmitigated** | High — orphaned PHI-access accounts create insider threat and external attacker opportunity |
| **HIPAA Relevance** | §164.308(a)(3)(ii)(C) — Termination Procedures |
| **Assigned Owner** | [System Administrator Name] |
| **ISSO Oversight** | [ISSO Name] |
| **Resources Required** | SA time (8 hours); ServiceNow admin access; no budget required |

**Milestones:**

| Milestone | Description | Target Date | Actual Date | Status |
|---|---|---|---|---|
| M1 | Diagnose root cause of ServiceNow–AD integration failure | ATO + 5 days | [Date] | ✅ Closed |
| M2 | Repair integration and test with 3 synthetic departure records | ATO + 10 days | [Date] | ✅ Closed |
| M3 | Implement daily automated report of accounts not disabled within 24 hours | ATO + 15 days | [Date] | 🔄 In Progress |
| M4 | ISSO reviews daily report for 30 consecutive days to verify reliability | ATO + 30 days | — | 🟠 Open |
| M5 | Process documented; deprovisioning SLA included in quarterly access review metrics | ATO + 30 days | — | 🟠 Open |

**Overall Status:** 🔄 In Progress
**% Complete:** 40%
**Next Action:** SA to deliver daily report by [date]; ISSO to begin 30-day monitoring
**Compensating Control:** Manual ISSO review of all departures during repair period

---

### P-002 — Audit Log Hash Chain Verification Not Automated

| Field | Detail |
|---|---|
| **POA&M ID** | P-002 |
| **Finding Ref** | F-002 (SAR) |
| **Severity** | 🟠 High |
| **Control** | AU-9(2) — Protection of Audit Information — Separate Storage |
| **Finding Summary** | SHA-256 hash chain is correctly implemented and intact, but the SIEM alert on hash chain failure was not configured. Verification runs manually weekly — up to 7 days of undetected log tampering possible in a failure scenario. |
| **System / Component Affected** | Audit Logging Server; SIEM |
| **Weakness Type** | Implementation gap — SIEM integration not completed |
| **Risk Level if Unmitigated** | High — 7-day detection gap for log tampering could conceal a breach |
| **HIPAA Relevance** | §164.312(b) — Audit Controls |
| **Assigned Owner** | [SOC Manager Name] |
| **ISSO Oversight** | [ISSO Name] |
| **Resources Required** | SOC/SIEM admin time (6 hours); no additional tooling required |

**Milestones:**

| Milestone | Description | Target Date | Actual Date | Status |
|---|---|---|---|---|
| M1 | Write hash chain verification script with JSON output parseable by SIEM | ATO + 7 days | [Date] | ✅ Closed |
| M2 | Configure SIEM job to run hash verification every 4 hours | ATO + 10 days | — | 🔄 In Progress |
| M3 | Configure SIEM alert — hash failure → ISSO notification within 15 minutes | ATO + 12 days | — | 🔄 In Progress |
| M4 | Test automated alert end-to-end: simulate hash failure → verify SIEM alert fires | ATO + 14 days | — | 🟠 Open |
| M5 | Document configuration; update SSP AU-9(2) implementation statement | ATO + 20 days | — | 🟠 Open |

**Overall Status:** 🔄 In Progress
**% Complete:** 20%
**Next Action:** SOC to complete SIEM job configuration by [date]
**Compensating Control:** Manual weekly verification continues until automation confirmed

---

### P-003 — Legacy TLS 1.2 on Clinical Endpoints and Weak IoT Cipher

| Field | Detail |
|---|---|
| **POA&M ID** | P-003 |
| **Finding Ref** | F-003 (SAR) |
| **Severity** | 🟠 High |
| **Control** | SC-8(1) — Transmission Confidentiality — Cryptographic Protection |
| **Finding Summary** | Two legacy Windows 10 workstations do not support TLS 1.3 — connecting to NEXUS via TLS 1.2 only. One IoT network connection uses a weak cipher (TLS_RSA_WITH_AES_128_CBC_SHA). TLS 1.2 is not a broken protocol, but the NEXUS SSP requires TLS 1.3 preferred and consistent cipher enforcement. |
| **System / Component Affected** | 2 legacy admin workstations (Windows 10); IoT VLAN termination point |
| **Weakness Type** | Configuration gap — legacy hardware; vendor default IoT config |
| **Risk Level if Unmitigated** | High — TLS_RSA cipher on IoT lacks forward secrecy; weak cipher in PHI transmission path |
| **HIPAA Relevance** | §164.312(e)(2)(ii) — Encryption and Decryption |
| **Assigned Owner** | [System Administrator Name] |
| **ISSO Oversight** | [ISSO Name] |
| **Resources Required** | Hardware budget: 2 workstations (~$2,400); SA configuration time (4 hours); IoT VLAN config (2 hours) |

**Milestones:**

| Milestone | Description | Target Date | Actual Date | Status |
|---|---|---|---|---|
| M1 | Procure 2 replacement workstations (Windows 11) | ATO + 7 days | [Date] | ✅ Closed |
| M2 | Replace legacy workstations; verify TLS 1.3 connectivity to NEXUS | ATO + 21 days | — | 🔄 In Progress |
| M3 | Reconfigure IoT VLAN termination — enforce AEAD cipher suites only | ATO + 14 days | — | 🔄 In Progress |
| M4 | Re-run sslyze TLS scan across all endpoints — verify 100% TLS 1.3 capable | ATO + 25 days | — | 🟠 Open |
| M5 | Update SSP SC-8(1) implementation statement; confirm A+ SSL Labs rating | ATO + 30 days | — | 🟠 Open |

**Overall Status:** 🔄 In Progress
**% Complete:** 20%
**Next Action:** SA to deploy replacement workstations; IoT cipher reconfiguration by [date]
**Compensating Control:** Legacy endpoints identified and network access logged; no TLS 1.0/1.1 in use

---

### P-004 — MFA Not Enrolled for 4 Billing Accounts

| Field | Detail |
|---|---|
| **POA&M ID** | P-004 |
| **Finding Ref** | F-004 (SAR) |
| **Severity** | 🟠 High |
| **Control** | IA-2(2) — MFA — Non-Privileged Accounts |
| **Finding Summary** | 4 billing user accounts were provisioned during a legacy module migration without MFA enrolment. SCA verified successful NEXUS login using username and password only. ATO condition: MFA enrolment must be completed before ATO is granted. |
| **System / Component Affected** | 4 billing user accounts; Azure AD Conditional Access; NEXUS application |
| **Weakness Type** | Process gap — provisioning checklist did not include MFA verification |
| **Risk Level if Unmitigated** | High — PHI-touching accounts accessible with single factor |
| **HIPAA Relevance** | §164.312(d) — Person Authentication |
| **Assigned Owner** | [System Administrator Name] |
| **ISSO Oversight** | [ISSO Name] |
| **Resources Required** | SA time (2 hours); user communication (IT helpdesk); no budget required |

**Milestones:**

| Milestone | Description | Target Date | Actual Date | Status |
|---|---|---|---|---|
| M1 | Contact all 4 users; schedule in-person MFA enrolment sessions | Pre-ATO | [Date] | ✅ Closed |
| M2 | Complete MFA enrolment for all 4 billing accounts | Pre-ATO | [Date] | ✅ **Closed** |
| M3 | Verify Conditional Access policy blocking login without MFA on all 4 accounts | Pre-ATO | [Date] | ✅ **Closed** |
| M4 | Update provisioning checklist — MFA enrolment verification mandatory before account activation | ATO + 7 days | [Date] | ✅ Closed |
| M5 | Add weekly automated Azure AD report of accounts without MFA enrolled | ATO + 14 days | — | 🔄 In Progress |

**Overall Status:** ✅ **Closed (Pre-ATO — ATO condition met)**
**% Complete:** 80% (M5 in progress — administrative improvement)
**Evidence of Closure:** Azure AD MFA status report showing all 4 accounts enrolled; Conditional Access test confirming MFA challenged; submitted to ISSO [Date]
**ATO Condition:** SATISFIED — ATO granted

---

### P-005 — High-Severity CVEs Exceeding 30-Day Remediation SLA

| Field | Detail |
|---|---|
| **POA&M ID** | P-005 |
| **Finding Ref** | F-005 (SAR); also linked to RA-5 |
| **Severity** | 🟠 High |
| **Control** | RA-5 — Vulnerability Monitoring; SI-2 — Flaw Remediation |
| **Finding Summary** | 3 High-severity CVEs (CVSS 7.0–8.9) were found open beyond the 30-day SLA: (1) PostgreSQL privilege escalation via extension (Primary DB); (2) RHEL 9 kernel local privilege escalation (SIEM server); (3) OpenSSL information disclosure (Audit Server). None were confirmed actively exploitable in current config, but no formal risk acknowledgement existed. |
| **System / Component Affected** | Primary DB Server (PostgreSQL CVE); SIEM Server (RHEL kernel CVE); Audit Logging Server (OpenSSL CVE) |
| **Weakness Type** | Process failure — patch SLA not enforced; no escalation mechanism |
| **Risk Level if Unmitigated** | High — 3 unacknowledged High CVEs; privilege escalation paths available |
| **HIPAA Relevance** | §164.308(a)(1)(ii)(A) — Risk Analysis |
| **Assigned Owner** | [System Administrator Name] |
| **ISSO Oversight** | [ISSO Name] |
| **Resources Required** | SA patching time (6 hours per server); maintenance window scheduling; no budget |

**Milestones:**

| Milestone | Description | Target Date | Actual Date | Status |
|---|---|---|---|---|
| M1 | Apply PostgreSQL patch — Primary DB Server | ATO + 5 days | [Date] | ✅ Closed |
| M2 | Apply RHEL 9 kernel patch — SIEM Server | ATO + 5 days | [Date] | ✅ Closed |
| M3 | Apply OpenSSL patch — Audit Logging Server | ATO + 5 days | [Date] | ✅ Closed |
| M4 | Re-scan all 3 servers — verify CVEs resolved in Nessus output | ATO + 7 days | [Date] | ✅ Closed |
| M5 | Implement SIEM alert: High/Critical CVE reaches Day 25 without patch applied | ATO + 20 days | — | 🔄 In Progress |
| M6 | ISSO weekly patch compliance report includes SLA breach flagging | ATO + 25 days | — | 🔄 In Progress |

**Overall Status:** 🔄 In Progress (patches applied; process improvements in progress)
**% Complete:** 67%
**Evidence of Patch Closure (M1–M4):** Nessus re-scan reports showing CVEs resolved; submitted to ISSO [Date]
**Next Action:** SA to complete SIEM Day-25 alert configuration; ISSO to formalise weekly report template

---

### P-006 — Q4 Backup Restoration Test Not Completed

| Field | Detail |
|---|---|
| **POA&M ID** | P-006 |
| **Finding Ref** | F-006 (SAR) |
| **Severity** | 🟡 Medium |
| **Control** | CP-9(1) — System Backup — Testing for Reliability |
| **Finding Summary** | The Q4 quarterly backup restoration test was deferred due to a maintenance window conflict and not rescheduled. Q1, Q2, Q3 tests all passed. The Q4 gap means one quarter passed without verified backup recoverability. The Step 5 assessment itself included a restoration test (3h 42m — PASSED), which provides assurance, but the administrative process gap remains. |
| **System / Component Affected** | AWS Backup Vault; Primary PostgreSQL DB; Restoration test process |
| **Weakness Type** | Process gap — no fixed quarterly schedule enforced |
| **Risk Level if Unmitigated** | Medium — process gap, not a technical failure; backup integrity confirmed during assessment |
| **Assigned Owner** | [DBA Name] |
| **ISSO Oversight** | [ISSO Name] |
| **Resources Required** | DBA time (4 hours per test); isolated test environment (already available) |

**Milestones:**

| Milestone | Description | Target Date | Actual Date | Status |
|---|---|---|---|---|
| M1 | Complete Q4 restoration test (deferred item — now completed during assessment) | ATO + 14 days | [Date] | ✅ Closed (done in assessment) |
| M2 | Document Q4 test result; ISSO sign-off | ATO + 14 days | [Date] | ✅ Closed |
| M3 | Establish fixed quarterly test calendar — dates cannot be deferred without AO approval | ATO + 20 days | — | 🔄 In Progress |
| M4 | Update Contingency Plan to include fixed test schedule with escalation process | ATO + 30 days | — | 🟠 Open |

**Overall Status:** 🔄 In Progress
**% Complete:** 50%
**Evidence:** Assessment restoration test report (3h 42m PASS); submitted to ISSO

---

### P-007 — FIM Baseline Stale After 2 Approved Changes

| Field | Detail |
|---|---|
| **POA&M ID** | P-007 |
| **Finding Ref** | F-007 (SAR) |
| **Severity** | 🟡 Medium |
| **Control** | SI-7(1) — Software Integrity — Automated Integrity Checks |
| **Finding Summary** | 2 approved CAB change tickets were not followed by FIM baseline updates. FIM was generating false-positive alerts that SOC analysts were routinely suppressing, creating risk that genuine alerts were being dismissed. A deliberate SCA modification test was initially suppressed by SOC. |
| **System / Component Affected** | FIM (AIDE) on Primary DB Server and Web/App Servers; SOC alert handling process |
| **Weakness Type** | Process gap — CAB closure does not enforce FIM baseline update |
| **Risk Level if Unmitigated** | Medium — integrity monitoring blind spot; SOC alert fatigue masking real alerts |
| **Assigned Owner** | [System Administrator Name] |
| **ISSO Oversight** | [ISSO Name] |
| **Resources Required** | SA time (3 hours); CAB process update (ISSO-led); no budget |

**Milestones:**

| Milestone | Description | Target Date | Actual Date | Status |
|---|---|---|---|---|
| M1 | Update FIM baseline to reflect 2 outstanding approved changes | ATO + 3 days | [Date] | ✅ Closed |
| M2 | Review all suppressed FIM alerts from past 60 days — confirm none were genuine | ATO + 7 days | [Date] | ✅ Closed |
| M3 | Update CAB closure checklist — FIM baseline update mandatory before ticket closure | ATO + 14 days | — | 🔄 In Progress |
| M4 | SOC training refresh — FIM alert suppression requires ISSO approval | ATO + 21 days | — | 🟠 Open |
| M5 | Verify no suppressed FIM alerts in 30-day post-fix review | ATO + 45 days | — | 🟠 Open |

**Overall Status:** 🔄 In Progress
**% Complete:** 40%

---

### P-008 — No Prior Penetration Test — First Test Completed

| Field | Detail |
|---|---|
| **POA&M ID** | P-008 |
| **Finding Ref** | F-008 (SAR) |
| **Severity** | 🟡 Medium |
| **Control** | CA-8 — Penetration Testing |
| **Finding Summary** | The annual penetration test (CA-8 tailoring addition) had not been previously conducted. The first test was completed as part of the Step 5 assessment — results: no critical or high vulnerabilities. No prior baseline exists for year-over-year comparison. Finding is medium rather than high because the first test was successfully completed. |
| **System / Component Affected** | All NEXUS components (pen test scope) |
| **Weakness Type** | Programme maturity — CA-8 recently added in Step 3 tailoring |
| **Risk Level if Unmitigated** | Medium — lack of prior baseline limits trend analysis |
| **Assigned Owner** | [ISSO Name] |
| **ISSO Oversight** | [ISSM Name] |
| **Resources Required** | Annual pen test budget: ~$15,000–25,000 per year (external firm) |

**Milestones:**

| Milestone | Description | Target Date | Actual Date | Status |
|---|---|---|---|---|
| M1 | Retain results of first pen test as Year 1 baseline | ATO | [Date] | ✅ Closed |
| M2 | Schedule Year 2 pen test — book external firm 3 months in advance | ATO + 30 days | — | 🔄 In Progress |
| M3 | Include pen test scope review in annual SAP development | ATO + annual | — | 🟠 Open |
| M4 | Year 2 pen test completed; Year 1 vs Year 2 comparison analysis | ATO + 12 months | — | 🟠 Open |

**Overall Status:** 🔄 In Progress
**% Complete:** 25%

---

### P-009 — Phishing Simulation — 22% Click Rate

| Field | Detail |
|---|---|
| **POA&M ID** | P-009 |
| **Finding Ref** | F-009 (SAR) |
| **Severity** | 🟡 Medium |
| **Control** | AT-2 — Literacy Training and Awareness; AT-2(2) — Insider Threat Awareness |
| **Finding Summary** | Simulated phishing email mimicking lab results achieved 22% click rate and 8% credential submission rate across 450 NEXUS users. 53% of credential submitters were clinical staff (nurses and junior doctors). Target: <10% click rate. MFA prevented any real credential use, but social engineering vulnerability is above acceptable threshold. |
| **System / Component Affected** | All NEXUS users; clinical staff phishing susceptibility |
| **Weakness Type** | Training gap — clinical-scenario phishing not previously tested |
| **Risk Level if Unmitigated** | Medium — MFA compensates technically; human layer remains exposed |
| **Assigned Owner** | [ISSO Name] / [HR Training Lead] |
| **ISSO Oversight** | [ISSM Name] |
| **Resources Required** | Phishing simulation platform (~$3,000/year); HR training time; ISSO time (8 hours) |

**Milestones:**

| Milestone | Description | Target Date | Actual Date | Status |
|---|---|---|---|---|
| M1 | Identify 36 credential submitters and assign mandatory targeted training | ATO + 14 days | [Date] | ✅ Closed |
| M2 | Deliver targeted phishing-resistant awareness training to 36 users | ATO + 30 days | — | 🔄 In Progress |
| M3 | Add external email warning banner: "This email originated outside Nexus Health System" | ATO + 21 days | — | 🔄 In Progress |
| M4 | Deploy quarterly phishing simulations — clinical scenario focus | ATO + 30 days | — | 🟠 Open |
| M5 | Q2 simulation result: target <15% click rate (improvement milestone) | ATO + 90 days | — | 🟠 Open |
| M6 | Annual simulation target: <10% click rate (full remediation) | ATO + 180 days | — | 🟠 Open |

**Overall Status:** 🔄 In Progress
**% Complete:** 17%

---

### P-010 — Medical IoT BAA Missing for 3 Device Vendors

| Field | Detail |
|---|---|
| **POA&M ID** | P-010 |
| **Finding Ref** | F-010 (SAR) |
| **Severity** | 🟡 Medium |
| **Control** | SA-9 — External System Services; PT-2 — Authority to Process PII |
| **Finding Summary** | 3 medical IoT device vendors whose devices transmit vital signs (PHI) to NEXUS have not executed Business Associate Agreements. BAAs have been requested but vendors have not responded for 90+ days. HIPAA requires BAAs before PHI is processed by a third party. |
| **System / Component Affected** | 3 IoT device vendors; vital signs data flow to NEXUS database |
| **Weakness Type** | Compliance gap — BAA execution delayed; HIPAA exposure |
| **Risk Level if Unmitigated** | Medium-High — HIPAA violation if PHI processed without BAA; OCR exposure |
| **HIPAA Relevance** | §164.308(b)(1) — Business Associate Contracts and Other Arrangements |
| **Assigned Owner** | [Privacy Officer Name] / [Legal Counsel] |
| **ISSO Oversight** | [ISSO Name] |
| **Resources Required** | Legal review time; potential vendor re-procurement if BAA refused |

**Milestones:**

| Milestone | Description | Target Date | Actual Date | Status |
|---|---|---|---|---|
| M1 | Escalate BAA request to vendor C-suite / legal departments | ATO + 5 days | [Date] | ✅ Closed |
| M2 | Vendor 1 BAA executed | ATO + 30 days | — | 🔄 In Progress |
| M3 | Vendor 2 BAA executed | ATO + 30 days | — | 🔄 In Progress |
| M4 | Vendor 3 BAA executed OR device disconnected if BAA refused after 30 days | ATO + 30 days | — | 🟠 Open |
| M5 | BAA requirement added to all future IoT procurement contracts | ATO + 45 days | — | 🟠 Open |
| M6 | BAA register updated; annual review cycle confirmed | ATO + 60 days | — | 🟠 Open |

**Overall Status:** 🔄 In Progress
**% Complete:** 17%
**Escalation Note:** If Vendor 3 does not execute BAA by ATO + 30 days, device must be disconnected from NEXUS pending HIPAA-compliant alternative arrangement.

---

### P-011 — SIEM After-Hours Alert Generating Alert Fatigue

| Field | Detail |
|---|---|
| **POA&M ID** | P-011 |
| **Finding Ref** | F-011 (SAR) |
| **Severity** | 🟡 Medium |
| **Control** | SI-4 — System Monitoring; AU-6(1) — Automated Audit Review |
| **Finding Summary** | The SIEM after-hours PHI access alert generates ~47 alerts per night, of which 94% are legitimate on-call staff. SOC alert fatigue means 3 actual non-on-call accesses were buried in the queue and went uninvestigated. Alert volume makes the rule functionally ineffective. |
| **System / Component Affected** | SIEM correlation rules; SOC alert queue; after-hours PHI access monitoring |
| **Weakness Type** | Configuration gap — SIEM rule not tuned to on-call schedule |
| **Risk Level if Unmitigated** | Medium — genuine after-hours access violations are effectively undetected |
| **Assigned Owner** | [SOC Manager Name] |
| **ISSO Oversight** | [ISSO Name] |
| **Resources Required** | SOC/SIEM admin time (8 hours); on-call schedule integration API development (12 hours) |

**Milestones:**

| Milestone | Description | Target Date | Actual Date | Status |
|---|---|---|---|---|
| M1 | Investigate and remediate 3 uninvestigated non-on-call accesses from assessment period | ATO + 7 days | [Date] | ✅ Closed |
| M2 | Obtain on-call schedule data feed from clinical scheduling system | ATO + 14 days | — | 🔄 In Progress |
| M3 | Integrate on-call schedule into SIEM — update alert rule to exclude on-call staff | ATO + 45 days | — | 🟠 Open |
| M4 | Target: <5 after-hours alerts per night with >95% genuine positive rate | ATO + 60 days | — | 🟠 Open |
| M5 | Validate tuned rule with 30-day observation period | ATO + 90 days | — | 🟠 Open |

**Overall Status:** 🔄 In Progress
**% Complete:** 20%

---

### P-012 — Privileged Session Audit Review Not Documented Monthly

| Field | Detail |
|---|---|
| **POA&M ID** | P-012 |
| **Finding Ref** | F-012 (SAR) |
| **Severity** | 🟡 Medium |
| **Control** | AU-14 — Session Audit; CA-7 — Continuous Monitoring |
| **Finding Summary** | Privileged session audit capture is correctly implemented. However, the ISSO conducted only 3 of 6 expected monthly reviews — alternate months were reviewed informally without documentation. Undocumented reviews cannot be evidenced to future SCAs or regulators. |
| **System / Component Affected** | ISSO process; privileged session audit review workpapers |
| **Weakness Type** | Documentation gap — informal review not formalised |
| **Risk Level if Unmitigated** | Medium — review gaps could miss privileged account misuse; documentation gap is HIPAA risk |
| **Assigned Owner** | [ISSO Name] |
| **ISSO Oversight** | [ISSM Name] |
| **Resources Required** | ISSO time (2 hours/month); review sign-off form template (1 hour to create) |

**Milestones:**

| Milestone | Description | Target Date | Actual Date | Status |
|---|---|---|---|---|
| M1 | Create privileged session review sign-off form template | ATO + 7 days | [Date] | ✅ Closed |
| M2 | Backfill review documentation for 3 informally reviewed months | ATO + 14 days | [Date] | ✅ Closed |
| M3 | Add monthly review to ISSO calendar with mandatory documentation step | ATO + 7 days | [Date] | ✅ Closed |
| M4 | Verify 3 consecutive months of documented reviews post-fix | ATO + 90 days | — | 🟠 Open |

**Overall Status:** 🔄 In Progress
**% Complete:** 75%

---

### P-013 — Contingency Plan Not Updated After AWS Multi-AZ Change

| Field | Detail |
|---|---|
| **POA&M ID** | P-013 |
| **Finding Ref** | F-013 (SAR) |
| **Severity** | 🟡 Medium |
| **Control** | CP-2 — Contingency Plan |
| **Finding Summary** | The Contingency Plan was not updated after NEXUS EC2 instances were deployed across two AWS Availability Zones 4 months prior. Recovery procedures reference single-AZ failover steps that are now inaccurate. Outdated procedures could slow recovery during an incident. |
| **System / Component Affected** | Contingency Plan document; AWS multi-AZ recovery procedures |
| **Weakness Type** | Documentation gap — change management did not trigger CP update |
| **Risk Level if Unmitigated** | Medium — inaccurate recovery procedures extend outage duration |
| **Assigned Owner** | [ISSO Name] / [System Administrator Name] |
| **ISSO Oversight** | [ISSM Name] |
| **Resources Required** | ISSO time (4 hours); SA input (2 hours); no budget |

**Milestones:**

| Milestone | Description | Target Date | Actual Date | Status |
|---|---|---|---|---|
| M1 | Update Contingency Plan — revise all recovery procedures for multi-AZ architecture | ATO + 20 days | — | 🔄 In Progress |
| M2 | ISSO reviews and approves updated Contingency Plan | ATO + 25 days | — | 🟠 Open |
| M3 | Update CAB process — infrastructure changes trigger mandatory CP review | ATO + 30 days | — | 🟠 Open |
| M4 | Tabletop exercise using updated CP to validate accuracy | ATO + 60 days | — | 🟠 Open |

**Overall Status:** 🔄 In Progress
**% Complete:** 0% (M1 in draft)

---

### P-014 — Annual Risk Assessment Completed 6 Weeks Late

| Field | Detail |
|---|---|
| **POA&M ID** | P-014 |
| **Finding Ref** | F-014 (SAR) |
| **Severity** | 🟡 Medium |
| **Control** | RA-3 — Risk Assessment |
| **Finding Summary** | The annual risk assessment was completed 6 weeks past the annual anniversary date. HIPAA requires risk analysis on a reasonable and appropriate basis. A 6-week gap, while not egregious, creates a period without a current formal risk assessment. |
| **System / Component Affected** | ISSO annual programme calendar; risk assessment scheduling |
| **Weakness Type** | Process gap — no advance scheduling mechanism |
| **Risk Level if Unmitigated** | Medium — regulatory gap; OCR may view late assessments as programme weakness |
| **Assigned Owner** | [ISSO Name] |
| **ISSO Oversight** | [ISSM Name] |
| **Resources Required** | ISSO calendar management; no budget |

**Milestones:**

| Milestone | Description | Target Date | Actual Date | Status |
|---|---|---|---|---|
| M1 | Schedule next annual risk assessment to BEGIN 6 weeks before due date | ATO + 14 days | [Date] | ✅ Closed |
| M2 | Add risk assessment initiation to ISSO annual programme calendar | ATO + 14 days | [Date] | ✅ Closed |
| M3 | Next annual risk assessment completed on time | ATO + 12 months | — | 🟠 Open |

**Overall Status:** ✅ **Closed (Process Fix)**
**% Complete:** 67% (M3 pending next year)

---

### P-015 — Visitor Access Log — 2 Missing Departure Times

| Field | Detail |
|---|---|
| **POA&M ID** | P-015 |
| **Finding Ref** | F-015 (SAR) |
| **Severity** | 🟢 Low |
| **Control** | PE-8 — Visitor Access Records |
| **Finding Summary** | 2 entries in the data centre visitor access log were missing departure times. Visitor identities and purpose were recorded; only departure time was absent. CCTV confirmed both visits were legitimate. |
| **System / Component Affected** | Site A data centre visitor log; facilities staff process |
| **Weakness Type** | Documentation gap — manual log entry error |
| **Risk Level if Unmitigated** | Low — minor documentation gap; no security impact identified |
| **Assigned Owner** | [Facilities Manager Name] |
| **ISSO Oversight** | [ISSO Name] |
| **Resources Required** | Facilities staff briefing (30 minutes); no budget |

**Milestones:**

| Milestone | Description | Target Date | Actual Date | Status |
|---|---|---|---|---|
| M1 | Brief data centre reception staff — departure time mandatory on visitor log | ATO + 14 days | [Date] | ✅ Closed |
| M2 | Add visual prompt to visitor log form ("Departure time — REQUIRED") | ATO + 14 days | [Date] | ✅ Closed |
| M3 | ISSO review of visitor log at next quarterly physical security review | ATO + 90 days | — | 🟠 Open |

**Overall Status:** ✅ **Closed (administratively)**
**% Complete:** 67% (M3 is routine quarterly review)

---

### P-016 — Annual Training — 3 Temporary Staff Not Completed

| Field | Detail |
|---|---|
| **POA&M ID** | P-016 |
| **Finding Ref** | F-016 (SAR) |
| **Severity** | 🟢 Low |
| **Control** | AT-2 — Literacy Training and Awareness; AT-4 — Training Records |
| **Finding Summary** | 3 temporary staff (2 agency nurses, 1 admin locum) had not completed annual security awareness training. Their accounts were active. Temporary staff training was tracked in agency HR systems not integrated with NEXUS LMS. |
| **System / Component Affected** | LMS training tracking; temporary staff onboarding process |
| **Weakness Type** | Process gap — temporary staff not included in NEXUS LMS |
| **Risk Level if Unmitigated** | Low — 3 users; gap in training coverage; temporary roles are lower-risk than permanent clinical staff |
| **Assigned Owner** | [HR Training Lead] / [ISSO Name] |
| **ISSO Oversight** | [ISSO Name] |
| **Resources Required** | HR process update; LMS guest account capability (may need IT support, 2 hours) |

**Milestones:**

| Milestone | Description | Target Date | Actual Date | Status |
|---|---|---|---|---|
| M1 | Enrol 3 temporary staff in NEXUS LMS; assign annual training | ATO + 7 days | [Date] | ✅ Closed |
| M2 | All 3 temporary staff complete annual training | ATO + 21 days | — | 🔄 In Progress |
| M3 | Update temporary staff onboarding checklist — LMS enrolment before account activation | ATO + 30 days | — | 🟠 Open |
| M4 | Account activation process updated — training completion is a gate | ATO + 45 days | — | 🟠 Open |

**Overall Status:** 🔄 In Progress
**% Complete:** 25%

---

### P-017 — Warning Banner Missing from Admin Console

| Field | Detail |
|---|---|
| **POA&M ID** | P-017 |
| **Finding Ref** | F-017 (SAR) |
| **Severity** | 🟢 Low |
| **Control** | AC-8 — System Use Notification |
| **Finding Summary** | The HIPAA system use notification banner is present on the main clinical interface and patient portal but absent from the NEXUS admin console (used exclusively by System Administrators). All SA users have signed acceptable use agreements, but the technical control is absent on this interface. |
| **System / Component Affected** | NEXUS admin console login page |
| **Weakness Type** | Implementation gap — banner not deployed to admin interface |
| **Risk Level if Unmitigated** | Low — SA users are already bound by signed AUP; technical gap is minor |
| **Assigned Owner** | [System Administrator Name] |
| **ISSO Oversight** | [ISSO Name] |
| **Resources Required** | SA development/config time (1 hour); no budget |

**Milestones:**

| Milestone | Description | Target Date | Actual Date | Status |
|---|---|---|---|---|
| M1 | Add HIPAA warning banner to admin console login screen | ATO + 30 days | — | 🔄 In Progress |
| M2 | Screenshot evidence of banner; submitted to ISSO for closure | ATO + 35 days | — | 🟠 Open |

**Overall Status:** 🔄 In Progress
**% Complete:** 0% (M1 scheduled)

---

### P-018 — Removable Media Policy Not in Annual Training

| Field | Detail |
|---|---|
| **POA&M ID** | P-018 |
| **Finding Ref** | F-018 (SAR) |
| **Severity** | 🟢 Low |
| **Control** | MP-7 — Media Use; AT-3 — Role-Based Training |
| **Finding Summary** | USB ports are technically disabled on clinical endpoints via GPO, which is the primary control. However, the annual security awareness training does not include a removable media policy module. Staff are not formally trained on the prohibition. |
| **System / Component Affected** | Annual security awareness training content |
| **Weakness Type** | Training gap — procedural layer absent; technical control compensates |
| **Risk Level if Unmitigated** | Low — GPO USB disable is the primary control; training is the procedural supplement |
| **Assigned Owner** | [HR Training Lead] / [ISSO Name] |
| **ISSO Oversight** | [ISSO Name] |
| **Resources Required** | Training content development (2 hours); no budget |

**Milestones:**

| Milestone | Description | Target Date | Actual Date | Status |
|---|---|---|---|---|
| M1 | Develop 5-minute removable media policy training module | ATO + 90 days | — | 🟠 Open |
| M2 | Include module in next annual training cycle | ATO + 180 days | — | 🟠 Open |

**Overall Status:** 🟠 Open
**% Complete:** 0%

---

## POA&M Summary Dashboard — All Items

| ID | Finding | Severity | Control | Owner | Status | Target | % Done |
|---|---|---|---|---|---|---|---|
| P-001 | Account deprovisioning automation | 🟠 High | AC-2 | SA | 🔄 In Progress | ATO+30 | 40% |
| P-002 | Hash chain verification not automated | 🟠 High | AU-9(2) | SOC | 🔄 In Progress | ATO+30 | 20% |
| P-003 | Legacy TLS 1.2 / weak IoT cipher | 🟠 High | SC-8(1) | SA | 🔄 In Progress | ATO+30 | 20% |
| P-004 | MFA missing for 4 billing accounts | 🟠 High | IA-2(2) | SA | ✅ **Closed** | Pre-ATO | 80% |
| P-005 | 3 High CVEs beyond 30-day SLA | 🟠 High | RA-5/SI-2 | SA | 🔄 In Progress | ATO+30 | 67% |
| P-006 | Q4 backup restoration test missing | 🟡 Medium | CP-9(1) | DBA | 🔄 In Progress | ATO+90 | 50% |
| P-007 | FIM baseline stale — 2 changes | 🟡 Medium | SI-7(1) | SA | 🔄 In Progress | ATO+45 | 40% |
| P-008 | No prior pen test — first baseline | 🟡 Medium | CA-8 | ISSO | 🔄 In Progress | ATO+30 | 25% |
| P-009 | 22% phishing click rate | 🟡 Medium | AT-2 | ISSO/HR | 🔄 In Progress | ATO+180 | 17% |
| P-010 | IoT BAA missing — 3 vendors | 🟡 Medium | SA-9/PT-2 | CPO/Legal | 🔄 In Progress | ATO+30 | 17% |
| P-011 | SIEM after-hours alert fatigue | 🟡 Medium | SI-4 | SOC | 🔄 In Progress | ATO+90 | 20% |
| P-012 | Privileged session review undocumented | 🟡 Medium | AU-14 | ISSO | 🔄 In Progress | ATO+90 | 75% |
| P-013 | CP not updated after AZ change | 🟡 Medium | CP-2 | ISSO/SA | 🔄 In Progress | ATO+60 | 0% |
| P-014 | Risk assessment 6 weeks late | 🟡 Medium | RA-3 | ISSO | ✅ **Closed** | ATO+14 | 67% |
| P-015 | Visitor log — 2 missing departures | 🟢 Low | PE-8 | Facilities | ✅ **Closed** | ATO+14 | 67% |
| P-016 | 3 temp staff missing training | 🟢 Low | AT-2 | HR/ISSO | 🔄 In Progress | ATO+45 | 25% |
| P-017 | Banner missing from admin console | 🟢 Low | AC-8 | SA | 🔄 In Progress | ATO+60 | 0% |
| P-018 | Removable media not in training | 🟢 Low | MP-7 | HR/ISSO | 🟠 Open | ATO+180 | 0% |

---

## Monthly POA&M Review Record

| Review Month | Items Open | Items Closed | Items Overdue | Reviewed By | AO Notified |
|---|---|---|---|---|---|
| Month 1 (ATO grant) | 18 | 0 | 0 | ISSO | ✅ |
| Month 2 | 15 | 3 (P-004, P-014, P-015) | 0 | ISSO | ✅ |
| Month 3 | 15 | 3 | 0 | ISSO | — (no changes) |
| Month 4 | TBD | TBD | TBD | ISSO | TBD |

---

## Escalation and Governance

### Overdue Item Escalation Process

| Days Overdue | Action | Escalation To |
|---|---|---|
| 1–7 days | ISSO contacts owner for status update | Item owner |
| 8–14 days | ISSO escalates to System Owner; revised plan required | System Owner |
| 15–30 days | ISSO escalates to AO; formal risk acceptance or emergency remediation | AO |
| 30+ days | AO makes formal risk acceptance decision; may result in ATO conditions or DATO | AO |

### ATO Conditions — Status

| Condition | Requirement | Status |
|---|---|---|
| Pre-ATO condition | F-004 (MFA) remediated before ATO grant | ✅ SATISFIED |
| ATO condition 1 | P-001, P-002, P-003, P-005 remediated within 30 days | 🔄 In Progress |
| ATO condition 2 | All POA&M items tracked monthly; report to AO | ✅ Active |
| ATO condition 3 | Next annual reassessment scheduled for 2026 | ✅ Scheduled |

---

## Closure Evidence Requirements

For each POA&M item to be marked CLOSED by the ISSO, the following evidence must be submitted and reviewed:

| Control Family | Required Evidence |
|---|---|
| Access Control (AC) | Screenshot or export showing control implementation; test result if applicable |
| Audit (AU) | SIEM configuration export; test result demonstrating expected behaviour |
| Training (AT) | LMS completion report; training content showing updated module |
| Contingency Planning (CP) | Updated document; test result; DBA sign-off |
| Identification/Auth (IA) | Azure AD MFA status report; login test result |
| Physical (PE) | Updated procedure; sign-off from Facilities Manager |
| Risk Assessment (RA) | Completed risk assessment document; scheduling calendar |
| System Integrity (SI) | FIM baseline snapshot; CAB checklist update; patch scan report |
| Comms Protection (SC) | TLS scan output; cipher suite configuration |

---

## Approval and Sign-Off

| Role | Name | Signature | Date |
|---|---|---|---|
| ISSO (POA&M Manager) | [Chioma Otteh] | _________________________ | 2026 |
| System Owner | [Jack Taylor] | _________________________ | 2026 |
| **Authorising Official** | **[Ben Jackson| _________________________ | **2026** |

---

*Document Reference: NEXUS-RMF-POAM-001 — Reference 7 | Version 1.2 | Classification: Internal — Controlled*
*NEXUS EHR is a fictional system created for a GRC portfolio demonstration. All names, data, and system details are illustrative only.*
