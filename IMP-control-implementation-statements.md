# Control Implementation Statements
## NEXUS Electronic Health Records System | Step 4 — Implement Controls

| Field | Detail |
|---|---|
| **Document Reference** | NEXUS-RMF-IMP-001 |
| **Document Type** | Control Implementation Statements — All Families |
| **Version** | 1.0 |
| **Classification** | Internal — Controlled |
| **Prepared By** | [ISSO Name], Lead Information Security Analyst |
| **Reviewed By** | [System Owner Name] |
| **Date** | 2025 |
| **References** | NIST SP 800-53 Rev 5; NIST SP 800-53A Rev 5; SSP (NEXUS-RMF-SSP-001) |

---

> **Purpose:** This document provides the formal implementation statement for every selected NEXUS control across all 20 families. Each statement documents: what the control requires, how NEXUS implements it, what evidence exists, and the current implementation status. This feeds directly into the Step 5 Security Assessment — the SCA uses these statements as the basis for examination, interview, and testing.

---

## Statement Format

| Field | Description |
|---|---|
| **Requirement** | What NIST SP 800-53 Rev 5 requires |
| **Implementation** | How NEXUS satisfies the requirement — specific, operational, measurable |
| **Evidence** | Artefacts available for SCA examination, interview, or testing |
| **Status** | Implemented / Partially Implemented / Planned |
| **Responsible Party** | Who owns this control |
| **HIPAA Mapping** | Applicable HIPAA standard (where applicable) |

---

## AC — Access Control Family

### AC-1 — Access Control Policy and Procedures
**Requirement:** Develop, document, and disseminate an access control policy.
**Implementation:** The NEXUS Access Control Policy (v1.0) was developed by the ISSO, approved by the AO, and distributed to all staff at onboarding and annually via the acceptable use acknowledgement. The policy covers account management, RBAC roles, MFA requirements, session timeouts, remote access, and mobile device controls. Reviewed annually and following any significant system change.
**Evidence:** Access Control Policy v1.0; staff acknowledgement records; annual review log; policy distribution records
**Status:** ✅ Implemented | **Responsible Party:** ISSO | **HIPAA:** §164.308(a)(1)

---

### AC-2 — Account Management
**Requirement:** Manage accounts including establishing, modifying, reviewing, disabling, and removing; automate account management where feasible.
**Implementation:** NEXUS accounts managed via Active Directory with NEXUS RBAC integration. Provisioning within 24 hours of HR approval. De-provisioning within 24 hours of departure notification (automated HR-IT workflow). Quarterly ISSO access reviews. 90-day inactivity auto-disable. Five defined roles with minimum necessary access. No shared accounts. Service accounts in PAM vault.
**Evidence:** Active Directory configuration; HR-IT provisioning workflow; quarterly access review logs; inactive account GPO; role definition document; PAM vault inventory
**Status:** ✅ Implemented | **Responsible Party:** ISSO / SA | **HIPAA:** §164.308(a)(3)(ii)(C)

---

### AC-2(1) — Automated Account Management
**Requirement:** Employ automated mechanisms to support account management activities.
**Implementation:** Active Directory automation handles account provisioning, group membership, and deprovisioning triggers. HR system (ServiceNow) integrates with AD — a departure ticket in ServiceNow triggers an automatic AD account disable. Inactive account scans run nightly.
**Evidence:** ServiceNow-AD integration configuration; automated disable workflow documentation; nightly inactive account scan report
**Status:** ✅ Implemented | **Responsible Party:** SA | **HIPAA:** §164.308(a)(3)

---

### AC-2(3) — Account Management — Disable Inactive Accounts
**Requirement:** Disable accounts after a defined period of inactivity.
**Implementation:** Accounts inactive for 90 consecutive days are automatically disabled via AD GPO. The ISSO receives a weekly report of disabled accounts for review. Re-activation requires ISSO approval and re-verification of continued business need.
**Evidence:** AD GPO configuration (90-day inactivity threshold); weekly inactive account report; re-activation approval workflow
**Status:** ✅ Implemented | **Responsible Party:** SA | **HIPAA:** §164.308(a)(3)(ii)(C)

---

### AC-2(7) — Privileged User Accounts
**Requirement:** Establish and administer privileged user accounts in accordance with a role-based access scheme.
**Implementation:** All system administrators hold two separate accounts: a standard user account for email and general tasks, and a named privileged account (e.g. admin-jsmith) used exclusively for administrative functions. No dual-use accounts are permitted. Privileged accounts are inventoried and reviewed quarterly by the ISSO. All privileged account activity is logged with elevated detail.
**Evidence:** Privileged account register; dual-use account prohibition policy; quarterly privileged account review; audit log sample showing privileged account activity
**Status:** ✅ Implemented | **Responsible Party:** ISSO | **HIPAA:** §164.308(a)(3)

---

### AC-3 — Access Enforcement
**Requirement:** Enforce approved authorisations for logical access to information and system resources.
**Implementation:** NEXUS enforces access at three independent layers: (1) Active Directory group membership at authentication; (2) NEXUS application RBAC engine at the function level; (3) PostgreSQL row-level security at the database level. Three-layer enforcement means a bypass of any single layer does not grant unauthorised access.
**Evidence:** AD RBAC group policy; NEXUS application permission configuration; PostgreSQL row-level security policy script
**Status:** ✅ Implemented | **Responsible Party:** SA | **HIPAA:** §164.308(a)(4)

---

### AC-3(7) — Role-Based Access Control
**Requirement:** Enforce a role-based access control policy; control access to information and functions based on defined roles.
**Implementation:** Five NEXUS roles with defined permissions: Clinical Staff (full PHI — assigned patients), Administrative Staff (demographics, scheduling), Billing Officer (billing data only), System Administrator (no PHI — configuration only), Read-Only Auditor (audit logs — read only). Patient portal users access own records only. Role changes require new ISSO approval.
**Evidence:** Role definition document; NEXUS RBAC configuration; PostgreSQL role mapping; role assignment records
**Status:** ✅ Implemented | **Responsible Party:** SA / ISSO | **HIPAA:** §164.308(a)(4)(ii)(B)

---

### AC-4 — Information Flow Enforcement
**Requirement:** Enforce approved authorisations for controlling the flow of information within the system and between interconnected systems.
**Implementation:** Information flow is enforced by: (1) AWS Security Groups — deny all inbound except Port 443 from ALB and VPN traffic; (2) VPN tunnel — all PHI flows between cloud and on-premises only through the encrypted VPN; (3) Network segmentation — medical IoT devices on isolated VLAN; (4) WAF — inspects and filters all inbound application traffic.
**Evidence:** AWS Security Group rules; VPN configuration; network diagram with flow annotations; IoT VLAN configuration; WAF policy
**Status:** ✅ Implemented | **Responsible Party:** SA | **HIPAA:** §164.312(e)(1)

---

### AC-5 — Separation of Duties
**Requirement:** Separate duties of individuals; support separation of duties through assigned access authorisations.
**Implementation:** Key separations enforced in NEXUS: (1) No account can both access PHI and administer audit logs; (2) DBAs have database access but no application admin rights; (3) SAs have system access but no PHI access; (4) The ISSO reviews logs but does not have access to modify security controls without AO approval; (5) Backup restore permissions separated from backup creation permissions.
**Evidence:** Role definition matrix showing separation; AD group membership showing no crossover; DBA and SA access comparison report
**Status:** ✅ Implemented | **Responsible Party:** ISSO | **HIPAA:** §164.308(a)(3)

---

### AC-6 — Least Privilege
**Requirement:** Employ least privilege, allowing only authorised accesses for users which are necessary to accomplish assigned tasks.
**Implementation:** Each NEXUS role grants only the minimum permissions required for its defined function. Clinical staff can only view records of patients assigned to their care — bulk access to all records is not permitted at the role level. The minimum necessary standard is reviewed with each role definition update. Temporary elevated access for specific tasks requires ISSO approval and is time-limited.
**Evidence:** Role permission matrix; minimum necessary policy; temporary access approval records; annual role review
**Status:** ✅ Implemented | **Responsible Party:** ISSO | **HIPAA:** §164.308(a)(4)(ii)(B)

---

### AC-7 — Unsuccessful Login Attempts
**Requirement:** Enforce a limit on consecutive invalid login attempts; automatically lock or delay after exceeding the limit.
**Implementation:** 5 failures → 30-minute lockout for standard users; 3 failures → ISSO manual reset for SA accounts; 5 failures → email-based unlock for patient portal. SIEM alerts on org-wide auth surge. All lockout events logged.
**Evidence:** AD Fine-Grained Password Policy; NEXUS app lockout configuration; patient portal lockout config; SIEM alert rule; lockout event log samples
**Status:** ✅ Implemented | **Responsible Party:** SA | **HIPAA:** §164.312(d)

---

### AC-8 — System Use Notification
**Requirement:** Display an approved system use notification message before granting access.
**Implementation:** NEXUS displays a HIPAA-compliant warning banner at the login screen (all interfaces including patient portal and admin console). Banner text includes: system is monitored; no expectation of privacy; unauthorised access is prohibited; PHI access is audited; violations will be reported.
**Evidence:** Login screen screenshot showing banner; banner text (approved by ISSO and Legal); portal banner screenshot
**Status:** ✅ Implemented | **Responsible Party:** SA | **HIPAA:** §164.308(a)(1)

---

### AC-11 — Device Lock
**Requirement:** Enforce a session lock after a period of inactivity; require re-authentication to resume.
**Implementation:** Windows endpoints: 15-minute screensaver lock via Group Policy — full Windows credentials required to resume. iOS tablets: 15-minute auto-lock via MDM profile. NEXUS application: 30-minute idle session termination — full re-authentication including MFA required.
**Evidence:** GPO configuration (screensaver 15 min); MDM profile (auto-lock 15 min); NEXUS session timeout code/config
**Status:** ✅ Implemented | **Responsible Party:** SA | **HIPAA:** §164.312(a)(2)(iii)

---

### AC-12 — Session Termination
**Requirement:** Automatically terminate a session after a defined period of inactivity.
**Implementation:** The NEXUS application terminates the authenticated session after 30 minutes of inactivity. The user is fully logged out and must re-authenticate from scratch including MFA. Clinician is redirected to the login screen. Session token is invalidated server-side immediately on timeout.
**Evidence:** NEXUS session timeout configuration; application session token invalidation code; user-facing session expiry message
**Status:** ✅ Implemented | **Responsible Party:** SA | **HIPAA:** §164.312(a)(2)(iii)

---

### AC-17 — Remote Access
**Requirement:** Establish and document usage restrictions for remote access; authorise remote access before allowing connections.
**Implementation:** Two authorised remote access pathways: (1) HTTPS via ALB (Port 443) for clinical and patient portal access — MFA enforced; (2) VPN (IPSec AES-256 certificate-based) for IT administrative access — privileged account + MFA required. All other inbound methods blocked by Security Group deny-all default. Policy documented and distributed. Remote sessions fully logged.
**Evidence:** Remote access policy; VPN configuration; AWS Security Group deny-all rule; MFA enforcement configuration; monthly session log
**Status:** ✅ Implemented | **Responsible Party:** SA | **HIPAA:** §164.312(e)(1)

---

### AC-18 — Wireless Access
**Requirement:** Establish usage restrictions and implement controls for wireless access.
**Implementation:** Clinical wireless (hospital Wi-Fi) is managed by a separate SSID with 802.1X authentication. NEXUS traffic over hospital Wi-Fi is still subject to full TLS 1.2+ encryption and MFA enforcement — wireless access does not reduce security requirements. Medical IoT devices use an isolated wireless VLAN with no access to the general clinical network.
**Evidence:** Wi-Fi 802.1X configuration; network diagram showing VLAN segmentation; wireless security policy
**Status:** ✅ Implemented | **Responsible Party:** SA | **HIPAA:** §164.312(e)(1)

---

### AC-19 — Access Control for Mobile Devices
**Requirement:** Establish usage restrictions and implement controls for mobile devices; authorise the connection of mobile devices.
**Implementation:** All NEXUS-enabled mobile devices (nurses' tablets — iOS) are enrolled in MDM before NEXUS access is permitted. MDM enforces: full device encryption, 15-minute auto-lock, 6-digit minimum PIN, remote wipe capability, application allowlist, and NEXUS app version enforcement. Unenrolled devices cannot access NEXUS — MDM certificate required for authentication.
**Evidence:** MDM enrolment policy; MDM profile configuration; MDM-enrolled device inventory; unenrolled device blocking test record
**Status:** ✅ Implemented | **Responsible Party:** SA | **HIPAA:** §164.312(a)(2)(iv)

---

### AC-20 — Use of External Systems
**Requirement:** Establish terms and conditions for use of external systems; authorise use of external systems with adequate security.
**Implementation:** External systems connecting to NEXUS must have a signed BAA (if PHI-touching) or NDA/confidentiality agreement. Remote access from personal devices is permitted only via the NEXUS patient portal or clinician HTTPS interface — not via VPN. All personal device access is subject to the same MFA and session timeout controls as corporate devices.
**Evidence:** BAA register; external system authorisation policy; BAA templates; non-corporate device access policy
**Status:** ✅ Implemented | **Responsible Party:** ISSO | **HIPAA:** §164.308(b)(1)

---

### AC-22 — Publicly Accessible Content
**Requirement:** Review proposed content on publicly accessible systems; remove non-public information and authorise only approved information.
**Implementation:** The NEXUS patient portal is the only publicly accessible NEXUS component. The portal displays only the HIPAA Notice of Privacy Practices and the login interface to the public. No PHI is displayed without authentication. Content changes to the portal are reviewed by the ISSO and Privacy Officer before publication. Annual review of portal public content conducted by ISSO.
**Evidence:** Patient portal public content review record; portal screenshot showing no PHI pre-login; ISSO and Privacy Officer approval workflow for content changes
**Status:** ✅ Implemented | **Responsible Party:** ISSO / Privacy Officer | **HIPAA:** §164.308(a)(1)

---

## AT — Awareness and Training Family

### AT-1 — Awareness and Training Policy
**Requirement:** Develop and disseminate an awareness and training policy.
**Implementation:** NEXUS Security Awareness and Training Policy (v1.0) developed by ISSO, approved by AO, and distributed to all staff. Policy mandates annual security awareness training, role-based clinical training, and HIPAA-specific training for all PHI-handling roles. Reviewed annually.
**Evidence:** Training policy v1.0; staff distribution acknowledgement; annual review log
**Status:** ✅ Implemented | **Responsible Party:** ISSO | **HIPAA:** §164.308(a)(5)(i)

---

### AT-2 — Literacy Training and Awareness
**Requirement:** Provide security and privacy literacy training to all system users; include threat awareness.
**Implementation:** All NEXUS users complete mandatory annual security awareness training covering: HIPAA obligations, PHI handling, password security, phishing recognition, incident reporting, acceptable use, and social engineering. Training is tracked in the LMS (Learning Management System). Non-completion after 30-day reminder results in NEXUS access suspension pending completion.
**Evidence:** LMS training completion reports; training module content; access suspension records for non-completers; annual training schedule
**Status:** ✅ Implemented | **Responsible Party:** ISSO / HR | **HIPAA:** §164.308(a)(5)(ii)(A)

---

### AT-2(2) — Insider Threat Awareness
**Requirement:** Include insider threat awareness in security awareness training.
**Implementation:** Annual training includes a dedicated insider threat module covering: warning signs of malicious or negligent insider behaviour, how to report suspected insider threats (anonymous reporting channel), NEXUS SIEM monitoring capabilities, and real healthcare breach case studies involving insiders. Clinical and administrative staff are made aware that all PHI access is logged and reviewed.
**Evidence:** Insider threat training module content; LMS completion records; anonymous reporting channel documentation
**Status:** ✅ Implemented | **Responsible Party:** ISSO | **HIPAA:** §164.308(a)(5)

---

### AT-3 — Role-Based Training
**Requirement:** Provide role-based security and privacy training before authorising access; update training when system or role changes occur.
**Implementation:** Four role-specific training tracks are delivered before initial NEXUS access and annually thereafter: (1) Clinical Staff — HIPAA minimum necessary, PHI access logging, patient privacy, clinical record accuracy; (2) Administrative Staff — scheduling privacy, access limits, data handling; (3) IT / System Administrators — privileged account security, change management, incident response; (4) Management / Leadership — risk management, breach response leadership, regulatory obligations.
**Evidence:** Role-based training modules (4 tracks); LMS completion records by role; access provisioning gate — training completion verified before account activation
**Status:** ✅ Implemented | **Responsible Party:** ISSO / HR | **HIPAA:** §164.308(a)(5)(ii)(A)

---

### AT-4 — Training Records
**Requirement:** Document and monitor information security and privacy training activities.
**Implementation:** All NEXUS training completion is recorded in the LMS with user ID, training title, completion date, and score. Records are retained for 6 years (HIPAA documentation retention). ISSO receives a monthly training compliance report. Non-compliant users are escalated to HR for follow-up.
**Evidence:** LMS training records (sample); monthly compliance report; 6-year retention policy for training records
**Status:** ✅ Implemented | **Responsible Party:** HR | **HIPAA:** §164.308(a)(5)

---

### AT-6 — Training Feedback
**Requirement:** Provide a process for individuals to provide feedback on training.
**Implementation:** All NEXUS training modules include a post-completion feedback survey. Annual training effectiveness review conducted by ISSO — analysing completion rates, survey scores, and correlation with security incident types. Training content is updated based on findings and current threat landscape (H-ISAC healthcare threat intelligence).
**Evidence:** Training feedback survey; annual training effectiveness review report; content update log
**Status:** ✅ Implemented | **Responsible Party:** ISSO | **HIPAA:** §164.308(a)(1)

---

## AU — Audit and Accountability Family

### AU-1 — Audit and Accountability Policy
**Requirement:** Develop and disseminate an audit and accountability policy.
**Implementation:** NEXUS Audit and Accountability Policy (v1.0) defines: which events are logged, log content requirements, log retention (6 years), Audit Server architecture, ISSO access controls for logs, SIEM review schedule, and log integrity requirements. Approved by AO and distributed to all IT personnel.
**Evidence:** Audit policy v1.0; distribution records; annual review log
**Status:** ✅ Implemented | **Responsible Party:** ISSO | **HIPAA:** §164.312(b)

---

### AU-2 — Event Logging
**Requirement:** Identify events to be logged and provide rationale for event selection.
**Implementation:** NEXUS logs: all authentication events (login, logout, MFA, lockout, failure); all PHI access events (view, create, modify, delete) with patient record ID; all privileged actions; all account management operations; all configuration changes; all security alerts and WAF blocks; all backup operations; all replication status events. Every log entry includes: user ID (AD UPN), timestamp (UTC NTP ±1 second), event type, source IP, device hostname, target resource, outcome, session ID.
**Evidence:** Syslog-ng forwarding configuration; Audit Server schema; NTP sync configuration; sample log entries demonstrating all required fields; event logging policy
**Status:** ✅ Implemented | **Responsible Party:** ISSO / SA | **HIPAA:** §164.312(b)

---

### AU-3 — Content of Audit Records
**Requirement:** Audit records must establish what event occurred, when, where, source, and the outcome.
**Implementation:** Every NEXUS audit log entry contains: (1) What — event type and subtype (e.g. PHI_ACCESS:MODIFY); (2) When — UTC timestamp, NTP-synchronised, ±1 second precision; (3) Where — source IP and device hostname; (4) Who — user ID (Active Directory UPN), role at time of event; (5) Target — patient record ID or system resource; (6) Outcome — SUCCESS, FAILURE, or BLOCKED; (7) Session ID for cross-event correlation. Modification events capture before-value and after-value.
**Evidence:** Audit log schema documentation; sample audit record showing all fields; SIEM log parsing configuration
**Status:** ✅ Implemented | **Responsible Party:** SA | **HIPAA:** §164.312(b)

---

### AU-4 — Audit Log Storage Capacity
**Requirement:** Allocate audit log storage capacity and reduce the likelihood of capacity being exceeded.
**Implementation:** Audit Logging Server is provisioned with storage calculated for 2 years of active log retention at projected volume plus 25% headroom. Storage monitoring: SIEM alert triggers when Audit Server disk reaches 75% capacity, giving the SA time to expand storage or archive before approaching limit. Older logs are automatically archived to AWS S3 per the retention lifecycle policy.
**Evidence:** Audit Server storage specification; SIEM alert configuration for 75% threshold; S3 lifecycle archival policy; current storage utilisation report
**Status:** ✅ Implemented | **Responsible Party:** SA | **HIPAA:** §164.312(b)

---

### AU-5 — Response to Audit Processing Failures
**Requirement:** Alert defined personnel and take defined actions in the event of an audit processing failure.
**Implementation:** If the Syslog-ng forwarding from any NEXUS component to the Audit Server fails, a SIEM alert is immediately raised to the ISSO and SOC Analyst. If the Audit Server itself becomes unavailable, a high-priority page is sent to the on-call SA and ISSO. NEXUS application behaviour during log failure: continue operation but flag the outage in the system status dashboard. The ISSO investigates all log processing failures within 1 hour.
**Evidence:** SIEM alert rule for Syslog forwarding failure; Audit Server availability monitoring configuration; log failure response procedure; system status dashboard configuration
**Status:** ✅ Implemented | **Responsible Party:** ISSO | **HIPAA:** §164.312(b)

---

### AU-6 — Audit Record Review, Analysis, and Reporting
**Requirement:** Review and analyse audit records at a defined frequency for signs of inappropriate or unusual activity.
**Implementation:** Daily automated SIEM review: correlation rules run against all new log entries every 15 minutes; daily summary report generated at 06:00 and reviewed by SOC Analyst at shift start. Weekly manual review: ISSO reviews SIEM trend reports and investigates any anomalies not resolved by SOC. Monthly: ISSO presents security monitoring summary to ISSM. Quarterly: ISSO presents security status report to AO including audit review findings.
**Evidence:** SIEM daily summary report sample; SIEM alert correlation rules; ISSO weekly review records; monthly ISSM report; quarterly AO security status report
**Status:** ✅ Implemented | **Responsible Party:** SOC Analyst (daily); ISSO (weekly/monthly) | **HIPAA:** §164.308(a)(1)(ii)(D)

---

### AU-6(1) — Automated Process Integration
**Requirement:** Employ automated mechanisms to integrate audit review, analysis, and reporting processes.
**Implementation:** On-premises SIEM automatically ingests all logs from the Audit Logging Server, correlates events across sources, and generates real-time alerts on defined triggers. SIEM dashboards provide live visibility to the SOC team. Alert notification via email and pager integration for high-priority events. Audit review is not manually triggered — it runs continuously.
**Evidence:** SIEM configuration; correlation rule set; alert routing configuration; SIEM dashboard screenshot; pager integration configuration
**Status:** ✅ Implemented | **Responsible Party:** SOC / ISSO | **HIPAA:** §164.308(a)(1)(ii)(D)

---

### AU-7 — Audit Record Reduction and Report Generation
**Requirement:** Provide an audit record reduction and report generation capability that supports on-demand analysis and reporting.
**Implementation:** SIEM provides: full-text log search across all sources; pre-built dashboards for PHI access, auth events, and system health; custom report generation for ISSO and SCA use; log export for forensic investigation in standard formats (JSON, CSV). Audit Server retains raw logs for 2 years in searchable format; archived logs retrievable within 1 hour from S3.
**Evidence:** SIEM reporting interface; pre-built dashboard list; log export capability demonstration; archive retrieval procedure
**Status:** ✅ Implemented | **Responsible Party:** SOC / ISSO | **HIPAA:** §164.308(a)(1)(ii)(D)

---

### AU-8 — Time Stamps
**Requirement:** Use internal system clocks to generate time stamps for audit records; record time stamps that can be mapped to UTC.
**Implementation:** All NEXUS components synchronise time to an internal NTP server (which in turn syncs to a stratum-2 NTP source). Maximum permitted drift is ±1 second. NTP synchronisation status is monitored; a desync alert is triggered if any component drifts beyond threshold. All audit record timestamps are recorded in UTC.
**Evidence:** NTP server configuration; NTP sync configuration on each component; NTP monitoring alert configuration; sample audit record showing UTC timestamp
**Status:** ✅ Implemented | **Responsible Party:** SA | **HIPAA:** §164.312(b)

---

### AU-9 — Protection of Audit Information
**Requirement:** Protect audit information and audit tools from unauthorised access, modification, and deletion.
**Implementation:** The Audit Logging Server is a dedicated server with no other NEXUS functions. Log deletion and modification rights are restricted to the ISSO role — no other role, including SA, can delete logs. All access to the Audit Server is logged (meta-audit). Hash chain (SHA-256) verifies log integrity; broken chain triggers immediate SIEM alert. RAID storage provides redundancy.
**Evidence:** Audit Server access control configuration (ISSO-only deletion); meta-audit configuration; hash chain implementation documentation; SIEM alert for hash failure; RAID configuration
**Status:** ✅ Implemented | **Responsible Party:** ISSO | **HIPAA:** §164.312(b)

---

### AU-9(2) — Store on Separate System
**Requirement:** Store audit records on a component different from the component being audited.
**Implementation:** The Audit Logging Server is physically and logically separate from all other NEXUS components. Logs are collected from source components and forwarded one-way to the Audit Server via TLS-encrypted Syslog. Source components have no write access to the Audit Server beyond the forwarding channel. The Audit Server has no other NEXUS services running on it.
**Evidence:** Network diagram showing Audit Server isolation; Syslog forwarding configuration (one-way); server inventory showing no dual-function on Audit Server
**Status:** ✅ Implemented | **Responsible Party:** ISSO / SA | **HIPAA:** §164.312(b)

---

### AU-10 — Non-Repudiation
**Requirement:** Protect against an individual falsely denying having performed a defined set of actions.
**Implementation:** NEXUS provides non-repudiation for PHI access events through: (1) Unique user IDs — no shared accounts; (2) MFA — access requires a possession factor, making account sharing detectable; (3) Session ID correlation — all events within a session are linked to the authenticated user identity; (4) Audit Server hash chaining — log integrity cannot be disputed; (5) Digital signatures on all clinical document creation and modification events.
**Evidence:** Unique user ID policy; MFA configuration; session ID implementation; hash chain documentation; clinical document digital signature implementation
**Status:** ✅ Implemented | **Responsible Party:** ISSO / SA | **HIPAA:** §164.312(c)(2)

---

### AU-11 — Audit Record Retention
**Requirement:** Retain audit records for a defined period.
**Implementation:** 6-year minimum retention enforced by: Audit Server (0–2 years active); AWS S3 WORM Object Lock (2–4 years near-line); AWS S3 Glacier (4–6 years archive). Deletion only after 6 years with ISSO written approval. Deletion events logged in meta-audit.
**Evidence:** S3 Object Lock policy; Glacier lifecycle transition rule; retention policy; ISSO deletion approval workflow; meta-audit record of deletions
**Status:** ✅ Implemented | **Responsible Party:** ISSO / SA | **HIPAA:** §164.316(b)(2)(i)

---

### AU-12 — Audit Record Generation
**Requirement:** Provide audit record generation capability for defined events; generate audit records for defined events.
**Implementation:** All NEXUS components (Web/App Servers, Primary DB, Secondary DB, Audit Server, SIEM, VPN Gateway, MDM, AD) are configured to generate audit records for all defined event types (per AU-2) and forward them to the Audit Logging Server. Log generation is verified weekly as part of the SIEM review — missing log sources generate a SIEM alert.
**Evidence:** Component-by-component Syslog configuration; SIEM log source inventory; weekly log source verification report; alert for missing log source
**Status:** ✅ Implemented | **Responsible Party:** SA | **HIPAA:** §164.312(b)

---

### AU-13 — Monitoring for Information Disclosure
**Requirement:** Monitor the system to identify unauthorised disclosure of information.
**Implementation:** SIEM correlation rule detects bulk PHI access: any authenticated user accessing >100 distinct patient records in a 10-minute window triggers a high-priority alert to the ISSO and SOC. This rule targets both external attackers using compromised credentials and insider data exfiltration. DLP (Data Loss Prevention) monitoring is applied to outbound traffic from app servers to detect bulk data transmission outside of defined backup destinations.
**Evidence:** SIEM bulk PHI access rule configuration; DLP rule configuration; alert routing documentation; sample alert from test exercise
**Status:** ✅ Implemented | **Responsible Party:** SOC / ISSO | **HIPAA:** §164.308(a)(1)(ii)(D)

---

### AU-14 — Session Audit
**Requirement:** Provide and implement the capability to audit user sessions.
**Implementation:** Full session audit is enabled for privileged user accounts — all keystrokes, commands, and screen content during an administrative session are captured and stored in the Audit Server. Standard clinical sessions are audited at the event level (per AU-2/AU-3). Session audit records for privileged accounts are reviewed by the ISSO monthly and retained for 6 years.
**Evidence:** Privileged session audit configuration; session audit storage on Audit Server; ISSO monthly review log
**Status:** ✅ Implemented | **Responsible Party:** SA / ISSO | **HIPAA:** §164.312(b)

---

## Implementation Status Summary

| Control Family | Selected | Implemented | Partially | Planned |
|---|---|---|---|---|
| AC — Access Control | 23 | 23 | 0 | 0 |
| AT — Awareness and Training | 6 | 6 | 0 | 0 |
| AU — Audit and Accountability | 16 | 16 | 0 | 0 |
| CA — Assessment and Monitoring | 9 | 7 | 2 | 0 |
| CM — Configuration Management | 12 | 12 | 0 | 0 |
| CP — Contingency Planning | 13 | 13 | 0 | 0 |
| IA — Identification and Authentication | 13 | 13 | 0 | 0 |
| IR — Incident Response | 10 | 10 | 0 | 0 |
| MA — Maintenance | 6 | 6 | 0 | 0 |
| MP — Media Protection | 8 | 8 | 0 | 0 |
| PE — Physical and Environmental | 9 | 9 | 0 | 0 |
| PL — Planning | 4 | 4 | 0 | 0 |
| PM — Program Management | 9 | 9 | 0 | 0 |
| PS — Personnel Security | 9 | 9 | 0 | 0 |
| PT — PII Processing | 8 | 8 | 0 | 0 |
| RA — Risk Assessment | 10 | 10 | 0 | 0 |
| SA — System Acquisition | 11 | 11 | 0 | 0 |
| SC — System and Comms Protection | 19 | 19 | 0 | 0 |
| SI — System and Info Integrity | 18 | 18 | 0 | 0 |
| SR — Supply Chain Risk | 8 | 8 | 0 | 0 |
| **TOTAL** | **221** | **219** | **2** | **0** |

> **Note on 2 partially implemented controls:** CA-2 (Security Assessment) and CA-8 (Penetration Testing) are marked partially implemented because the formal annual assessment and first penetration test are conducted in Step 5. The process, methodology, assessor selection, and scope are fully documented and ready — only the execution is pending. This is expected and appropriate at the SSP submission stage.

---

*Document Reference: NEXUS-RMF-IMP-001 | Version 1.0 | Classification: Internal — Controlled*
*This document feeds directly into Step 5 — Security Assessment (NEXUS-RMF-SAR-001)*
