# Risk Register — Reference 5
## NEXUS Electronic Health Records System

| Field | Detail |
|---|---|
| **Document Reference** | NEXUS-RMF-RA-002 — **Reference 5** |
| **Document Type** | Risk Register |
| **System Name** | NEXUS Electronic Health Records System |
| **Version** | 1.0 |
| **Classification** | Internal — Controlled |
| **Methodology** | NIST SP 800-30 Rev 1 |
| **Total Risks** | 28 |
| **Prepared By** | [ISSO Name], Lead Information Security Analyst |
| **Approved By** | [AO Name], Chief Information Officer |
| **Date** | 2025 |
| **Next Review** | 2026 — Annual, or upon significant system change |

---

## Risk Register — Reading Guide

| Column | Description |
|---|---|
| **Risk ID** | Unique identifier for tracking and POA&M reference |
| **Category** | Threat category (Technical / Insider / Physical / Third-Party / Compliance) |
| **Threat Source** | Actor or condition that could cause the adverse event |
| **Threat Event** | Specific adverse event that could occur |
| **Vulnerability Exploited** | Weakness in NEXUS that enables the threat event |
| **Affected Asset** | NEXUS component or data type at risk |
| **NEXUS Zone** | Architecture zone affected (Cloud / On-Premises / Both / Endpoints) |
| **CIA Impact** | Which security objectives are affected (C = Confidentiality, I = Integrity, A = Availability) |
| **Likelihood (L)** | 1–5 scale (1 = Rare, 5 = Almost Certain) |
| **Impact (I)** | 1–5 scale (1 = Negligible, 5 = Catastrophic) |
| **Risk Score** | L × I |
| **Risk Rating** | Critical / High / Medium / Low |
| **Existing Controls** | Current NEXUS controls that reduce this risk |
| **Residual Risk** | Rating after existing controls are applied |
| **Recommended Response** | Additional action required to address residual risk |
| **POA&M Ref** | Reference to POA&M entry if applicable |
| **Risk Owner** | Responsible party for tracking and remediation |

---

## Risk Rating Scale

| Score | Rating | Colour | Action Required |
|---|---|---|---|
| 20–25 | Critical | 🔴 | Immediate remediation or AO formal acceptance with compensating controls |
| 13–19 | High | 🟠 | Remediate within 30 days; POA&M entry required |
| 7–12 | Medium | 🟡 | Remediate within 90 days; POA&M tracked |
| 1–6 | Low | 🟢 | Accept or remediate within 180 days |

---

## Section A — Technical Threats

### R-001 — Ransomware Attack Targeting NEXUS EHR Infrastructure

| Field | Detail |
|---|---|
| **Risk ID** | R-001 |
| **Category** | Technical — Malware |
| **Threat Source** | Organised ransomware group (e.g. LockBit, BlackCat, Rhysida) — healthcare-specialised |
| **Threat Event** | Ransomware deployed across NEXUS environment — database servers encrypted; clinical operations halted |
| **Vulnerability Exploited** | Phishing for initial access; unpatched endpoint for privilege escalation; lateral movement via clinical network to database |
| **Affected Asset** | Primary PostgreSQL DB; Secondary DB; Web/App Servers; Clinical endpoints |
| **NEXUS Zone** | Both — Cloud and On-Premises |
| **CIA Impact** | Confidentiality (PHI exfiltration before encryption — double extortion), Integrity (encrypted/corrupt records), Availability (complete system unavailability) |
| **Likelihood** | 5 — Almost Certain |
| **Impact** | 5 — Catastrophic |
| **Risk Score** | **25** |
| **Risk Rating** | 🔴 **Critical** |
| **Existing Controls** | AWS Shield; WAF; MFA all users; EDR (CrowdStrike) on all servers; daily backups (AWS Backup Vault); S3 WORM; network segmentation; IoT VLAN; SI-3 malicious code protection; CP-9 backups tested quarterly |
| **Residual Risk** | 🟠 High — Controls reduce likelihood significantly but cannot eliminate risk; backup integrity is the primary recovery dependency |
| **Recommended Response** | (1) Ransomware-specific tabletop exercise annually; (2) Verify backup restoration completes within RTO < 4 hours; (3) Consider cyber insurance policy; (4) Engage with H-ISAC for ransomware threat intelligence; (5) Harden IoT VLAN segmentation to eliminate lateral movement path |
| **HIPAA Impact** | Breach Notification Rule — mandatory 60-day HHS notification if PHI accessed |
| **MITRE ATT&CK** | T1566 (Phishing), T1078 (Valid Accounts), T1486 (Data Encrypted for Impact), T1490 (Inhibit System Recovery) |
| **POA&M Ref** | P-001 |
| **Risk Owner** | ISSO / SOC Manager |

---

### R-002 — Insider Threat — Malicious PHI Exfiltration

| Field | Detail |
|---|---|
| **Risk ID** | R-002 |
| **Category** | Insider — Malicious |
| **Threat Source** | Malicious insider — clinical staff, admin staff, or IT personnel with legitimate NEXUS access |
| **Threat Event** | Authorised user systematically exfiltrates patient PHI for financial gain (dark web sale), personal interest (celebrity records), or on behalf of a competitor or criminal organisation |
| **Vulnerability Exploited** | Authorised access to PHI by role; ability to access records beyond immediate care assignment; slow exfiltration below SIEM alert threshold |
| **Affected Asset** | Patient health records; PHI database; billing and demographic data |
| **NEXUS Zone** | On-Premises — Data Tier; Hospital Endpoints |
| **CIA Impact** | Confidentiality (mass PHI exposure), Integrity (audit trail manipulation to hide access) |
| **Likelihood** | 4 — Likely |
| **Impact** | 5 — Catastrophic |
| **Risk Score** | **20** |
| **Risk Rating** | 🔴 **Critical** |
| **Existing Controls** | AU-2 PHI access logging (every record view logged); AU-13 bulk access SIEM detection (>100 records/10 min); AC-3(7) RBAC minimum necessary; quarterly access reviews; AT-2(2) insider threat training; PS-3 background checks; AU-9 tamper-evident audit logs |
| **Residual Risk** | 🟠 High — Slow, deliberate access (1–5 records per session over weeks) can evade bulk-access SIEM rules; authorised access is inherently difficult to distinguish from malicious access |
| **Recommended Response** | (1) Implement User Behaviour Analytics (UBA) — baseline normal access patterns; alert on deviations; (2) Lower SIEM threshold for VIP/sensitive patient record access; (3) Include PHI access pattern analysis in quarterly access reviews; (4) Implement "break-glass" style notification when records outside care assignment are accessed |
| **HIPAA Impact** | Breach Notification — PHI disclosure; potential criminal prosecution under HIPAA §1320d-6 |
| **MITRE ATT&CK** | T1078 (Valid Accounts), T1048 (Exfiltration Over Alternative Protocol), T1070 (Indicator Removal) |
| **POA&M Ref** | P-002 |
| **Risk Owner** | ISSO / SOC Manager |

---

### R-003 — Compromised Clinical Staff Credentials — Phishing / Credential Stuffing

| Field | Detail |
|---|---|
| **Risk ID** | R-003 |
| **Category** | Technical — Credential Attack |
| **Threat Source** | External cybercriminal; ransomware affiliate; nation-state actor |
| **Threat Event** | Clinical staff credentials obtained via phishing or credential stuffing; attacker uses valid credentials to access NEXUS and exfiltrate PHI or establish persistence |
| **Vulnerability Exploited** | Clinical staff are high-value phishing targets (frequent external communications); password reuse across personal and professional accounts; MFA fatigue attacks on push-based MFA |
| **Affected Asset** | Patient records; clinical documentation; NEXUS application |
| **NEXUS Zone** | Cloud — Web/App Servers; Patient portal |
| **CIA Impact** | Confidentiality (PHI access under valid identity), Integrity (record modification under compromised account) |
| **Likelihood** | 5 — Almost Certain |
| **Impact** | 4 — Severe |
| **Risk Score** | **20** |
| **Risk Rating** | 🔴 **Critical** |
| **Existing Controls** | MFA enforced for all users (IA-2(1)(2)); TOTP/FIDO2 only — SMS rejected; AC-7 account lockout (5 attempts); AWS WAF credential stuffing protection; AU-2 failed auth logging; SIEM alert on auth surge; phishing training (AT-2) |
| **Residual Risk** | 🟡 Medium — MFA significantly reduces residual risk; primary residual exposure is MFA fatigue (push bombing) and sophisticated spear-phishing with real-time session capture |
| **Recommended Response** | (1) Migrate privileged accounts to FIDO2 hardware keys (phishing-resistant); (2) Implement MFA fatigue detection in SIEM (>3 MFA push requests in 5 minutes without approval); (3) Quarterly phishing simulation exercises for all clinical staff; (4) Consider number-matching MFA to eliminate push fatigue |
| **HIPAA Impact** | PHI access under compromised credentials constitutes a breach |
| **MITRE ATT&CK** | T1566 (Phishing), T1110.004 (Credential Stuffing), T1621 (MFA Request Generation) |
| **POA&M Ref** | P-003 |
| **Risk Owner** | ISSO / System Administrator |

---

### R-004 — Medical IoT Device Exploitation — Network Pivot to NEXUS

| Field | Detail |
|---|---|
| **Risk ID** | R-004 |
| **Category** | Technical — IoT / OT |
| **Threat Source** | External attacker (ransomware affiliate; nation-state); compromised IoT vendor |
| **Threat Event** | Attacker exploits known or zero-day vulnerability in medical IoT device firmware; uses device as foothold to pivot to hospital LAN; reaches NEXUS database or clinical endpoints |
| **Vulnerability Exploited** | IoT devices run vendor firmware with long update cycles; known CVEs often unpatched; devices have network access to reach NEXUS components; some IoT devices have vendor remote access channels |
| **Affected Asset** | Medical IoT devices (vital signs monitors, infusion pumps, wearables); hospital LAN; NEXUS database |
| **NEXUS Zone** | On-Premises — Hospital Endpoints → Data Tier |
| **CIA Impact** | Confidentiality (PHI access via pivot), Integrity (record manipulation after pivot), Availability (ransomware deployment after pivot) |
| **Likelihood** | 4 — Likely |
| **Impact** | 5 — Catastrophic |
| **Risk Score** | **20** |
| **Risk Rating** | 🔴 **Critical** |
| **Existing Controls** | IoT VLAN network segmentation; network-based IDS on hospital LAN; device certificate authentication; IoT device inventory; SA-22 EOL component tracking; vendor assessment process; SR-6 supplier review |
| **Residual Risk** | 🟠 High — VLAN segmentation reduces pivot path but does not eliminate it; zero-day IoT vulnerabilities bypass all patch-based controls; vendor remote access channels are a persistent risk |
| **Recommended Response** | (1) Implement micro-segmentation — restrict IoT VLAN to only the data flows required (vital signs to DB only; no lateral movement permitted); (2) Disable vendor remote access channels where not operationally required; (3) Complete IoT-specific BAA and security review for all device vendors; (4) Deploy IoT-specific security monitoring (e.g. Claroty, Medigate) |
| **HIPAA Impact** | Any attacker access to PHI via IoT pivot constitutes a HIPAA breach |
| **MITRE ATT&CK for ICS** | T0866 (Exploitation of Remote Services), T0886 (Remote Services), T0843 (Program Download) |
| **POA&M Ref** | P-004 |
| **Risk Owner** | ISSO / System Administrator |

---

### R-005 — Unplanned NEXUS Outage During Active Clinical Care

| Field | Detail |
|---|---|
| **Risk ID** | R-005 |
| **Category** | Technical — Availability |
| **Threat Source** | Hardware failure; software defect; AWS service disruption; network failure |
| **Threat Event** | NEXUS becomes unavailable during active clinical operations; clinical staff cannot access patient records; patient safety risk activated |
| **Vulnerability Exploited** | Dependency on single primary database; potential AWS single-AZ failure; VPN tunnel as single connectivity path; application defect triggered by specific clinical workflow |
| **Affected Asset** | Primary PostgreSQL DB; Web/App Servers; VPN tunnel; all clinical workflows |
| **NEXUS Zone** | Both |
| **CIA Impact** | Availability (primary impact); Integrity (data reconciliation errors after downtime) |
| **Likelihood** | 3 — Possible |
| **Impact** | 5 — Catastrophic |
| **Risk Score** | **15** |
| **Risk Rating** | 🟠 **High** |
| **Existing Controls** | Dual Web/App Servers (ALB load balanced); Secondary DB (streaming replication; RTO <30 min); AWS Backup Vault (RTO <4hr); CP-2 Contingency Plan; CP-10 recovery procedures; clinical downtime procedure binder; quarterly failover tests |
| **Residual Risk** | 🟡 Medium — Dual-server and failover DB reduce single points of failure; residual risk is a simultaneous dual failure or prolonged AWS regional outage |
| **Recommended Response** | (1) Complete AWS multi-AZ deployment for EC2 instances; (2) Test VPN failover to secondary circuit quarterly; (3) Verify clinical downtime procedure currency — update with current patient list process; (4) Establish RTO/RPO metrics dashboard for ISSO monitoring |
| **HIPAA Impact** | Extended unavailability may violate HIPAA contingency plan requirements |
| **MITRE ATT&CK** | N/A — Non-adversarial threat event |
| **POA&M Ref** | P-005 |
| **Risk Owner** | DBA / System Administrator / ISSO |

---

### R-006 — SQL Injection / Web Application Attack Against NEXUS

| Field | Detail |
|---|---|
| **Risk ID** | R-006 |
| **Category** | Technical — Web Application |
| **Threat Source** | External attacker; automated web scanner; ransomware affiliate |
| **Threat Event** | Attacker exploits web application vulnerability (SQL injection, XSS, CSRF) in NEXUS patient portal or clinical web interface to access or modify database records |
| **Vulnerability Exploited** | Web application input validation gaps; NEXUS application code vulnerabilities; unpatched web framework components |
| **Affected Asset** | NEXUS web application; patient portal; PostgreSQL database |
| **NEXUS Zone** | Cloud — Public Subnet |
| **CIA Impact** | Confidentiality (PHI extraction), Integrity (record manipulation), Availability (application disruption) |
| **Likelihood** | 3 — Possible |
| **Impact** | 5 — Catastrophic |
| **Risk Score** | **15** |
| **Risk Rating** | 🟠 **High** |
| **Existing Controls** | AWS WAF (OWASP Top 10 rules including SQLi and XSS); input validation (SI-10); parameterised queries in NEXUS application; TLS 1.2+ on all connections; WAF logging to SIEM; annual penetration test (CA-8) |
| **Residual Risk** | 🟡 Medium — WAF blocks known patterns; custom NEXUS application logic may contain zero-day vulnerabilities not caught by WAF pattern matching |
| **Recommended Response** | (1) Annual penetration test with web application scope (OWASP testing guide); (2) Implement Content Security Policy (CSP) headers; (3) Dynamic Application Security Testing (DAST) in CI/CD pipeline for any NEXUS code changes; (4) Developer security training if any in-house development occurs |
| **HIPAA Impact** | Database breach via SQLi = HIPAA reportable breach |
| **MITRE ATT&CK** | T1190 (Exploit Public-Facing Application), T1059 (Command and Scripting Interpreter) |
| **POA&M Ref** | P-006 |
| **Risk Owner** | ISSO / System Administrator |

---

### R-007 — VPN Tunnel Compromise — Attacker Access to On-Premises Network

| Field | Detail |
|---|---|
| **Risk ID** | R-007 |
| **Category** | Technical — Network |
| **Threat Source** | Nation-state actor; advanced persistent threat (APT); VPN vendor vulnerability |
| **Threat Event** | Attacker compromises VPN gateway credentials or exploits VPN software vulnerability; gains access to on-premises hospital network including PHI database servers |
| **Vulnerability Exploited** | VPN software vulnerabilities (historically high CVE count for VPN products); VPN admin credential exposure; certificate compromise |
| **Affected Asset** | VPN gateway; on-premises network; Primary DB; Secondary DB; Audit Server |
| **NEXUS Zone** | On-Premises — full access if VPN compromised |
| **CIA Impact** | Confidentiality (full PHI access), Integrity (database manipulation), Availability (service disruption) |
| **Likelihood** | 2 — Unlikely |
| **Impact** | 5 — Catastrophic |
| **Risk Score** | **10** |
| **Risk Rating** | 🟡 **Medium** |
| **Existing Controls** | Certificate-based mutual authentication (no password-only VPN); IKEv2/AES-256; VPN patching (RA-5); VPN access logs to SIEM; network-based IDS on LAN segment; MFA for VPN admin access |
| **Residual Risk** | 🟢 Low-Medium — Certificate-based auth significantly reduces credential attack risk; primary residual risk is VPN software zero-day |
| **Recommended Response** | (1) Subscribe to VPN vendor security advisories; patch within 48 hours of critical VPN CVE; (2) Consider Zero Trust Network Access (ZTNA) as long-term VPN replacement; (3) Network segmentation within on-premises LAN to limit blast radius if VPN is compromised |
| **HIPAA Impact** | VPN compromise = potential HIPAA breach depending on attacker actions |
| **MITRE ATT&CK** | T1133 (External Remote Services), T1190 (Exploit Public-Facing Application) |
| **POA&M Ref** | — |
| **Risk Owner** | System Administrator |

---

### R-008 — AWS Misconfiguration — S3 Bucket Public Exposure

| Field | Detail |
|---|---|
| **Risk ID** | R-008 |
| **Category** | Technical — Cloud Misconfiguration |
| **Threat Source** | Unintentional misconfiguration by SA; attacker scanning for exposed S3 buckets |
| **Threat Event** | NEXUS backup data in Amazon S3 accidentally made publicly accessible; PHI archived data exposed to internet |
| **Vulnerability Exploited** | AWS S3 default public access settings (if not explicitly blocked); misconfiguration during provisioning; IAM policy error |
| **Affected Asset** | Amazon S3 backup archive; AWS Backup Vault |
| **NEXUS Zone** | Cloud — Private Subnet |
| **CIA Impact** | Confidentiality (PHI archive exposed) |
| **Likelihood** | 2 — Unlikely |
| **Impact** | 5 — Catastrophic |
| **Risk Score** | **10** |
| **Risk Rating** | 🟡 **Medium** |
| **Existing Controls** | S3 Block Public Access enabled at account level; S3 SSE-KMS encryption with CMK; AWS Config rules monitoring bucket policy changes; AWS CloudTrail logging all S3 API calls; IAM least privilege for S3 access; quarterly AWS security configuration review |
| **Residual Risk** | 🟢 Low — S3 Block Public Access at account level prevents any public exposure regardless of bucket-level settings; encryption means exposed data is still unreadable without CMK |
| **Recommended Response** | (1) Enable AWS Security Hub for continuous S3 misconfiguration detection; (2) Add S3 public access check to monthly ISSO configuration review; (3) Verify S3 Block Public Access is account-level (not just bucket-level) |
| **HIPAA Impact** | S3 PHI exposure = HIPAA breach regardless of whether attacker actually accessed data |
| **MITRE ATT&CK** | T1530 (Data from Cloud Storage Object) |
| **POA&M Ref** | — |
| **Risk Owner** | System Administrator / ISSO |

---

### R-009 — Unpatched Vulnerability Exploitation on NEXUS Servers

| Field | Detail |
|---|---|
| **Risk ID** | R-009 |
| **Category** | Technical — Vulnerability |
| **Threat Source** | Opportunistic attacker; ransomware affiliate; automated exploit kit |
| **Threat Event** | Attacker exploits known unpatched vulnerability on NEXUS EC2 instance or on-premises server to gain initial access or escalate privileges |
| **Vulnerability Exploited** | Delayed patch application; RHEL / Amazon Linux vulnerabilities; web framework CVEs; PostgreSQL vulnerabilities |
| **Affected Asset** | Web/App Servers (EC2); Primary DB Server; Secondary DB Server; SIEM Server |
| **NEXUS Zone** | Both |
| **CIA Impact** | Confidentiality, Integrity, Availability — all three depending on exploitation path |
| **Likelihood** | 3 — Possible |
| **Impact** | 4 — Severe |
| **Risk Score** | **12** |
| **Risk Rating** | 🟡 **Medium** |
| **Existing Controls** | Weekly AWS Inspector + Nessus scans; CISA KEV daily monitoring; patching SLA (Critical: 24-72hr; High: 30 days); AWS Systems Manager Patch Manager; RHEL Satellite; EDR behavioural detection covers some exploit attempts |
| **Residual Risk** | 🟡 Medium — Zero-day vulnerabilities cannot be patched; window between CVE publication and patch application remains |
| **Recommended Response** | (1) Reduce Critical patch window to 24 hours using emergency change procedure; (2) Enable virtual patching (WAF rules for critical CVEs while patch is prepared); (3) Verify CISA KEV correlation is automated in SIEM |
| **HIPAA Impact** | Server compromise likely constitutes HIPAA breach |
| **MITRE ATT&CK** | T1190 (Exploit Public-Facing Application), T1068 (Exploitation for Privilege Escalation) |
| **POA&M Ref** | — |
| **Risk Owner** | System Administrator / ISSO |

---

### R-010 — Clinical Endpoint Malware Infection

| Field | Detail |
|---|---|
| **Risk ID** | R-010 |
| **Category** | Technical — Malware |
| **Threat Source** | Phishing email; malicious USB drive; drive-by download; compromised clinical software update |
| **Threat Event** | Malware (keylogger, RAT, information stealer) installed on clinician laptop or admin workstation; credentials harvested; NEXUS PHI accessed or pivoted to |
| **Vulnerability Exploited** | Clinical staff email habits (opening attachments from patients, labs, insurers); USB port availability; legacy endpoint OS; delayed endpoint patching |
| **Affected Asset** | Clinician laptops; admin workstations; NEXUS credentials stored on endpoint |
| **NEXUS Zone** | On-Premises — Hospital Endpoints |
| **CIA Impact** | Confidentiality (credentials harvested; PHI viewed via compromised session), Integrity (record manipulation via compromised session) |
| **Likelihood** | 4 — Likely |
| **Impact** | 3 — Significant |
| **Risk Score** | **12** |
| **Risk Rating** | 🟡 **Medium** |
| **Existing Controls** | Microsoft Defender for Endpoint (EDR); controlled folder access; USB ports disabled via MDM/GPO; phishing training (AT-2); MFA (credential harvest alone insufficient); email gateway anti-phishing; quarterly endpoint patching |
| **Residual Risk** | 🟡 Medium — EDR and MFA significantly reduce risk; residual exposure is session hijacking (valid MFA session compromised by malware after authentication) |
| **Recommended Response** | (1) Implement application allowlisting on admin workstations; (2) Deploy email attachment sandboxing; (3) Enforce session binding controls (IP/device binding for NEXUS sessions); (4) Quarterly phishing simulation with metrics reported to ISSO |
| **HIPAA Impact** | Malware on endpoint with PHI access = potential HIPAA breach |
| **MITRE ATT&CK** | T1566 (Phishing), T1056 (Input Capture), T1555 (Credentials from Password Stores) |
| **POA&M Ref** | — |
| **Risk Owner** | System Administrator / ISSO |

---

### R-011 — Database Replication Failure — Data Divergence

| Field | Detail |
|---|---|
| **Risk ID** | R-011 |
| **Category** | Technical — Availability / Integrity |
| **Threat Source** | Network failure; hardware fault; software defect in PostgreSQL replication |
| **Threat Event** | PostgreSQL streaming replication between Primary and Secondary DB fails silently; systems diverge; failover to Secondary restores outdated data; clinical decisions based on stale records |
| **Vulnerability Exploited** | Silent replication failure without adequate monitoring; lag detection threshold too high; failover not tested with diverged data |
| **Affected Asset** | Primary DB; Secondary DB; all clinical workflows |
| **NEXUS Zone** | On-Premises — Data Tier |
| **CIA Impact** | Integrity (stale data used for clinical decisions), Availability (failover compromised) |
| **Likelihood** | 2 — Unlikely |
| **Impact** | 4 — Severe |
| **Risk Score** | **8** |
| **Risk Rating** | 🟡 **Medium** |
| **Existing Controls** | SIEM alert on replication lag >5 minutes; DBA daily replication status check; quarterly failover test; CP-9(1) backup restoration test; automated replication monitoring |
| **Residual Risk** | 🟢 Low — Monitoring and alerting significantly reduce silent failure risk; quarterly testing validates failover integrity |
| **Recommended Response** | (1) Reduce replication lag alert threshold to 2 minutes; (2) Include data integrity check (row count comparison) in quarterly failover test; (3) Document and test replication recovery procedure |
| **HIPAA Impact** | Data integrity failure affecting clinical decisions may trigger HIPAA breach investigation |
| **MITRE ATT&CK** | N/A |
| **POA&M Ref** | — |
| **Risk Owner** | DBA |

---

### R-012 — Log Tampering / SIEM Evasion

| Field | Detail |
|---|---|
| **Risk ID** | R-012 |
| **Category** | Technical — Defense Evasion |
| **Threat Source** | Sophisticated attacker post-compromise; privileged insider |
| **Threat Event** | Attacker with elevated access modifies or deletes NEXUS audit logs to conceal activity; SIEM blind spot created; breach goes undetected |
| **Vulnerability Exploited** | Logs co-located with compromised system; excessive log access permissions; gaps in SIEM coverage |
| **Affected Asset** | Audit Logging Server; SIEM; all NEXUS audit records |
| **NEXUS Zone** | On-Premises — Security and Audit |
| **CIA Impact** | Integrity (log tampering), Availability (loss of forensic capability) |
| **Likelihood** | 2 — Unlikely |
| **Impact** | 4 — Severe |
| **Risk Score** | **8** |
| **Risk Rating** | 🟡 **Medium** |
| **Existing Controls** | AU-9(2) dedicated Audit Server; SHA-256 hash chain integrity; ISSO-only deletion rights; SIEM alert on log volume drop >50%; S3 WORM backup of all logs; meta-audit (access to audit server itself is logged) |
| **Residual Risk** | 🟢 Low — Dedicated server plus hash chain plus WORM backup creates three independent barriers to log tampering |
| **Recommended Response** | (1) Ensure SIEM alert for hash chain failure is tested annually; (2) Consider forwarding critical logs to a second geographically separated location; (3) Include log integrity verification in annual assessment |
| **HIPAA Impact** | Log tampering violates HIPAA Audit Controls requirement §164.312(b) |
| **MITRE ATT&CK** | T1070 (Indicator Removal), T1070.001 (Clear Windows Event Logs) |
| **POA&M Ref** | — |
| **Risk Owner** | ISSO |

---

## Section B — Insider Threats

### R-013 — Negligent Insider — Accidental PHI Disclosure

| Field | Detail |
|---|---|
| **Risk ID** | R-013 |
| **Category** | Insider — Negligent |
| **Threat Source** | Clinical or administrative staff — unintentional actions |
| **Threat Event** | Clinical staff accidentally sends PHI to wrong recipient (misdirected email); leaves patient record open on shared terminal; prints and misplaces PHI; uses personal device in violation of policy |
| **Vulnerability Exploited** | Clinical urgency; busy ward environment; insufficient PHI handling awareness; shared workstations in clinical areas |
| **Affected Asset** | PHI in transit; printed PHI; open sessions on shared workstations |
| **NEXUS Zone** | On-Premises — Hospital Endpoints |
| **CIA Impact** | Confidentiality (inadvertent PHI disclosure) |
| **Likelihood** | 5 — Almost Certain |
| **Impact** | 2 — Minor |
| **Risk Score** | **10** |
| **Risk Rating** | 🟡 **Medium** |
| **Existing Controls** | AC-11 device lock (15 minutes); AC-12 session termination (30 minutes); PHI handling training (AT-2); minimum necessary access (AC-6); secure print release; acceptable use policy |
| **Residual Risk** | 🟡 Medium — Session timeouts reduce open-screen risk; email misdirection and printed PHI remain hard to control technically |
| **Recommended Response** | (1) Deploy email DLP to flag potential misdirected PHI (patient name in subject + external recipient); (2) Implement secure print release (badge tap to print) for PHI documents; (3) Refresh PHI handling training annually with real-case scenarios |
| **HIPAA Impact** | Misdirected PHI = HIPAA breach (even if inadvertent); notification required if >500 affected |
| **POA&M Ref** | — |
| **Risk Owner** | Privacy Officer / ISSO |

---

### R-014 — Privileged User Abuse — System Administrator

| Field | Detail |
|---|---|
| **Risk ID** | R-014 |
| **Category** | Insider — Privileged |
| **Threat Source** | Malicious or coerced system administrator |
| **Threat Event** | SA uses privileged access to extract database contents, disable security controls, or create backdoor accounts; abuse is concealed using privileged access to audit logs |
| **Vulnerability Exploited** | Privileged accounts have broad system access; SA role has ability to modify security tool configurations; potential to suppress or modify logs before dedicated Audit Server captures them |
| **Affected Asset** | Primary DB; Security Group configurations; SIEM; user account management |
| **NEXUS Zone** | Both |
| **CIA Impact** | Confidentiality, Integrity, Availability — all three |
| **Likelihood** | 2 — Unlikely |
| **Impact** | 5 — Catastrophic |
| **Risk Score** | **10** |
| **Risk Rating** | 🟡 **Medium** |
| **Existing Controls** | AC-5 separation of duties (SA has no PHI access); AC-2(7) separate privileged accounts; AU-9 ISSO-only log deletion; AU-14 privileged session full audit capture; AC-6(9) all privileged actions logged; PS-3 background checks; quarterly privileged account review |
| **Residual Risk** | 🟡 Medium — SA has no direct PHI access (RBAC enforced); separated Audit Server reduces log manipulation risk; residual risk is SA bypassing application layer and accessing PostgreSQL directly |
| **Recommended Response** | (1) Implement database activity monitoring (DAM) to log all direct PostgreSQL connections including SA-level connections; (2) Require dual approval for direct database access outside of normal maintenance; (3) Include SA access review in quarterly access certification |
| **HIPAA Impact** | Privileged insider PHI access = HIPAA breach; criminal liability |
| **MITRE ATT&CK** | T1078.003 (Valid Accounts — Local Accounts), T1070 (Indicator Removal) |
| **POA&M Ref** | — |
| **Risk Owner** | ISSO / ISSM |

---

### R-015 — Terminated Employee Account Not Deprovisioned

| Field | Detail |
|---|---|
| **Risk ID** | R-015 |
| **Category** | Insider — Process Failure |
| **Threat Source** | Departed employee (voluntary or involuntary); external actor using orphaned credentials |
| **Threat Event** | Former employee retains active NEXUS account after departure; accesses system from outside (to take patient list to competitor, view celebrity records, or act in revenge) |
| **Vulnerability Exploited** | HR-IT deprovisioning process delay; high staff turnover creating volume pressure on timely deprovisioning |
| **Affected Asset** | Active user accounts; PHI accessible under former employee's role |
| **NEXUS Zone** | Both — via external HTTPS access |
| **CIA Impact** | Confidentiality (unauthorised PHI access), Integrity (unauthorised record modification) |
| **Likelihood** | 3 — Possible |
| **Impact** | 3 — Significant |
| **Risk Score** | **9** |
| **Risk Rating** | 🟡 **Medium** |
| **Existing Controls** | AC-2 24-hour deprovisioning SLA (automated HR-IT workflow); AC-2(3) 90-day inactivity auto-disable; quarterly access reviews; MFA (attacker needs physical MFA device too); SIEM alert on after-hours access |
| **Residual Risk** | 🟢 Low — Automated deprovisioning and 90-day inactivity lockout provide two safeguards; MFA means credential alone is insufficient |
| **Recommended Response** | (1) Verify HR-IT automation covers all employment termination types (voluntary, involuntary, contractor); (2) Add same-day deprovisioning for involuntary terminations; (3) Include deprovisioning timeliness in quarterly access review metrics |
| **HIPAA Impact** | Orphaned account access = HIPAA breach |
| **POA&M Ref** | — |
| **Risk Owner** | ISSO / HR |

---

## Section C — Physical Threats

### R-016 — Clinical Endpoint Physical Theft — Laptop or Tablet

| Field | Detail |
|---|---|
| **Risk ID** | R-016 |
| **Category** | Physical — Device Theft |
| **Threat Source** | Opportunistic thief; targeted attacker; disgruntled employee |
| **Threat Event** | Clinician laptop or nurse's tablet stolen from hospital ward, car park, or public area; device contains cached credentials or offline PHI |
| **Vulnerability Exploited** | Hospital wards are semi-public environments; devices left unattended during clinical rounds; PHI potentially cached on device offline |
| **Affected Asset** | Clinician laptops; nurses' tablets; cached credentials or locally stored PHI |
| **NEXUS Zone** | On-Premises — Endpoints |
| **CIA Impact** | Confidentiality (PHI on device; cached credentials enabling NEXUS access) |
| **Likelihood** | 3 — Possible |
| **Impact** | 3 — Significant |
| **Risk Score** | **9** |
| **Risk Rating** | 🟡 **Medium** |
| **Existing Controls** | AC-19 full device encryption (BitLocker Windows; iOS hardware encryption); MDM remote wipe capability; AC-11 device lock (15 minutes); 15-minute session lock; MFA required for NEXUS access (stolen device + stolen password alone insufficient); no offline PHI caching policy |
| **Residual Risk** | 🟢 Low — Full device encryption makes data inaccessible without credentials; MDM remote wipe eliminates residual risk if reported promptly |
| **Recommended Response** | (1) Publish and train staff on the lost device reporting procedure (report within 1 hour); (2) Verify MDM remote wipe capability with quarterly test; (3) Confirm no PHI is cached offline in NEXUS mobile application |
| **HIPAA Impact** | Unencrypted PHI on stolen device = HIPAA breach; encrypted device theft is not reportable if encryption is demonstrated |
| **POA&M Ref** | — |
| **Risk Owner** | System Administrator |

---

### R-017 — Unauthorised Physical Access to On-Premises Data Centre

| Field | Detail |
|---|---|
| **Risk ID** | R-017 |
| **Category** | Physical — Unauthorised Access |
| **Threat Source** | External intruder; tailgating; social engineering of facilities staff |
| **Threat Event** | Unauthorised individual gains physical access to the on-premises data centre housing the Primary DB Server; direct access to server enables credential bypass, hardware tampering, or device theft |
| **Vulnerability Exploited** | Social engineering of security/facilities staff; tailgating; stolen access badge |
| **Affected Asset** | Primary DB Server; Audit Logging Server; SIEM Server; VPN Gateway |
| **NEXUS Zone** | On-Premises — Data Tier |
| **CIA Impact** | Confidentiality, Integrity, Availability — all three if physical access achieved |
| **Likelihood** | 1 — Rare |
| **Impact** | 5 — Catastrophic |
| **Risk Score** | **5** |
| **Risk Rating** | 🟢 **Low** |
| **Existing Controls** | PE-2 badge access control (authorised personnel list maintained); PE-3 CCTV monitoring; PE-6 visitor access records; PE-8 visitor log; locked server racks; alarm system; security guard presence |
| **Residual Risk** | 🟢 Low — Multiple physical controls; locked server racks provide secondary barrier even if room is accessed |
| **Recommended Response** | (1) Review and update authorised personnel list quarterly; (2) Ensure anti-tailgating policy is enforced and trained; (3) Include data centre access log review in monthly ISSO security review |
| **HIPAA Impact** | Physical access to PHI systems = potential HIPAA breach if data accessed or removed |
| **POA&M Ref** | — |
| **Risk Owner** | Facilities / ISSO |

---

### R-018 — Power Outage Affecting On-Premises Infrastructure

| Field | Detail |
|---|---|
| **Risk ID** | R-018 |
| **Category** | Physical — Environmental |
| **Threat Source** | Utility power failure; electrical fault; weather event |
| **Threat Event** | Extended power outage at Hospital Site A causes Primary DB Server and Audit Server to become unavailable; clinical operations affected; failover to Site B required |
| **Vulnerability Exploited** | UPS limited runtime; generator start time; simultaneous power failure at both sites (major weather event) |
| **Affected Asset** | Primary DB Server; Audit Server; SIEM; VPN Gateway (Site A) |
| **NEXUS Zone** | On-Premises — Site A |
| **CIA Impact** | Availability (primary), Integrity (data consistency during unplanned shutdown) |
| **Likelihood** | 2 — Unlikely |
| **Impact** | 3 — Significant |
| **Risk Score** | **6** |
| **Risk Rating** | 🟢 **Low** |
| **Existing Controls** | PE-11 UPS (30-minute battery backup); generator (auto-start, 8-hour fuel); PE-9 redundant power feeds; Secondary DB at Site B (separate power infrastructure); CP-7 alternate processing (AWS); CP-10 recovery procedures |
| **Residual Risk** | 🟢 Low — UPS and generator provide >8-hour protection; Secondary DB at separate site; AWS cloud tier unaffected |
| **Recommended Response** | (1) Test generator auto-start and runtime annually; (2) Verify UPS battery health quarterly; (3) Document clean shutdown procedure for planned power maintenance |
| **HIPAA Impact** | Extended unavailability may require activation of HIPAA contingency plan provisions |
| **POA&M Ref** | — |
| **Risk Owner** | Facilities / System Administrator |

---

## Section D — Third-Party and Supply Chain Threats

### R-019 — Business Associate (Lab System) Breach — PHI Transmission Interception

| Field | Detail |
|---|---|
| **Risk ID** | R-019 |
| **Category** | Third-Party — Business Associate |
| **Threat Source** | External attacker targeting laboratory system; compromised lab interface |
| **Threat Event** | External laboratory system (connected to NEXUS via HL7 interface) is breached; PHI transmitted between NEXUS and the lab is intercepted or the lab provides corrupted result data back to NEXUS |
| **Vulnerability Exploited** | Third-party systems have different security postures; HL7 interface may have weaker authentication than NEXUS internal controls |
| **Affected Asset** | Lab orders and results transmitted to/from NEXUS; patient records updated with lab results |
| **NEXUS Zone** | Both — via third-party connection |
| **CIA Impact** | Confidentiality (PHI in transit), Integrity (falsified lab results entering NEXUS) |
| **Likelihood** | 2 — Unlikely |
| **Impact** | 4 — Severe |
| **Risk Score** | **8** |
| **Risk Rating** | 🟡 **Medium** |
| **Existing Controls** | BAA with laboratory systems; TLS encryption on all HL7 transmission; CA-3 interconnection documented; SA-9 third-party service controls; SR-6 annual supplier review |
| **Residual Risk** | 🟡 Medium — NEXUS controls cover the NEXUS side of the connection; lab system security is outside NEXUS control and relies on BAA contractual requirements |
| **Recommended Response** | (1) Include lab system security assessment in annual supplier review (SR-6); (2) Require labs to demonstrate SOC 2 Type II or equivalent; (3) Implement result plausibility checking (clinical decision support alerts on extreme lab values) |
| **HIPAA Impact** | PHI breach via BAA partner = Nexus Health System may still be liable |
| **POA&M Ref** | — |
| **Risk Owner** | ISSO / System Owner |

---

### R-020 — Software Supply Chain Attack — NEXUS Application Update

| Field | Detail |
|---|---|
| **Risk ID** | R-020 |
| **Category** | Third-Party — Supply Chain |
| **Threat Source** | Nation-state actor; advanced persistent threat targeting healthcare software supply chain |
| **Threat Event** | NEXUS application update or third-party library update is compromised at the vendor/repository level; malicious code is introduced into NEXUS via trusted update channel (similar to SolarWinds, MOVEit attacks) |
| **Vulnerability Exploited** | Trust in vendor-signed updates; open-source library dependencies; automated update processes without code review |
| **Affected Asset** | NEXUS application code; all components running NEXUS software |
| **NEXUS Zone** | Both |
| **CIA Impact** | Confidentiality, Integrity, Availability — all three via backdoor |
| **Likelihood** | 2 — Unlikely |
| **Impact** | 5 — Catastrophic |
| **Risk Score** | **10** |
| **Risk Rating** | 🟡 **Medium** |
| **Existing Controls** | SA-10 developer configuration management; SA-11 developer testing; SR-3 supply chain controls; CM-3 change control (CAB approval for all updates); SI-7(1) FIM detects unexpected file changes post-update; SR-11 component authenticity verification |
| **Residual Risk** | 🟡 Medium — Sophisticated supply chain attacks (signed malicious updates) can bypass signature verification; FIM provides post-deployment detection |
| **Recommended Response** | (1) Implement software bill of materials (SBOM) for NEXUS application; (2) Subscribe to vendor security advisories and H-ISAC supply chain alerts; (3) Stage updates through dev/test environment before production deployment; (4) Verify FIM baseline update process is enforced for all updates |
| **HIPAA Impact** | Backdoor = potential mass PHI breach; HIPAA criminal liability |
| **MITRE ATT&CK** | T1195 (Supply Chain Compromise), T1195.002 (Compromise Software Supply Chain) |
| **POA&M Ref** | — |
| **Risk Owner** | System Administrator / ISSO |

---

### R-021 — Cloud Provider (AWS) Service Outage

| Field | Detail |
|---|---|
| **Risk ID** | R-021 |
| **Category** | Third-Party — Cloud Provider |
| **Threat Source** | AWS infrastructure failure (non-adversarial) |
| **Threat Event** | AWS us-east-1 regional outage causes NEXUS Web/App Servers and Backup Vault to become unavailable; on-premises DB still operational but clinical web interface inaccessible |
| **Vulnerability Exploited** | Single AWS region dependency; all cloud components in one region |
| **Affected Asset** | Web/App Servers; AWS Backup Vault; Patient portal |
| **NEXUS Zone** | Cloud |
| **CIA Impact** | Availability (web interface unavailable; backups inaccessible during outage) |
| **Likelihood** | 2 — Unlikely |
| **Impact** | 3 — Significant |
| **Risk Score** | **6** |
| **Risk Rating** | 🟢 **Low** |
| **Existing Controls** | CP-7 alternate processing (AWS us-east-2 backup region available); CP-6 alternate storage; AWS multi-AZ within us-east-1; clinical downtime procedures |
| **Residual Risk** | 🟢 Low — On-premises DB remains operational; clinical downtime procedure provides fallback |
| **Recommended Response** | (1) Deploy NEXUS EC2 instances across two AWS AZs within us-east-1 (immediate); (2) Define activation criteria for AWS us-east-2 regional failover in contingency plan; (3) Verify RTO for cross-region failover |
| **HIPAA Impact** | Extended cloud outage may trigger contingency plan provisions |
| **POA&M Ref** | P-005 (linked) |
| **Risk Owner** | System Administrator |

---

## Section E — Compliance and Legal Threats

### R-022 — HIPAA Breach — HHS OCR Investigation and Penalty

| Field | Detail |
|---|---|
| **Risk ID** | R-022 |
| **Category** | Compliance — Regulatory |
| **Threat Source** | HIPAA compliance failure; any of the technical risks above if not properly mitigated |
| **Threat Event** | NEXUS-related PHI breach triggers HHS OCR investigation; OCR determines inadequate safeguards; civil monetary penalties imposed; corrective action plan required |
| **Vulnerability Exploited** | Any technical or administrative control gap; inadequate breach notification; failure to conduct annual risk analysis |
| **Affected Asset** | Organisational operations; financial resources; operating licence; public trust |
| **NEXUS Zone** | Both |
| **CIA Impact** | All — regulatory consequence of any security failure |
| **Likelihood** | 3 — Possible |
| **Impact** | 4 — Severe |
| **Risk Score** | **12** |
| **Risk Rating** | 🟡 **Medium** |
| **Existing Controls** | Full HIPAA Security Rule compliance programme; annual risk assessment (this document); annual SCA assessment (CA-2); HIPAA training (AT-2); Privacy Officer; 60-day breach notification procedure (IR-6); BAAs in place |
| **Residual Risk** | 🟡 Medium — No programme fully eliminates regulatory risk; OCR investigations can arise from patient complaints as well as confirmed breaches |
| **Recommended Response** | (1) Maintain current annual risk assessment; (2) Ensure breach notification procedures are tested in annual IR tabletop; (3) Consider HIPAA compliance audit (pre-OCR mock audit) every 2–3 years; (4) Maintain documentation of all security activities for OCR production request |
| **HIPAA Impact** | This risk IS a HIPAA compliance failure |
| **POA&M Ref** | — |
| **Risk Owner** | Privacy Officer / ISSO / AO |

---

### R-023 — State Health Information Law Violation

| Field | Detail |
|---|---|
| **Risk ID** | R-023 |
| **Category** | Compliance — Regulatory |
| **Threat Source** | State attorney general investigation; patient complaint |
| **Threat Event** | NEXUS operation violates state-level health information privacy law (which may be stricter than HIPAA in some states); state-level penalties imposed |
| **Vulnerability Exploited** | State law requirements not fully mapped to NEXUS controls; updates to state law not monitored |
| **Affected Asset** | Organisational operations; financial resources |
| **NEXUS Zone** | Both |
| **CIA Impact** | Confidentiality (primary) |
| **Likelihood** | 2 — Unlikely |
| **Impact** | 3 — Significant |
| **Risk Score** | **6** |
| **Risk Rating** | 🟢 **Low** |
| **Existing Controls** | Legal counsel review of applicable state laws; HIPAA provides federal minimum floor; Privacy Officer oversight |
| **Residual Risk** | 🟢 Low — HIPAA compliance covers the majority of state requirements; state-specific gaps managed by legal counsel |
| **Recommended Response** | (1) Annual legal review of state health information laws applicable to all operating states; (2) Brief ISSO on any state law requirements that exceed HIPAA |
| **HIPAA Impact** | Indirect — state violations often co-occur with HIPAA issues |
| **POA&M Ref** | — |
| **Risk Owner** | Privacy Officer / Legal Counsel |

---

## Section F — Additional Identified Risks

### R-024 through R-028 — Summary Table

The following additional risks were identified and rated during the assessment:

| Risk ID | Risk Title | Threat Source | L | I | Score | Rating | Controls | Risk Owner |
|---|---|---|---|---|---|---|---|---|
| R-024 | DDoS attack against patient portal | Hacktivist group; botnet operator | 3 | 3 | 9 | 🟡 Medium | AWS Shield Standard; WAF rate limiting; ALB scaling | SA |
| R-025 | Phishing-resistant MFA not deployed for all privileged accounts | Configuration gap | 3 | 3 | 9 | 🟡 Medium | TOTP MFA in place; FIDO2 hardware keys not yet universal | ISSO / SA |
| R-026 | Medical IoT device BAA gaps (3 vendors) | Vendor non-compliance | 3 | 2 | 6 | 🟢 Low | Vendor assessment in progress (PRE-001) | ISSO |
| R-027 | Loss of audit log integrity during SIEM maintenance | Maintenance window gap | 2 | 3 | 6 | 🟢 Low | SIEM maintenance scheduled during lowest-activity period; Audit Server continues logging to local buffer | ISSO |
| R-028 | Nurse tablet lost or stolen — patient list accessed | Device loss | 3 | 2 | 6 | 🟢 Low | Full device encryption; MDM remote wipe; MFA required for NEXUS | SA |

---

## Risk Register Summary Dashboard

```
╔══════════════════════════════════════════════════════════════════╗
║           NEXUS EHR — RISK REGISTER SUMMARY                     ║
║           Reference 5 | NEXUS-RMF-RA-002 | 2025                 ║
╠══════════════════════════════════════════════════════════════════╣
║  Total Risks Identified:       28                               ║
║                                                                  ║
║  🔴 Critical  (Score 20–25):    4 risks   (14%)                 ║
║     R-001 Ransomware            Score: 25  ████████████████████  ║
║     R-002 Insider — malicious   Score: 20  ████████████████      ║
║     R-003 Credential attack     Score: 20  ████████████████      ║
║     R-004 IoT exploitation      Score: 20  ████████████████      ║
║                                                                  ║
║  🟠 High      (Score 13–19):   10 risks   (36%)                 ║
║     R-005 Unplanned outage      Score: 15  ████████████          ║
║     R-006 SQL injection         Score: 15  ████████████          ║
║     R-007 VPN compromise        Score: 10  (after controls: Med) ║
║     R-010 Endpoint malware      Score: 12  █████████             ║
║     [+ 6 additional High risks]                                  ║
║                                                                  ║
║  🟡 Medium    (Score 7–12):    11 risks   (39%)                 ║
║  🟢 Low       (Score 1–6):      3 risks   (11%)                 ║
╠══════════════════════════════════════════════════════════════════╣
║  Primary Threat Vectors:                                         ║
║  • Ransomware / Malware      • Insider threat                   ║
║  • Credential compromise     • Medical IoT exploitation         ║
║  • Third-party / supply chain• Regulatory compliance            ║
╚══════════════════════════════════════════════════════════════════╝
```

---

## Approval and Sign-Off

| Role | Name | Signature | Date |
|---|---|---|---|
| Prepared By | [Chioma Otteh] | _________________________ | 2026 |
| Reviewed By | [Jack Taylor] | _________________________ | 2026 |
| Reviewed By | [Jack TAylor] | _________________________ | 2026 |
| Reviewed By | [Jane PAul] | _________________________ | 2026 |
| **Approved By (AO)** | **[Ben Jackson]** | _________________________ | **2026** |

---

## Review and Maintenance Schedule

| Trigger | Action |
|---|---|
| Annually | Full risk register review; update likelihood based on current threat intelligence |
| New vulnerability identified (CISA KEV) | Assess impact on existing risk entries; add new risk entry if not covered |
| Security incident | Post-incident review; update affected risk entries; add new risks if uncovered |
| Significant system change | Re-assess risks for affected components within 30 days |
| New third-party connection | Add third-party risk entry; assess integration risks |
| Regulatory change (HIPAA/state) | Review compliance risk entries |

---

*Document Reference: NEXUS-RMF-RA-002 — Reference 5 | Version 1.0 | Classification: Internal — Controlled*
*NEXUS EHR is a fictional system created for a GRC portfolio demonstration. All names, data, and system details are illustrative only.*
