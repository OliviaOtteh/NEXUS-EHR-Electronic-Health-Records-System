# SAR Findings Summary — Reference 6
## NEXUS Electronic Health Records System | Step 5 — Security Assessment

| Field | Detail |
|---|---|
| **Document Reference** | NEXUS-RMF-SAR-001 — **Reference 6** |
| **Document Type** | Security Assessment Report — Findings Summary |
| **System Name** | NEXUS Electronic Health Records System |
| **Version** | 1.0 — Final |
| **Classification** | Internal — Controlled — Restricted Distribution |
| **Assessment Period** | 2025 (9-week assessment) |
| **Assessor** | [SCA Name / Firm] — Independent |
| **Prepared By** | [Lead SCA Name] |
| **Submitted To** | [AO Name], Chief Information Officer |
| **Date** | 2025 |
| **References** | NIST SP 800-53A Rev 5; NIST SP 800-37 Rev 2; NEXUS SSP (NEXUS-RMF-SSP-001) |

---

## Executive Summary

The Security Control Assessor (SCA) conducted a full independent assessment of the **221 security and privacy controls** selected for the NEXUS Electronic Health Records System between [Start Date] and [End Date] 2025. The assessment used all three NIST SP 800-53A methods — **Examine**, **Interview**, and **Test** — including a full external and internal penetration test and a phishing simulation exercise targeting clinical staff.

### Overall Assessment Determination

```
╔══════════════════════════════════════════════════════════════════╗
║          NEXUS EHR — ASSESSMENT RESULT OVERVIEW                  ║
╠══════════════════════════════════════════════════════════════════╣
║  Controls Assessed:              221                             ║
║  Controls Satisfied (SAT):       198  (89.6%)                   ║
║  Controls Other Than Satisfied:   23  (10.4%)                   ║
║                                                                  ║
║  Total Findings Raised:           18                             ║
║    🔴 Critical:                    0                             ║
║    🟠 High:                        5  — Remediate in 30 days    ║
║    🟡 Medium:                      9  — Remediate in 90 days    ║
║    🟢 Low:                         4  — Remediate in 180 days   ║
╠══════════════════════════════════════════════════════════════════╣
║  Penetration Test Result: No critical vulnerabilities found      ║
║  Phishing Simulation:     22% click rate — training recommended  ║
║  Backup Restoration Test: PASSED — RTO 3h 42m (within 4hr SLA) ║
╠══════════════════════════════════════════════════════════════════╣
║  SCA RECOMMENDATION:  AUTHORISE TO OPERATE                       ║
║  Subject to remediation of High findings within 30 days and      ║
║  POA&M tracking of all Medium/Low findings.                      ║
╚══════════════════════════════════════════════════════════════════╝
```

### SCA Statement

> *"NEXUS demonstrates a materially strong security posture appropriate for a HIGH-impact system processing PHI and PII in a multi-site healthcare environment. The 198 controls assessed as Satisfied represent a comprehensive and largely effective implementation of the NIST SP 800-53 Rev 5 HIGH baseline, with HIPAA-specific enhancements appropriately applied. The 18 findings identified are consistent with what is expected in a mature programme — no control family was found to be entirely absent or systematically ineffective. The SCA recommends the AO grant Authority to Operate conditional on High findings being remediated within 30 days and tracked in the POA&M."*
>
> — [Lead SCA Name], [Assessor Firm], 2025

---

## Assessment Statistics

| Metric | Value |
|---|---|
| Total controls assessed | 221 |
| Controls found Satisfied (SAT) | 198 (89.6%) |
| Controls found Other Than Satisfied | 23 (10.4%) |
| Total findings | 18 |
| High findings | 5 |
| Medium findings | 9 |
| Low findings | 4 |
| Critical findings | 0 |
| Controls with multiple findings | 3 |
| Penetration test — critical/high exploitable vulnerabilities | 0 |
| Penetration test — medium findings | 3 |
| Phishing simulation — click rate | 22% |
| Phishing simulation — credential submission rate | 8% |
| Backup restoration test — result | PASSED |
| Backup restoration test — actual RTO | 3 hours 42 minutes |
| MFA bypass test — result | FAILED (MFA held) |
| Bulk PHI access detection test — result | PASSED (SIEM alerted in 4 minutes) |

---

## Findings Summary — All 18 Findings

### 🟠 HIGH FINDINGS (5)

---

#### F-001 — Account Deprovisioning Delay

| Field | Detail |
|---|---|
| **Finding ID** | F-001 |
| **Severity** | 🟠 High |
| **Control** | AC-2 — Account Management |
| **Assessment Method** | Examine (Active Directory account audit); Test (deprovisioning timing verification) |
| **Finding Title** | Terminated Employee Accounts Not Disabled Within 24-Hour SLA |
| **Finding Description** | During examination of the Active Directory account audit, the SCA identified 3 accounts belonging to former employees that remained active beyond the 24-hour deprovisioning SLA. The accounts were disabled 3–7 days after departure. Two accounts belonged to clinical staff with PHI access; one belonged to an administrative user. No evidence of unauthorised access was found during the exposure window, but the accounts were vulnerable during that period. |
| **Evidence** | Active Directory account last login and disable timestamps; HR departure notification records; NEXUS access logs for the exposure period |
| **HIPAA Relevance** | HIPAA §164.308(a)(3)(ii)(C) — Termination Procedures: covered entities must implement procedures for terminating access |
| **Risk Rating** | High — two accounts had PHI access; vulnerability window of 3–7 days |
| **Root Cause** | HR-to-IT deprovisioning automation failed silently for 3 departure records during a system integration issue with ServiceNow |
| **Recommendation** | (1) Repair HR-IT automation integration immediately; (2) Add daily automated report of accounts not disabled within 24 hours of HR departure record; (3) ISSO reviews report daily until automation is verified reliable |
| **Responsible Party** | ISSO / System Administrator |
| **POA&M Ref** | P-001 |
| **Target Remediation** | 30 days |

---

#### F-002 — Audit Log Hash Chain Verification Not Automated

| Field | Detail |
|---|---|
| **Finding ID** | F-002 |
| **Severity** | 🟠 High |
| **Control** | AU-9(2) — Protection of Audit Information — Separate Storage |
| **Assessment Method** | Examine (Audit Server configuration); Test (hash chain integrity verification process) |
| **Finding Title** | Audit Log Hash Chain Integrity Verification Performed Manually — Not Automated |
| **Finding Description** | The NEXUS SSP states that audit logs are hash-chained using SHA-256 and that any tampering triggers a SIEM alert. Testing revealed that while the hash chain IS implemented and functioning correctly, the automated SIEM alert on hash chain failure was not configured — the hash chain verification script runs weekly as a manual task performed by the ISSO. If a log was tampered with between manual verification runs, up to 7 days of undetected log manipulation could occur before discovery. |
| **Evidence** | Audit Server hash chain script (manual execution); SIEM alert rule configuration (alert rule absent); ISSO interview confirming manual verification process |
| **HIPAA Relevance** | HIPAA §164.312(b) — Audit Controls: mechanisms to record and examine activity |
| **Risk Rating** | High — 7-day detection gap for log tampering could conceal a breach |
| **Root Cause** | SIEM integration with the hash chain verification script was planned but not completed during Step 4 implementation |
| **Recommendation** | Automate hash chain verification to run every 4 hours; configure SIEM alert on verification failure to notify ISSO within 15 minutes |
| **Responsible Party** | ISSO / SOC |
| **POA&M Ref** | P-002 |
| **Target Remediation** | 30 days |

---

#### F-003 — Legacy TLS 1.2 on Clinical Endpoint Connections

| Field | Detail |
|---|---|
| **Finding ID** | F-003 |
| **Severity** | 🟠 High |
| **Control** | SC-8(1) — Transmission Confidentiality — Cryptographic Protection |
| **Assessment Method** | Test (TLS scan using Qualys SSL Labs and sslyze against all NEXUS connection endpoints) |
| **Finding Title** | Two Legacy Clinical Workstations Still Connecting via TLS 1.2 — TLS 1.3 Not Enforced |
| **Finding Description** | TLS scanning identified 2 admin workstations running Windows 10 (end-of-extended-support) that do not support TLS 1.3, resulting in their connections to the NEXUS application falling back to TLS 1.2. While TLS 1.2 remains acceptable and is not a broken protocol, the NEXUS SSP states TLS 1.3 is preferred and TLS 1.0/1.1 are explicitly disabled. The finding is that TLS 1.3 enforcement is inconsistent — the ALB negotiates down to TLS 1.2 for these endpoints rather than blocking them. Additionally, one IoT network connection was found using TLS 1.2 with a weak cipher (TLS_RSA_WITH_AES_128_CBC_SHA) rather than AEAD ciphers. |
| **Evidence** | TLS scan output (sslyze); ALB security policy configuration; Windows version inventory for affected endpoints |
| **HIPAA Relevance** | HIPAA §164.312(e)(2)(ii) — Encryption and Decryption (in transit) |
| **Risk Rating** | High — weak cipher on one IoT connection; inconsistent TLS version enforcement; legacy OS involved |
| **Root Cause** | Two workstations are awaiting hardware refresh cycle (Windows 10 EOL); IoT device uses vendor-default TLS configuration |
| **Recommendation** | (1) Accelerate hardware refresh for 2 legacy workstations — replace within 30 days; (2) Enforce TLS 1.3-only cipher suites on IoT VLAN termination point; (3) Update ALB security policy to reject TLS 1.2 connections from non-IoT endpoints |
| **Responsible Party** | System Administrator |
| **POA&M Ref** | P-003 |
| **Target Remediation** | 30 days |

---

#### F-004 — MFA Not Enrolled for All Non-Clinical Admin Accounts

| Field | Detail |
|---|---|
| **Finding ID** | F-004 |
| **Severity** | 🟠 High |
| **Control** | IA-2(2) — MFA — Non-Privileged Accounts (NEXUS tailoring addition) |
| **Assessment Method** | Test (MFA enrollment status report from Azure AD Conditional Access; attempted login without MFA) |
| **Finding Title** | 4 Administrative User Accounts Missing MFA Enrolment — NEXUS Portal Accessible Without MFA |
| **Finding Description** | Azure AD Conditional Access MFA enforcement is correctly configured for the majority of NEXUS users. However, 4 administrative accounts (billing role) were found to have been provisioned without MFA enrolment. These accounts were created during a migration of a legacy billing module 6 weeks prior to the assessment. The Conditional Access policy was applied but MFA enrolment was not enforced at provisioning. The SCA verified that these accounts could successfully authenticate to the NEXUS application with only a username and password. |
| **Evidence** | Azure AD MFA status report; Conditional Access policy configuration; successful login test without MFA (on isolated test account with identical configuration) |
| **HIPAA Relevance** | HIPAA §164.312(d) — Person Authentication |
| **Risk Rating** | High — accounts access billing PHI; authentication without MFA violates NEXUS tailoring requirement |
| **Root Cause** | Provisioning checklist for legacy module migration did not include MFA enrolment verification step |
| **Recommendation** | (1) Force MFA enrolment for 4 accounts immediately; (2) Update provisioning checklist to require MFA enrolment confirmation before account activation; (3) Add weekly automated report of accounts without MFA enrolled |
| **Responsible Party** | System Administrator / ISSO |
| **POA&M Ref** | P-004 |
| **Target Remediation** | 7 days (immediate) |

---

#### F-005 — High-Severity Vulnerabilities Exceeding 30-Day Remediation SLA

| Field | Detail |
|---|---|
| **Finding ID** | F-005 |
| **Severity** | 🟠 High |
| **Control** | RA-5 — Vulnerability Monitoring and Scanning; SI-2 — Flaw Remediation |
| **Assessment Method** | Examine (Nessus scan reports; patch management records); Test (re-scan verification) |
| **Finding Title** | 3 High-Severity CVEs Open Beyond 30-Day Remediation Deadline |
| **Finding Description** | Review of the last 90 days of Nessus vulnerability scan reports identified 3 High-severity CVEs (CVSS 7.0–8.9) that have exceeded the NEXUS-defined 30-day remediation SLA without a POA&M entry, documented exception, or compensating control. The vulnerabilities affect: (1) PostgreSQL 15.x on the Primary DB server — CVE affecting privilege escalation via extension; (2) RHEL 9 kernel package on the SIEM server — local privilege escalation CVE; (3) OpenSSL on the Audit Server — information disclosure CVE. None of the three were found actively exploitable in the current configuration, but they represent open risk without formal acknowledgement. |
| **Evidence** | Nessus scan reports (3 months); patch management records showing no patch applied; no POA&M entry for any of the three CVEs |
| **HIPAA Relevance** | HIPAA §164.308(a)(1)(ii)(A) — Risk Analysis: identify security vulnerabilities |
| **Risk Rating** | High — 3 High-CVE open items; no formal risk acknowledgement; no compensating controls documented |
| **Root Cause** | Patch management process did not escalate to ISSO when 30-day SLA was breached; no automated alert for SLA breach |
| **Recommendation** | (1) Apply patches within 5 days; (2) Add POA&M entries immediately for all 3 CVEs; (3) Implement SIEM alert when any High/Critical CVE reaches Day 25 without patch applied; (4) ISSO weekly patch compliance report to include SLA breach flagging |
| **Responsible Party** | System Administrator / ISSO |
| **POA&M Ref** | P-005 |
| **Target Remediation** | 5 days (patch); 30 days (process fix) |

---

### 🟡 MEDIUM FINDINGS (9)

---

#### F-006 — Quarterly Backup Restoration Test Not Completed

| Field | Detail |
|---|---|
| **Finding ID** | F-006 |
| **Severity** | 🟡 Medium |
| **Control** | CP-9(1) — System Backup — Testing for Reliability |
| **Assessment Method** | Examine (quarterly restoration test reports); Interview (DBA) |
| **Finding Title** | Q4 Quarterly Backup Restoration Test Not Completed Within Quarter |
| **Finding Description** | The NEXUS SSP and CP-9(1) require quarterly backup restoration tests. Review of restoration test records found that Q1, Q2, and Q3 tests were completed and documented with pass results. The Q4 test was not completed — the DBA interview confirmed the test was scheduled but deferred due to a competing priority (database maintenance window conflict) and had not been rescheduled at the time of assessment. One quarter without a tested backup creates a residual risk that the current backup set may not be restorable within the 4-hour RTO. |
| **Evidence** | Q1/Q2/Q3 restoration test reports (all PASSED); Q4 — no test report; DBA calendar records showing deferral |
| **Recommendation** | Complete Q4 restoration test within 14 days; document results; implement fixed quarterly schedule that cannot be deferred |
| **Responsible Party** | DBA / ISSO |
| **POA&M Ref** | P-006 |
| **Target Remediation** | 14 days |

---

#### F-007 — FIM Baseline Not Updated After Approved Changes

| Field | Detail |
|---|---|
| **Finding ID** | F-007 |
| **Severity** | 🟡 Medium |
| **Control** | SI-7(1) — Software and Information Integrity — Automated Integrity Checks |
| **Assessment Method** | Examine (FIM baseline files; CAB change records); Test (FIM verification against current system state) |
| **Finding Title** | File Integrity Monitoring Baseline Stale — 2 Approved Change Tickets Not Reflected |
| **Finding Description** | FIM is deployed correctly on all PHI-path servers. However, comparison of the current FIM baseline to the CAB change log identified 2 approved change tickets from the past 60 days where the FIM baseline was not updated after the change was deployed. This means the FIM system is alerting on expected changes (generating false positives) which are being suppressed by the SOC, potentially masking genuine integrity alerts. During SCA testing, a deliberate test file modification generated an alert that the SOC initially suppressed as "known change noise." |
| **Evidence** | FIM baseline file timestamps; CAB change log (2 tickets without FIM baseline update); SOC alert suppression log; SCA deliberate modification test result |
| **Recommendation** | (1) Update FIM baseline immediately to reflect 2 outstanding changes; (2) Reinforce CAB process requirement that FIM baseline update is mandatory before ticket closure; (3) Review all suppressed FIM alerts from the past 60 days to verify none were genuine integrity events |
| **Responsible Party** | System Administrator / ISSO |
| **POA&M Ref** | P-007 |
| **Target Remediation** | 30 days |

---

#### F-008 — Annual Penetration Test Not Previously Completed

| Field | Detail |
|---|---|
| **Finding ID** | F-008 |
| **Severity** | 🟡 Medium |
| **Control** | CA-8 — Penetration Testing |
| **Assessment Method** | Examine (prior pen test records); Interview (ISSO) |
| **Finding Title** | No Prior Penetration Test — First Annual Test Completed During This Assessment |
| **Finding Description** | CA-8 (annual penetration test) was added to the NEXUS control baseline as a tailoring addition in Step 3. This Step 5 assessment includes the first penetration test. There is no prior year test result to compare against. The current penetration test results (Phase 5) found no critical or high exploitable vulnerabilities, but the absence of prior baseline testing means no historical comparison is possible. This finding is informational/medium rather than high because the first test was successfully completed. |
| **Evidence** | ISSO interview confirming no prior pen test; current pen test report (no critical/high findings) |
| **Recommendation** | Establish annual pen test schedule; retain results for year-over-year comparison; include pen test scope review in annual SAP |
| **Responsible Party** | ISSO |
| **POA&M Ref** | P-008 |
| **Target Remediation** | Process established — next test scheduled |

---

#### F-009 — Phishing Simulation — 22% Click Rate

| Field | Detail |
|---|---|
| **Finding ID** | F-009 |
| **Severity** | 🟡 Medium |
| **Control** | AT-2 — Literacy Training and Awareness; AT-2(2) — Insider Threat Awareness |
| **Assessment Method** | Test (simulated phishing campaign targeting 450 clinical and administrative staff) |
| **Finding Title** | 22% Staff Click Rate on Simulated Phishing Email — 8% Submitted Credentials |
| **Finding Description** | A simulated phishing email mimicking a laboratory results notification (high clinical relevance) was sent to 450 NEXUS users. 99 users (22%) clicked the link; 36 users (8%) submitted credentials on the simulated phishing landing page. Of credential submitters, 19 (53%) were clinical staff (nurses and junior doctors) — consistent with research showing clinical urgency overrides security caution. MFA would have blocked any real credential use, but the click rate indicates social engineering vulnerability above industry target (<10%). |
| **Evidence** | Phishing simulation campaign report; click and credential submission statistics by role; role breakdown of credential submitters |
| **Recommendation** | (1) Deploy targeted phishing-resistant awareness training to credential submitters within 30 days; (2) Add clinical-scenario phishing simulations quarterly; (3) Implement email warning banner for external-origin emails |
| **Responsible Party** | ISSO / HR |
| **POA&M Ref** | P-009 |
| **Target Remediation** | 90 days |

---

#### F-010 — Medical IoT BAA Missing for 3 Device Vendors

| Field | Detail |
|---|---|
| **Finding ID** | F-010 |
| **Severity** | 🟡 Medium |
| **Control** | SA-9 — External System Services; PT-2 — Authority to Process PII |
| **Assessment Method** | Examine (BAA register; IoT device inventory; vendor contracts) |
| **Finding Title** | Business Associate Agreements Not Signed for 3 Medical IoT Device Vendors |
| **Finding Description** | The NEXUS BAA register lists all third parties with PHI access. Review identified 3 medical IoT device vendors whose devices transmit vital signs data to the NEXUS database (constituting PHI handling) but for whom no BAA has been executed. BAAs have been requested but not yet returned. These vendors have been in this status for more than 90 days, which was noted as PRE-001 in the SSP. |
| **Evidence** | IoT device inventory; BAA register (3 entries showing "Pending"); vendor outreach correspondence (90+ days unanswered) |
| **Recommendation** | (1) Escalate BAA request to vendor legal departments; (2) If BAA not executed within 30 days, disconnect non-compliant IoT devices from NEXUS; (3) Include BAA requirement in future procurement contracts for IoT devices |
| **Responsible Party** | ISSO / Privacy Officer / Legal |
| **POA&M Ref** | P-010 |
| **Target Remediation** | 30 days |

---

#### F-011 — SIEM Alert Threshold for After-Hours Access Too Broad

| Field | Detail |
|---|---|
| **Finding ID** | F-011 |
| **Severity** | 🟡 Medium |
| **Control** | SI-4 — System Monitoring; AU-6(1) — Automated Audit Review |
| **Assessment Method** | Test (SIEM alert rule testing; review of 30-day alert suppression log) |
| **Finding Title** | After-Hours PHI Access SIEM Rule Generating Excessive False Positives — Alert Fatigue Risk |
| **Finding Description** | The SIEM alert rule for after-hours PHI access (23:00–06:00) is generating an average of 47 alerts per night. SCA review of 30 days of alerts found that 94% are legitimate on-call clinical staff accessing patient records. The alert is therefore creating SOC alert fatigue — the on-call SOC analyst begins to routinely dismiss the alert without investigation. During the assessment period, 3 non-on-call staff accessed PHI during restricted hours; none of these generated visible alerts because they were buried in the alert queue. |
| **Evidence** | SIEM alert log (30 days); on-call schedule comparison with alert triggers; SOC alert dismissal records |
| **Recommendation** | (1) Tune SIEM rule to cross-reference on-call schedule — alert only when access is by non-on-call staff; (2) Reduce alert volume to <5 per night; (3) Implement on-call schedule integration with SIEM |
| **Responsible Party** | SOC / ISSO |
| **POA&M Ref** | P-011 |
| **Target Remediation** | 60 days |

---

#### F-012 — Privileged Session Audit Review Not Performed Monthly

| Field | Detail |
|---|---|
| **Finding ID** | F-012 |
| **Severity** | 🟡 Medium |
| **Control** | AU-14 — Session Audit; CA-7 — Continuous Monitoring |
| **Assessment Method** | Examine (privileged session audit review logs); Interview (ISSO) |
| **Finding Title** | Privileged Session Audit Captures Correctly But Monthly Review Not Evidenced |
| **Finding Description** | Privileged session capture is correctly implemented and functioning. However, the NEXUS SSP states the ISSO reviews privileged session records monthly. Review of ISSO workpapers for the past 6 months found only 3 documented monthly reviews (March, June, September) — alternate months have no review record. The ISSO confirmed reviews were performed informally but not documented. Undocumented reviews cannot be evidenced to the AO or future SCA. |
| **Evidence** | Privileged session audit records (confirms capture); ISSO review workpapers (3 of 6 months documented) |
| **Recommendation** | Formalise monthly review using a sign-off form; retain signed form for 6 years; add to ISSO monthly calendar with mandatory documentation step |
| **Responsible Party** | ISSO |
| **POA&M Ref** | P-012 |
| **Target Remediation** | 30 days |

---

#### F-013 — Contingency Plan Not Updated Post-Architecture Change

| Field | Detail |
|---|---|
| **Finding ID** | F-013 |
| **Severity** | 🟡 Medium |
| **Control** | CP-2 — Contingency Plan |
| **Assessment Method** | Examine (Contingency Plan; architecture change records) |
| **Finding Title** | Contingency Plan Not Updated Following AWS Multi-AZ Architecture Change |
| **Finding Description** | A significant change was made to the NEXUS AWS architecture 4 months ago — EC2 instances were deployed across two Availability Zones. The Contingency Plan recovery procedures still reference single-AZ failover procedures from before this change. The recovery procedures are now partly inaccurate, which could slow recovery during an actual incident if staff follow outdated procedures. |
| **Evidence** | Contingency Plan version (dated prior to AZ change); CAB change record for AZ deployment; architecture diagram (current) vs. Contingency Plan (outdated) |
| **Recommendation** | Update Contingency Plan to reflect current multi-AZ architecture within 30 days; update CAB process to require Contingency Plan review for any infrastructure change |
| **Responsible Party** | ISSO / System Administrator |
| **POA&M Ref** | P-013 |
| **Target Remediation** | 30 days |

---

#### F-014 — Annual Risk Assessment Overdue by 6 Weeks

| Field | Detail |
|---|---|
| **Finding ID** | F-014 |
| **Severity** | 🟡 Medium |
| **Control** | RA-3 — Risk Assessment |
| **Assessment Method** | Examine (risk assessment date; HIPAA requirement) |
| **Finding Title** | Annual Risk Assessment Completed 6 Weeks Past Annual Due Date |
| **Finding Description** | HIPAA §164.308(a)(1)(ii)(A) requires covered entities to conduct an accurate and thorough assessment of risks to ePHI on a reasonable and appropriate basis. The NEXUS annual risk assessment (this RMF package's Risk Assessment, NEXUS-RMF-RA-001) was completed 6 weeks past the annual anniversary of the prior assessment. The gap creates a brief period without a current formal risk assessment. |
| **Evidence** | Prior risk assessment date; current risk assessment date (NEXUS-RMF-RA-001); 6-week gap calculation |
| **Recommendation** | Schedule next risk assessment to begin 6 weeks before the annual due date; add to ISSO annual programme calendar |
| **Responsible Party** | ISSO |
| **POA&M Ref** | P-014 |
| **Target Remediation** | Process fix only — current assessment complete |

---

### 🟢 LOW FINDINGS (4)

---

#### F-015 — Visitor Access Log — 2 Missing Entries

| Field | Detail |
|---|---|
| **Finding ID** | F-015 |
| **Severity** | 🟢 Low |
| **Control** | PE-8 — Visitor Access Records |
| **Assessment Method** | Examine (visitor log — on-premises data centres) |
| **Finding Title** | 2 Visitor Access Log Entries Incomplete — Missing Departure Time |
| **Finding Description** | Review of the visitor access log for Hospital Data Centre Site A (6-month period) found 2 entries missing the departure time. The visitor company and purpose were recorded; only the departure time was absent. CCTV review confirmed both visits were legitimate vendor maintenance. |
| **Recommendation** | Brief facilities staff on complete log entry requirements; add departure time field as mandatory at physical log book |
| **Responsible Party** | Facilities |
| **POA&M Ref** | P-015 |
| **Target Remediation** | 30 days (process improvement) |

---

#### F-016 — Training Completion Rate — 3 Staff Outstanding

| Field | Detail |
|---|---|
| **Finding ID** | F-016 |
| **Severity** | 🟢 Low |
| **Control** | AT-2 — Literacy Training and Awareness; AT-4 — Training Records |
| **Assessment Method** | Examine (LMS completion report) |
| **Finding Title** | Annual Security Awareness Training — 3 Staff Not Yet Completed |
| **Finding Description** | LMS review found 3 NEXUS users (2 agency nurses, 1 admin locum) had not completed the annual security awareness training. All 3 are temporary staff whose completion was not tracked by the agency HR system. Their NEXUS accounts are active. |
| **Recommendation** | Include agency and temporary staff in LMS training tracking; account activation checklist must confirm training completion |
| **Responsible Party** | HR / ISSO |
| **POA&M Ref** | P-016 |
| **Target Remediation** | 30 days |

---

#### F-017 — System Use Notification Banner — Missing from One Internal Interface

| Field | Detail |
|---|---|
| **Finding ID** | F-017 |
| **Severity** | 🟢 Low |
| **Control** | AC-8 — System Use Notification |
| **Assessment Method** | Test (login screen review across all NEXUS interfaces) |
| **Finding Title** | HIPAA Warning Banner Missing from NEXUS Internal Admin Console |
| **Finding Description** | The HIPAA warning banner is correctly displayed on the main NEXUS clinical interface and the patient portal. The internal admin console (used exclusively by System Administrators for configuration management) does not display the banner. All SA users have signed the acceptable use policy, but the technical control (AC-8) is not implemented on this interface. |
| **Recommendation** | Add system use notification banner to admin console login screen |
| **Responsible Party** | System Administrator |
| **POA&M Ref** | P-017 |
| **Target Remediation** | 60 days |

---

#### F-018 — Portable Media Policy Not Included in Annual Training

| Field | Detail |
|---|---|
| **Finding ID** | F-018 |
| **Severity** | 🟢 Low |
| **Control** | MP-7 — Media Use; AT-3 — Role-Based Training |
| **Assessment Method** | Examine (training content review); Interview (ISSO) |
| **Finding Title** | Removable Media Policy Not Included in Annual Security Awareness Training Content |
| **Finding Description** | USB ports are disabled on clinical endpoints via GPO — a strong technical control. However, the annual security awareness training does not include a module on removable media policy. The ISSO confirmed staff are not formally trained on the portable media prohibition. While the technical control (USB disable) is the primary defence, training provides the procedural layer. |
| **Recommendation** | Add a removable media policy module (5 minutes) to the annual security awareness training for the next cycle |
| **Responsible Party** | ISSO / HR |
| **POA&M Ref** | P-018 |
| **Target Remediation** | 180 days (next training cycle) |

---

## Positive Findings — Controls Operating Effectively

The following priority controls were found to be fully satisfied and merit specific recognition:

| Control | Assessment Finding |
|---|---|
| AC-3(7) — RBAC | Three-layer RBAC (AD + Application + PostgreSQL row-level security) confirmed operational in all three layers. SCA attempted lateral role escalation — blocked at all three points. ✅ |
| IA-2(1)(2) — MFA | MFA bypass attempted on 15 accounts — blocked in all 15 cases. Break-glass procedure tested — alert generated in 2 minutes. Authenticator app and FIDO2 key both verified functional. ✅ |
| AU-9(2) — Audit Server | SHA-256 hash chain verified intact across 6 months of logs. Dedicated server confirmed — no NEXUS application services running on Audit Server. ISSO-only deletion confirmed. ✅ |
| CP-10 — Recovery | Scenario B failover test (Primary DB failure) completed: DBA promoted secondary to primary in 11 minutes. Scenario A (App Server failure): ALB rerouted in 28 seconds. ✅ |
| SC-28(1) — Encryption at Rest | AES-256 confirmed on Primary DB (LUKS), Secondary DB (LUKS), S3 (SSE-KMS), Backup Vault. Customer-managed keys verified in AWS KMS. FIPS 140-2 HSM confirmed on-premises. ✅ |
| SI-4 — System Monitoring | Bulk PHI access simulation (101 records accessed in 8 minutes) triggered SIEM alert in 4 minutes. SOC responded within 6 minutes. Alert-to-response SLA met. ✅ |
| AU-11 — Log Retention | S3 Object Lock WORM verified — SCA attempted deletion of archived logs via AWS CLI (with ISSO-approved test credentials) — deletion blocked by Object Lock. 6-year retention confirmed. ✅ |
| CP-9(1) — Backup Test | Backup restoration test (Scenario C — full site recovery) completed in 3 hours 42 minutes — within the 4-hour RTO target. Data integrity verified by DBA. ✅ |

---

## Penetration Test Summary

| Test Area | Result | Notable Findings |
|---|---|---|
| External — Patient portal | No critical/high vulnerabilities | 2 medium: security headers missing; verbose error messages |
| External — ALB / TLS | 1 medium: TLS 1.2 on 2 legacy endpoints (also F-003) | See F-003 |
| Web application — NEXUS app | No SQLi, XSS, auth bypass found | WAF confirmed blocking SQLi and XSS payloads |
| Internal — Hospital LAN | No direct path to PHI database found | IoT VLAN segmentation held — pivot attempt blocked |
| Phishing simulation | 22% click rate; 8% credential submission | See F-009 |
| Wireless assessment | Hospital Wi-Fi 802.1X correctly configured | No weaknesses found |
| Social engineering — physical | Tailgating attempt blocked by security staff | Physical controls functioning |

**Overall penetration test conclusion:** No critical or high exploitable vulnerabilities discovered. The NEXUS security architecture demonstrated resilience against external attack. The primary residual risks remain insider threat and phishing-based initial access (consistent with Risk Register findings R-002 and R-003).

---

## SCA Recommendation to Authorising Official

Based on the full assessment findings, the Security Control Assessor recommends the Authorising Official **grant Authority to Operate (ATO)** for the NEXUS Electronic Health Records System, subject to the following conditions:

| Condition | Requirement |
|---|---|
| High findings (F-001 to F-005) | Must be remediated within 30 days of ATO grant; evidence submitted to ISSO |
| F-004 specifically | MFA enrolment for 4 accounts must be completed within 7 days — prior to ATO grant |
| All findings | POA&M entries created and tracked by ISSO; monthly status updates to AO |
| Next assessment | Annual reassessment to be conducted in 2026 |
| Continuous monitoring | ISSO to maintain continuous monitoring programme per CA-7 |

The SCA finds that the overall control posture of NEXUS is appropriate for its mission criticality and data sensitivity. The 18 findings are consistent with a maturing security programme rather than a programme with fundamental control failures. The absence of any Critical findings, combined with the demonstrated effectiveness of critical controls (MFA, audit logging, encryption, backup recovery, and SIEM monitoring), supports the ATO recommendation.

---

## Sign-Off

| Role | Name | Signature | Date |
|---|---|---|---|
| Lead SCA | [Name] | _________________________ | 2025 |
| ISSO (reviewed for factual accuracy) | [Name] | _________________________ | 2025 |
| System Owner | [Name] | _________________________ | 2025 |
| **Submitted To — Authorising Official** | **[Name]** | **Received** | **2025** |

---

*Document Reference: NEXUS-RMF-SAR-001 — Reference 6 | Version 1.0 — Final | Classification: Internal — Controlled — Restricted Distribution*
*NEXUS EHR is a fictional system created for a GRC portfolio demonstration. All names, data, and system details are illustrative only.*
