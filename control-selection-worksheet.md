# Control Selection Worksheet
## NEXUS Electronic Health Records System | Step 3 — Select Controls

| Field | Detail |
|---|---|
| **Document Reference** | NEXUS-RMF-SEL-003 |
| **Document Type** | Control Selection Worksheet |
| **Version** | 1.0 |
| **Baseline** | NIST SP 800-53 Rev 5 — HIGH Impact Baseline |
| **Classification** | Internal — Controlled |
| **Prepared By** | [ISSO Name] |
| **Date** | 2025 |

---

> **Purpose:** This worksheet provides a concise, at-a-glance record of every control selected for NEXUS, its implementation status, and the responsible party. It is the working reference document used during Step 4 (Implementation) and Step 5 (Assessment). The full justification for each tailoring decision is in the [Tailoring Decisions Log](./tailoring-decisions.md).

---

## Status Key

| Symbol | Meaning |
|---|---|
| ✅ | Selected — HIGH baseline; to be implemented |
| ➕ | Added or Enhanced — beyond HIGH baseline (tailoring) |
| 🔵 | Inherited — AWS common control |
| ⬜ | Scoped out — not applicable |
| 🔄 | In Progress — implementation underway (Step 4) |
| ✔️ | Implemented — confirmed in Step 4 |

---

## AC — Access Control

| Control ID | Control Name | Selected | Tailoring | Owner | Step 4 Status |
|---|---|---|---|---|---|
| AC-1 | Access Control Policy and Procedures | ✅ | None | ISSO | 🔄 |
| AC-2 | Account Management | ✅ | Enhanced | ISSO / SA | 🔄 |
| AC-2(1) | Automated System Account Management | ➕ | Added | SA | 🔄 |
| AC-2(3) | Disable Inactive Accounts | ✅ | None | SA | 🔄 |
| AC-2(7) | Privileged User Accounts | ➕ | Added (TD-010) | ISSO | 🔄 |
| AC-3 | Access Enforcement | ✅ | None | SA | 🔄 |
| AC-3(7) | Role-Based Access Control | ➕ | Added | ISSO | 🔄 |
| AC-4 | Information Flow Enforcement | ✅ | None | SA | 🔄 |
| AC-5 | Separation of Duties | ✅ | None | ISSO | 🔄 |
| AC-6 | Least Privilege | ✅ | None | ISSO | 🔄 |
| AC-6(1) | Authorise Access to Security Functions | ➕ | Added | ISSO | 🔄 |
| AC-6(5) | Privileged Accounts | ✅ | None | ISSO | 🔄 |
| AC-6(9) | Log Use of Privileged Functions | ➕ | Added | ISSO / SA | 🔄 |
| AC-7 | Unsuccessful Login Attempts | ✅ | None | SA | 🔄 |
| AC-8 | System Use Notification | ✅ | None | SA | 🔄 |
| AC-11 | Device Lock | ✅ | None | SA | 🔄 |
| AC-12 | Session Termination | ✅ | None | SA | 🔄 |
| AC-14 | Permitted Actions Without Identification | ✅ | None | ISSO | 🔄 |
| AC-17 | Remote Access | ✅ | None | SA | 🔄 |
| AC-18 | Wireless Access | ✅ | None | SA | 🔄 |
| AC-19 | Access Control for Mobile Devices | ✅ | None | SA | 🔄 |
| AC-20 | Use of External Systems | ✅ | None | ISSO | 🔄 |
| AC-22 | Publicly Accessible Content | ✅ | None | ISSO | 🔄 |

---

## AT — Awareness and Training

| Control ID | Control Name | Selected | Tailoring | Owner | Step 4 Status |
|---|---|---|---|---|---|
| AT-1 | Awareness and Training Policy | ✅ | None | ISSO | 🔄 |
| AT-2 | Literacy Training and Awareness | ✅ | None | ISSO / HR | 🔄 |
| AT-2(2) | Insider Threat Awareness | ➕ | Added | ISSO | 🔄 |
| AT-3 | Role-Based Training | ✅ | None | ISSO / HR | 🔄 |
| AT-4 | Training Records | ✅ | None | HR | 🔄 |
| AT-6 | Training Feedback | ✅ | None | ISSO | 🔄 |

---

## AU — Audit and Accountability

| Control ID | Control Name | Selected | Tailoring | Owner | Step 4 Status |
|---|---|---|---|---|---|
| AU-1 | Audit and Accountability Policy | ✅ | None | ISSO | 🔄 |
| AU-2 | Event Logging | ✅ | None | ISSO / SA | 🔄 |
| AU-3 | Content of Audit Records | ✅ | None | ISSO / SA | 🔄 |
| AU-4 | Audit Log Storage Capacity | ✅ | None | SA | 🔄 |
| AU-5 | Response to Audit Processing Failures | ✅ | None | ISSO | 🔄 |
| AU-6 | Audit Record Review, Analysis, Reporting | ✅ | None | ISSO / SOC | 🔄 |
| AU-6(1) | Automated Process Integration | ➕ | Added | SOC | 🔄 |
| AU-7 | Audit Record Reduction and Report Generation | ✅ | None | SOC | 🔄 |
| AU-8 | Time Stamps | ✅ | None | SA | 🔄 |
| AU-9 | Protection of Audit Information | ✅ | None | ISSO | 🔄 |
| AU-9(2) | Store on Separate System | ➕ | Added (TD-003) | ISSO / SA | 🔄 |
| AU-10 | Non-Repudiation | ✅ | None | ISSO / SA | 🔄 |
| AU-11 | Audit Record Retention | ➕ | Added (TD-002) | ISSO | 🔄 |
| AU-12 | Audit Record Generation | ✅ | None | SA | 🔄 |
| AU-13 | Monitoring for Information Disclosure | ➕ | Added (TD-004) | SOC | 🔄 |
| AU-14 | Session Audit | ✅ | None | SA | 🔄 |

---

## CA — Assessment, Authorisation, and Monitoring

| Control ID | Control Name | Selected | Tailoring | Owner | Step 4 Status |
|---|---|---|---|---|---|
| CA-1 | Policy and Procedures | ✅ | None | ISSO | 🔄 |
| CA-2 | Control Assessments | ✅ | None | SCA / ISSO | 🔄 |
| CA-2(1) | Independent Assessors | ➕ | Added | ISSO | 🔄 |
| CA-3 | Information Exchange | ✅ | None | ISSO | 🔄 |
| CA-5 | Plan of Action and Milestones | ✅ | None | ISSO | 🔄 |
| CA-6 | Authorisation | ✅ | None | AO | 🔄 |
| CA-7 | Continuous Monitoring | ✅ | None | ISSO / SOC | 🔄 |
| CA-8 | Penetration Testing | ➕ | Added (TD-009) | ISSO / Third Party | 🔄 |
| CA-9 | Internal System Connections | ✅ | None | ISSO / SA | 🔄 |

---

## CM — Configuration Management

| Control ID | Control Name | Selected | Tailoring | Owner | Step 4 Status |
|---|---|---|---|---|---|
| CM-1 | Configuration Management Policy | ✅ | None | ISSO | 🔄 |
| CM-2 | Baseline Configuration | ✅ | None | SA | 🔄 |
| CM-2(2) | Automation Support | ➕ | Added | SA | 🔄 |
| CM-3 | Configuration Change Control | ✅ | None | SA / CAB | 🔄 |
| CM-4 | Impact Analysis | ✅ | None | ISSO / SA | 🔄 |
| CM-5 | Access Restrictions for Change | ✅ | None | SA | 🔄 |
| CM-6 | Configuration Settings | ✅ | None | SA | 🔄 |
| CM-7 | Least Functionality | ✅ | None | SA | 🔄 |
| CM-8 | System Component Inventory | ✅ | None | SA | 🔄 |
| CM-9 | Configuration Management Plan | ✅ | None | SA | 🔄 |
| CM-10 | Software Usage Restrictions | ✅ | None | SA | 🔄 |
| CM-12 | Information Location | ➕ | Added | ISSO | 🔄 |

---

## CP — Contingency Planning

| Control ID | Control Name | Selected | Tailoring | Owner | Step 4 Status |
|---|---|---|---|---|---|
| CP-1 | Contingency Planning Policy | ✅ | None | ISSO | 🔄 |
| CP-2 | Contingency Plan | ✅ | None | ISSO / DBA | 🔄 |
| CP-2(1) | Coordinate with Related Plans | ➕ | Added | ISSO | 🔄 |
| CP-3 | Contingency Training | ✅ | None | ISSO / HR | 🔄 |
| CP-4 | Contingency Plan Testing | ✅ | None | ISSO | 🔄 |
| CP-6 | Alternate Storage Site | ✅ | None | SA / DBA | 🔄 |
| CP-7 | Alternate Processing Site | ✅ | None | SA / DBA | 🔄 |
| CP-8 | Telecommunications Services | ✅ | None | SA | 🔄 |
| CP-9 | System Backup | ✅ | None | DBA | 🔄 |
| CP-9(1) | Testing for Reliability | ➕ | Added (TD-015) | DBA / ISSO | 🔄 |
| CP-10 | System Recovery and Reconstitution | ✅ | None | DBA / SA | 🔄 |
| CP-11 | Alternate Communications Protocols | ✅ | None | SA | 🔄 |
| CP-13 | Alternative Security Mechanisms | ➕ | Added | ISSO / Clinical Lead | 🔄 |

---

## IA — Identification and Authentication

| Control ID | Control Name | Selected | Tailoring | Owner | Step 4 Status |
|---|---|---|---|---|---|
| IA-1 | Policy and Procedures | ✅ | None | ISSO | 🔄 |
| IA-2 | Identification and Authentication | ✅ | None | SA | 🔄 |
| IA-2(1) | MFA — Privileged Accounts | ✅ | None | SA | 🔄 |
| IA-2(2) | MFA — Non-Privileged Accounts | ➕ | Added (TD-001) | SA | 🔄 |
| IA-2(6) | Separate Device for MFA | ➕ | Added | SA | 🔄 |
| IA-2(8) | Replay Resistant | ✅ | None | SA | 🔄 |
| IA-3 | Device Identification and Authentication | ✅ | None | SA | 🔄 |
| IA-4 | Identifier Management | ✅ | None | SA | 🔄 |
| IA-5 | Authenticator Management | ✅ | None | SA | 🔄 |
| IA-5(1) | Password-Based Authentication | ✅ | None | SA | 🔄 |
| IA-6 | Authentication Feedback | ✅ | None | SA | 🔄 |
| IA-7 | Cryptographic Module Authentication | ✅ | None | SA | 🔄 |
| IA-8 | Non-Organisational User Authentication | ✅ | None | SA | 🔄 |

---

## IR — Incident Response

| Control ID | Control Name | Selected | Tailoring | Owner | Step 4 Status |
|---|---|---|---|---|---|
| IR-1 | Incident Response Policy | ✅ | None | ISSO | 🔄 |
| IR-2 | Incident Response Training | ✅ | None | ISSO / HR | 🔄 |
| IR-3 | Incident Response Testing | ✅ | None | ISSO / SOC | 🔄 |
| IR-4 | Incident Handling | ✅ | None | SOC Manager | 🔄 |
| IR-4(1) | Automated Incident Handling | ➕ | Added | SOC | 🔄 |
| IR-5 | Incident Monitoring | ✅ | None | SOC | 🔄 |
| IR-6 | Incident Reporting | ✅ | Enhanced (TD-007) | ISSO / Privacy Officer | 🔄 |
| IR-6(1) | Automated Reporting | ➕ | Added (TD-008) | SOC | 🔄 |
| IR-7 | Incident Response Assistance | ✅ | None | ISSO | 🔄 |
| IR-8 | Incident Response Plan | ✅ | None | ISSO | 🔄 |

---

## MA — Maintenance

| Control ID | Control Name | Selected | Tailoring | Owner | Step 4 Status |
|---|---|---|---|---|---|
| MA-1 | Maintenance Policy | 🔵 AWS / ✅ | Inherited (cloud) | SA / AWS | 🔄 |
| MA-2 | Controlled Maintenance | 🔵 AWS / ✅ | Inherited (cloud) | SA / AWS | 🔄 |
| MA-3 | Maintenance Tools | ✅ | None | SA | 🔄 |
| MA-4 | Nonlocal Maintenance | ✅ | None | SA | 🔄 |
| MA-5 | Maintenance Personnel | ✅ | None | SA | 🔄 |
| MA-6 | Timely Maintenance | 🔵 AWS / ✅ | Inherited (cloud) | SA / AWS | 🔄 |

---

## MP — Media Protection

| Control ID | Control Name | Selected | Tailoring | Owner | Step 4 Status |
|---|---|---|---|---|---|
| MP-1 | Media Protection Policy | ✅ | None | ISSO | 🔄 |
| MP-2 | Media Access | ✅ | None | SA | 🔄 |
| MP-3 | Media Marking | ✅ | None | SA | 🔄 |
| MP-4 | Media Storage | ✅ | None | SA | 🔄 |
| MP-5 | Media Transport | ✅ | None | SA | 🔄 |
| MP-6 | Media Sanitisation | ✅ | None | SA | 🔄 |
| MP-7 | Media Use | ✅ | None | SA | 🔄 |
| MP-8 | Media Downgrading | ✅ | None | SA | 🔄 |

---

## PE — Physical and Environmental Protection

| Control ID | Control Name | Selected | Tailoring | Owner | Step 4 Status |
|---|---|---|---|---|---|
| PE-1 | PE Policy | 🔵 AWS / ✅ | Inherited (TD-019) | Facilities / AWS | 🔄 |
| PE-2 | Physical Access Authorisations | 🔵 AWS / ✅ | Inherited (cloud) + NEXUS (on-prem) | Facilities | 🔄 |
| PE-3 | Physical Access Control | 🔵 AWS / ✅ | Inherited (cloud) + NEXUS (on-prem) | Facilities | 🔄 |
| PE-6 | Monitoring Physical Access | 🔵 AWS / ✅ | Inherited (cloud) + NEXUS (on-prem) | Facilities | 🔄 |
| PE-8 | Visitor Access Records | ✅ | None | Facilities | 🔄 |
| PE-9 | Power Equipment | 🔵 AWS / ✅ | Inherited (cloud) + NEXUS (on-prem) | Facilities | 🔄 |
| PE-11 | Emergency Power | 🔵 AWS / ✅ | Inherited (cloud) + NEXUS (on-prem) | Facilities | 🔄 |
| PE-13 | Fire Protection | 🔵 AWS / ✅ | Inherited (cloud) + NEXUS (on-prem) | Facilities | 🔄 |
| PE-14 | Environmental Controls | 🔵 AWS / ✅ | Inherited (cloud) + NEXUS (on-prem) | Facilities | 🔄 |

---

## PL — Planning

| Control ID | Control Name | Selected | Tailoring | Owner | Step 4 Status |
|---|---|---|---|---|---|
| PL-1 | Planning Policy | ✅ | None | ISSO | 🔄 |
| PL-2 | System Security and Privacy Plans | ✅ | None | ISSO | 🔄 |
| PL-4 | Rules of Behaviour | ✅ | None | ISSO / HR | 🔄 |
| PL-8 | Security and Privacy Architectures | ✅ | None | ISSO / SA | 🔄 |

---

## PM — Program Management

| Control ID | Control Name | Selected | Tailoring | Owner | Step 4 Status |
|---|---|---|---|---|---|
| PM-1 | Information Security Program Plan | ✅ | None | ISSM | 🔄 |
| PM-2 | IS Program Leadership Roles | ✅ | None | ISSM | 🔄 |
| PM-3 | IS and Privacy Resources | ✅ | None | ISSM | 🔄 |
| PM-5 | System Inventory | ✅ | None | ISSO | 🔄 |
| PM-9 | Risk Management Strategy | ✅ | None | ISSM / ISSO | 🔄 |
| PM-10 | Authorisation Process | ✅ | None | AO / ISSO | 🔄 |
| PM-14 | Testing, Training, and Monitoring | ✅ | None | ISSO | 🔄 |
| PM-15 | Contacts with Security Groups | ✅ | None | ISSO | 🔄 |
| PM-16 | Threat Awareness Program | ➕ | Added (TD-012) | ISSO | 🔄 |

---

## PS — Personnel Security

| Control ID | Control Name | Selected | Tailoring | Owner | Step 4 Status |
|---|---|---|---|---|---|
| PS-1 | Personnel Security Policy | ✅ | None | HR / ISSO | 🔄 |
| PS-2 | Position Risk Designation | ✅ | None | HR | 🔄 |
| PS-3 | Personnel Screening | ✅ | None | HR | 🔄 |
| PS-4 | Personnel Termination | ✅ | None | HR / SA | 🔄 |
| PS-5 | Personnel Transfer | ✅ | None | HR / ISSO | 🔄 |
| PS-6 | Access Agreements | ✅ | None | HR | 🔄 |
| PS-7 | External Personnel Security | ✅ | None | ISSO | 🔄 |
| PS-8 | Personnel Sanctions | ✅ | None | HR | 🔄 |
| PS-9 | Position Descriptions | ✅ | None | HR | 🔄 |

---

## PT — PII Processing and Transparency

| Control ID | Control Name | Selected | Tailoring | Owner | Step 4 Status |
|---|---|---|---|---|---|
| PT-1 | Policy and Procedures | ✅ | None | Privacy Officer | 🔄 |
| PT-2 | Authority to Process PII | ✅ | None | Privacy Officer | 🔄 |
| PT-3 | PII Processing Purposes | ✅ | None | Privacy Officer | 🔄 |
| PT-4 | Consent for PII Processing | ✅ | None | Privacy Officer | 🔄 |
| PT-5 | Privacy Notice | ✅ | None | Privacy Officer | 🔄 |
| PT-6 | System of Records Notice | ✅ | None | Privacy Officer | 🔄 |
| PT-7 | Specific Categories of PII | ➕ | Added (TD-013) | Privacy Officer | 🔄 |
| PT-8 | Computer Matching Requirements | ✅ | None | Privacy Officer | 🔄 |

---

## RA — Risk Assessment

| Control ID | Control Name | Selected | Tailoring | Owner | Step 4 Status |
|---|---|---|---|---|---|
| RA-1 | Risk Assessment Policy | ✅ | None | ISSO | 🔄 |
| RA-2 | Security Categorisation | ✅ | None | ISSO | ✔️ (Step 2 complete) |
| RA-3 | Risk Assessment | ✅ | None | ISSO | 🔄 |
| RA-3(1) | Supply Chain Risk Assessment | ➕ | Added | ISSO | 🔄 |
| RA-5 | Vulnerability Monitoring and Scanning | ✅ | None | ISSO / SA | 🔄 |
| RA-5(2) | Update Vulnerabilities Scanned | ➕ | Added | SA | 🔄 |
| RA-5(5) | Privileged Access for Scanning | ➕ | Added | SA | 🔄 |
| RA-7 | Risk Response | ✅ | None | ISSO | 🔄 |
| RA-9 | Criticality Analysis | ✅ | None | ISSO | 🔄 |
| RA-10 | Threat Hunting | ➕ | Added (TD-011) | SOC | 🔄 |

---

## SA — System and Services Acquisition

| Control ID | Control Name | Selected | Tailoring | Owner | Step 4 Status |
|---|---|---|---|---|---|
| SA-1 | Policy and Procedures | ✅ | None | System Owner | 🔄 |
| SA-2 | Allocation of Resources | ✅ | None | System Owner | 🔄 |
| SA-3 | System Development Life Cycle | ✅ | None | System Owner / SA | 🔄 |
| SA-4 | Acquisition Process | ✅ | None | System Owner | 🔄 |
| SA-5 | System Documentation | ✅ | None | SA | 🔄 |
| SA-8 | Security and Privacy Engineering Principles | ✅ | None | ISSO / SA | 🔄 |
| SA-9 | External System Services | ✅ | None | ISSO | 🔄 |
| SA-9(2) | Identification of Functions | ➕ | Added | ISSO / SA | 🔄 |
| SA-10 | Developer Configuration Management | ✅ | None | SA | 🔄 |
| SA-11 | Developer Testing and Evaluation | ✅ | None | SA | 🔄 |
| SA-11(6) | Attack Surface Reviews | ⬜ | Scoped Out (TD-021) | N/A | N/A |
| SA-22 | Unsupported System Components | ➕ | Added (TD-017) | SA | 🔄 |

---

## SC — System and Communications Protection

| Control ID | Control Name | Selected | Tailoring | Owner | Step 4 Status |
|---|---|---|---|---|---|
| SC-1 | Policy and Procedures | ✅ | None | ISSO | 🔄 |
| SC-2 | Separation of System and User Functionality | ✅ | None | SA | 🔄 |
| SC-3 | Security Function Isolation | ✅ | None | SA | 🔄 |
| SC-4 | Information in Shared Resources | ✅ | None | SA | 🔄 |
| SC-5 | Denial-of-Service Protection | ✅ | None | SA / AWS | 🔄 |
| SC-7 | Boundary Protection | ✅ | None | SA | 🔄 |
| SC-7(3) | Access Points | ✅ | None | SA | 🔄 |
| SC-8 | Transmission Confidentiality and Integrity | ✅ | None | SA | 🔄 |
| SC-8(1) | Cryptographic Protection — TLS Enhanced | ➕ | Enhanced (TD-005) | SA | 🔄 |
| SC-10 | Network Disconnect | ✅ | None | SA | 🔄 |
| SC-12 | Cryptographic Key Establishment | ✅ | None | SA | 🔄 |
| SC-13 | Cryptographic Protection | ✅ | None | SA | 🔄 |
| SC-17 | Public Key Infrastructure Certificates | ✅ | None | SA | 🔄 |
| SC-18 | Mobile Code | ✅ | None | SA | 🔄 |
| SC-20 | Secure Name/Address Resolution | ➕ | Added (TD-018) | SA | 🔄 |
| SC-23 | Session Authenticity | ✅ | None | SA | 🔄 |
| SC-28 | Protection of Information at Rest | ✅ | None | DBA / SA | 🔄 |
| SC-28(1) | Cryptographic Protection — CMK | ➕ | Added (TD-006) | SA | 🔄 |
| SC-39 | Process Isolation | ✅ | None | SA | 🔄 |

---

## SI — System and Information Integrity

| Control ID | Control Name | Selected | Tailoring | Owner | Step 4 Status |
|---|---|---|---|---|---|
| SI-1 | Policy and Procedures | ✅ | None | ISSO | 🔄 |
| SI-2 | Flaw Remediation | ✅ | None | SA | 🔄 |
| SI-2(2) | Automated Patch Management | ➕ | Added | SA | 🔄 |
| SI-3 | Malicious Code Protection | ✅ | None | SA | 🔄 |
| SI-3(2) | Automatic Updates | ✅ | None | SA | 🔄 |
| SI-4 | System Monitoring | ✅ | None | SOC | 🔄 |
| SI-4(2) | Automated Monitoring Tools | ➕ | Added | SOC | 🔄 |
| SI-4(4) | Inbound/Outbound Traffic | ✅ | None | SA / SOC | 🔄 |
| SI-4(16) | Correlate Monitoring Information | ➕ | Added | SOC | 🔄 |
| SI-5 | Security Alerts, Advisories, and Directives | ✅ | None | ISSO | 🔄 |
| SI-6 | Security Function Verification | ✅ | None | ISSO | 🔄 |
| SI-7 | Software and Information Integrity | ✅ | None | SA | 🔄 |
| SI-7(1) | Automated Integrity Checks — FIM | ➕ | Added (TD-016) | SA | 🔄 |
| SI-10 | Information Input Validation | ✅ | None | SA | 🔄 |
| SI-12 | Information Management and Retention | ✅ | None | DBA / ISSO | 🔄 |
| SI-16 | Memory Protection | ✅ | None | SA | 🔄 |
| SI-18 | PII Quality Operations | ➕ | Added | Privacy Officer | 🔄 |
| SI-19 | De-identification | ➕ | Added (TD-014) | Privacy Officer | 🔄 |

---

## SR — Supply Chain Risk Management

| Control ID | Control Name | Selected | Tailoring | Owner | Step 4 Status |
|---|---|---|---|---|---|
| SR-1 | Policy and Procedures | ✅ | None | System Owner | 🔄 |
| SR-2 | Supply Chain Risk Management Plan | ✅ | None | System Owner / ISSO | 🔄 |
| SR-3 | Supply Chain Controls and Processes | ✅ | None | System Owner | 🔄 |
| SR-5 | Acquisition Strategies | ✅ | None | System Owner | 🔄 |
| SR-6 | Supplier Assessments and Reviews | ✅ | None | ISSO | 🔄 |
| SR-8 | Notification Agreements | ✅ | None | ISSO | 🔄 |
| SR-10 | Inspection of Systems | ✅ | None | SA | 🔄 |
| SR-11 | Component Authenticity | ✅ | None | SA | 🔄 |

---

## Worksheet Summary

| Family | Controls Selected | Tailored/Added | Inherited | Scoped Out |
|---|---|---|---|---|
| AC | 23 | 5 | 0 | 0 |
| AT | 6 | 1 | 0 | 0 |
| AU | 16 | 5 | 0 | 0 |
| CA | 9 | 2 | 0 | 0 |
| CM | 12 | 2 | 0 | 0 |
| CP | 13 | 3 | 0 | 0 |
| IA | 13 | 2 | 0 | 0 |
| IR | 10 | 3 | 0 | 0 |
| MA | 6 | 0 | 3 | 0 |
| MP | 8 | 0 | 0 | 0 |
| PE | 9 | 0 | 9 | 0 |
| PL | 4 | 0 | 0 | 0 |
| PM | 9 | 1 | 0 | 0 |
| PS | 9 | 0 | 0 | 0 |
| PT | 8 | 1 | 0 | 0 |
| RA | 10 | 4 | 0 | 0 |
| SA | 11 | 2 | 0 | 1 |
| SC | 19 | 4 | 0 | 0 |
| SI | 18 | 6 | 0 | 0 |
| SR | 8 | 0 | 0 | 0 |
| **TOTAL** | **221** | **41** | **12** | **1** |

---

*Document Reference: NEXUS-RMF-SEL-003 | Version 1.0 | Classification: Internal — Controlled*
*This worksheet feeds directly into Step 4 — Implement Controls.*
