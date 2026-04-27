# Data Inventory
### NEXUS Electronic Health Records System | Categorise

| Field | Value |
|---|---|
| **Document Type** | Data Inventory |
| **System Name** | NEXUS Electronic Health Records System |
| **Version** | 1.0 |
| **Classification** | Internal — Controlled |
| **Last Updated** | 2026 |



##  Purpose

This inventory documents all categories of data processed, stored, or transmitted by NEXUS. It supports the FIPS 199 categorisation, informs control selection, and satisfies HIPAA requirements for knowing where PHI resides across the system.

---

##  Complete Data Inventory

| Data Element | Classification | Contains PHI | Contains PII | Storage Location | Encrypted at Rest | Encrypted in Transit | Retention Period | Regulatory Requirement |
|---|---|---|---|---|---|---|---|---|
| Patient demographics | Highly Sensitive | Yes | Yes | On-prem Primary DB | Yes (AES-256) | Yes (TLS 1.2+) | 10 years | HIPAA |
| Medical diagnoses and ICD codes | Highly Sensitive | Yes | No | On-prem Primary DB | Yes (AES-256) | Yes (TLS 1.2+) | 10 years | HIPAA |
| Prescription records | Highly Sensitive | Yes | No | On-prem Primary DB | Yes (AES-256) | Yes (TLS 1.2+) | 10 years | HIPAA / DEA |
| Laboratory results | Highly Sensitive | Yes | No | On-prem Primary DB | Yes (AES-256) | Yes (TLS 1.2+) | 10 years | HIPAA / CLIA |
| Clinical notes and documentation | Highly Sensitive | Yes | No | On-prem Primary DB | Yes (AES-256) | Yes (TLS 1.2+) | 10 years | HIPAA |
| Medication Administration Records (MAR) | Highly Sensitive | Yes | No | On-prem Primary DB | Yes (AES-256) | Yes (TLS 1.2+) | 10 years | HIPAA |
| Referral records | Highly Sensitive | Yes | No | On-prem Primary DB | Yes (AES-256) | Yes (TLS 1.2+) | 10 years | HIPAA |
| Appointment scheduling data | Sensitive | Yes | Yes | On-prem Primary DB | Yes (AES-256) | Yes (TLS 1.2+) | 7 years | HIPAA |
| Patient insurance information | Highly Sensitive | Yes | Yes | On-prem Primary DB | Yes (AES-256) | Yes (TLS 1.2+) | 10 years | HIPAA |
| Billing and payment records | Sensitive | Partial | Yes | On-prem Primary DB | Yes (AES-256) | Yes (TLS 1.2+) | 7 years | HIPAA / PCI DSS |
| Patient consent forms | Highly Sensitive | Yes | Yes | On-prem Primary DB | Yes (AES-256) | Yes (TLS 1.2+) | 10 years | HIPAA |
| Vital signs (from IoT devices) | Highly Sensitive | Yes | No | On-prem Primary DB | Yes (AES-256) | Yes (TLS 1.2+) | 10 years | HIPAA |
| Audit logs (access events) | Internal — Controlled | No (metadata) | Partial | On-prem Audit Server | Yes | Yes | 6 years minimum | HIPAA |
| SIEM telemetry | Internal — Controlled | No | No | On-prem SIEM | Yes | Yes | 1 year rolling | Internal policy |
| Application configuration | Internal — Controlled | No | No | AWS Cloud (encrypted) | Yes (KMS) | Yes | Lifecycle of system | Internal policy |
| Backup archives (full system) | Highly Sensitive | Yes | Yes | AWS Backup Vault + S3 | Yes (AES-256, KMS) | Yes | 10 years | HIPAA |
| System event logs | Internal | No | No | AWS CloudWatch / on-prem | Yes | Yes | 1 year | Internal policy |
| User account data (staff) | Sensitive | No | Yes | Active Directory (on-prem) | Yes | Yes | Duration of employment + 3 years | Internal policy |
| Patient portal credentials | Sensitive | No | Yes | AWS App Tier (hashed) | Yes | Yes | Account lifetime | HIPAA |

---

## PHI Data Elements Inventory

The following specific PHI data elements are processed by NEXUS as defined under HIPAA 45 CFR §164.514(b)(2):

| HIPAA PHI Identifier | Present in NEXUS | Field Examples |
|---|---|---|
| Names | Yes | Patient full name, next-of-kin name |
| Geographic data (smaller than state) | Yes | Street address, city, postcode |
| Dates (except year) | Yes | DOB, admission date, discharge date, appointment date |
| Phone numbers | Yes | Home phone, mobile, emergency contact |
| Fax numbers | Yes | GP fax, referral fax |
| Email addresses | Yes | Patient email, clinical staff email |
| Social Security numbers | Yes (partial / last 4) | Insurance verification |
| Medical record numbers | Yes | NEXUS patient ID |
| Health plan beneficiary numbers | Yes | Insurance member ID |
| Account numbers | Yes | Billing account ID |
| Certificate / licence numbers | No | N/A |
| Vehicle identifiers | No | N/A |
| Device identifiers / serial numbers | Yes | Medical IoT device IDs linked to patient |
| Web URLs | No | N/A |
| IP addresses | Partial | Patient portal login IPs (audit logs) |
| Biometric identifiers | No | N/A |
| Full-face photographs | No | N/A |
| Any other unique identifying number | Yes | NEXUS encounter ID |

> **All 18 HIPAA Safe Harbour identifiers that are present in NEXUS must be treated as PHI and subject to all applicable HIPAA Security Rule safeguards.**


##  Data Flow Summary


External Users / Patients
        |
        | HTTPS (TLS 1.2+)
        v
[AWS Cloud Zone]
  - WAF → ALB → Web/App Servers
        |
        | IPSec VPN Tunnel
        v
[On-Premises Hospital Zone]
  - Primary PostgreSQL DB  ←→  Secondary Failover DB (replication)
  - Audit Logging Server
  - SIEM Monitoring Server
        ^
        |
[Hospital Endpoints]
  - Admin Workstations
  - Clinician Laptops
  - Nurses' Tablets
  - Medical IoT Devices  (vital signs → Primary DB)
        |
        | Scheduled Backups
        v
[AWS Private Subnet]
  - AWS Backup Vault
  - Amazon S3


##  Third-Party Data Sharing

| Third Party | Data Shared | Legal Basis | Agreement in Place |
|---|---|---|---|
| External laboratories | Lab orders, results (PHI) | Treatment — HIPAA §164.506 | Business Associate Agreement (BAA) |
| Insurance companies | Billing data, diagnosis codes (PHI) | Healthcare operations — HIPAA §164.506 | BAA |
| Referring physicians / external providers | Referral data, clinical summaries (PHI) | Treatment — HIPAA §164.506 | BAA |
| Amazon Web Services (AWS) | Encrypted backup data only | Business Associate | BAA signed with AWS |
| IT support vendors | Audit logs (no PHI) | Business operations | Confidentiality agreement |

> **All third parties who access, process, or store PHI on behalf of Nexus Health System must have a signed Business Associate Agreement (BAA) in place prior to any data sharing.**

---

##  Data at Rest — Encryption Summary

| Location | Encryption Standard | Key Management |
|---|---|---|
| On-premises Primary DB | AES-256 (PostgreSQL TDE / OS-level encryption) | On-premises HSM / KMS |
| On-premises Secondary DB | AES-256 | On-premises HSM / KMS |
| AWS Backup Vault | AES-256 | AWS KMS (customer-managed key) |
| Amazon S3 | AES-256 (SSE-KMS) | AWS KMS (customer-managed key) |
| Clinical endpoint hard drives | AES-256 (BitLocker / FileVault) | Active Directory / MDM |

---

##  Data in Transit — Encryption Summary

| Connection | Protocol | Minimum TLS Version |
|---|---|---|
| External users → AWS WAF/ALB | HTTPS | TLS 1.2 |
| AWS App Servers → On-prem DB (via VPN) | IPSec + TLS | TLS 1.2 |
| PostgreSQL replication | PostgreSQL SSL | TLS 1.2 |
| Hospital endpoints → NEXUS | HTTPS (internal) | TLS 1.2 |
| IoT devices → Hospital LAN | Proprietary encrypted protocol | Device-level encryption |
| SIEM telemetry | Syslog/TLS | TLS 1.2 |
| Backup to AWS | HTTPS (AWS SDK) | TLS 1.2 |

---

*Document Owner: Chioma Otteh | Reviewed by: Jack Taylor | Classification: Internal — Controlled*
