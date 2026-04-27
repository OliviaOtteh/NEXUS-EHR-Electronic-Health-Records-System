# FIPS 199 Security Categorisation Worksheet
### NEXUS Electronic Health Records System | Step 2 — Categorise

| Field | Value |
|---|---|
| **Document Type** | FIPS 199 Security Categorisation Worksheet |
| **System Name** | NEXUS Electronic Health Records System |
| **Version** | 1.0 |
| **Classification** | Internal — Controlled |
| **Prepared By** | ISSO | Chioma Otteh
| **Reviewed By** | System Owner, ISSM |
| **Approved By** | Authorising Official |
| **Date** | 2026 |
| **References** | FIPS Publication 199; NIST SP 800-60 Vol 1 Rev 1; NIST SP 800-60 Vol 2 Rev 1 |

---

## 1. Purpose and Scope

This worksheet documents the security categorisation of the NEXUS Electronic Health Records System in accordance with:

- **FIPS Publication 199** — Standards for Security Categorisation of Federal Information and Information Systems
- **NIST SP 800-60 Volume 1, Rev 1** — Guide for Mapping Types of Information and Information Systems to Security Categories
- **NIST SP 800-60 Volume 2, Rev 1** — Appendices to Guide for Mapping Types of Information and Information Systems to Security Categories

The categorisation determines the potential impact to the organisation and to patients if the confidentiality, integrity, or availability of NEXUS information is compromised. This result drives the selection of the appropriate NIST SP 800-53 Rev 5 control baseline in Step 3.

---

## 2. FIPS 199 Impact Level Definitions

| Impact Level | Definition |
|---|---|
| **LOW** | A security breach could be expected to have a **limited** adverse effect on organisational operations, assets, or individuals |
| **MODERATE** | A security breach could be expected to have a **serious** adverse effect on organisational operations, assets, or individuals |
| **HIGH** | A security breach could be expected to have a **severe or catastrophic** adverse effect on organisational operations, assets, or individuals |

**Adverse effects include:** mission capability degradation, financial loss, harm to individuals, civil or criminal violations, and loss of public trust.

---

## 3. Information Types Processed by NEXUS

The following information types have been identified per NIST SP 800-60 Vol 2:

| Information Type | SP 800-60 Identifier | Default C | Default I | Default A | NEXUS Adjusted C | NEXUS Adjusted I | NEXUS Adjusted A |
|---|---|---|---|---|---|---|---|
| Health Care Delivery Services | C.2.8.1 | Moderate | Moderate | Moderate | **High** | **High** | **High** |
| Patient Health Records (PHI) | C.2.8.1 / D.14 | Moderate | Moderate | Low | **High** | **High** | **High** |
| Patient Identity / PII | D.14 | Moderate | Moderate | Low | **High** | **High** | **High** |
| Billing and Financial Records | D.12 | Moderate | Moderate | Low | **High** | **High** | Moderate |
| Medical Device / IoT Data | C.2.8.1 | Moderate | Moderate | Moderate | **High** | **High** | **High** |
| Audit and Accountability Records | D.20 | Moderate | High | Moderate | **High** | **High** | Moderate |
| System Configuration Data | D.21 | Moderate | High | Moderate | Moderate | **High** | Moderate |
| Laboratory Results | C.2.8.1 | Moderate | High | Moderate | **High** | **High** | **High** |
| Prescriptions and Medications | C.2.8.1 | Moderate | High | Moderate | **High** | **High** | **High** |
| Referrals and Appointments | C.2.8.1 | Low | Moderate | Moderate | Moderate | **High** | **High** |

> **Adjustment rationale:** Default values from SP 800-60 have been adjusted upward where the NEXUS operational context — specifically the direct patient care dependency and multi-site clinical environment — creates higher potential for patient harm than the default level contemplates.

---

## 4. Security Categorisation Analysis

### 4.1 Confidentiality

**Definition:** Preserving authorised restrictions on information access and disclosure, including means for protecting personal privacy and proprietary information.

**Impact Analysis:**

The unauthorised disclosure of information processed by NEXUS would have a **HIGH** adverse effect because:

1. **HIPAA violation and regulatory penalties:** Unauthorised disclosure of PHI constitutes a HIPAA breach. The Department of Health and Human Services (HHS) Office for Civil Rights (OCR) can impose civil monetary penalties of up to $1,919,173 per violation category per year. Criminal penalties under HIPAA can include imprisonment.

2. **Patient harm:** Exposure of a patient's diagnosis (e.g. HIV status, mental health conditions, substance use), treatment history, or medication records can cause direct harm — including discrimination in employment, insurance denial, family or community harm, and psychological distress.

3. **Identity theft and fraud:** PII fields (SSN, date of birth, address, insurance ID) combined with PHI create a highly valuable dataset for identity theft and insurance fraud.

4. **Loss of patient trust:** A breach affecting hundreds of thousands of patient records would severely and potentially irreparably damage public trust in Nexus Health System's ability to protect sensitive health information.

5. **Multi-site exposure:** The NEXUS breach surface spans multiple hospital sites, multiplying the potential number of affected individuals.

**Confidentiality Impact Level: HIGH**

---

### 4.2 Integrity

**Definition:** Guarding against improper information modification or destruction, and ensuring information non-repudiation and authenticity.

**Impact Analysis:**

The unauthorised modification or destruction of information processed by NEXUS would have a **HIGH** adverse effect because:

1. **Direct patient safety risk:** NEXUS is used at the point of clinical care. If a patient's allergy record, medication dosage, blood type, or lab result is altered — deliberately or through a technical failure — the result could be an incorrect clinical decision that harms or kills a patient. This is the highest possible individual-level consequence.

2. **Prescription and medication integrity:** Manipulation of prescription records or medication administration logs (MAR) could result in patients receiving incorrect medications, doses, or harmful drug combinations.

3. **Clinical decision support integrity:** NEXUS aggregates data to support clinical decisions (referrals, diagnoses, treatment plans). Corrupted input data produces corrupted clinical decisions.

4. **Legal and audit integrity:** Tampered or destroyed audit logs eliminate the ability to detect a breach, investigate incidents, or demonstrate HIPAA compliance. This alone constitutes a serious violation.

5. **Non-repudiation:** Clinical documentation must be attributable, time-stamped, and tamper-evident for medico-legal purposes. Loss of integrity undermines the legal validity of all records.

6. **Cascading effect across sites:** A single corrupted patient record, propagated across the replication cluster to secondary databases, affects all clinical sites simultaneously.

**Integrity Impact Level: HIGH**

---

### 4.3 Availability

**Definition:** Ensuring timely and reliable access to and use of information and the information system.

**Impact Analysis:**

The disruption of access to NEXUS would have a **HIGH** adverse effect because:

1. **Active clinical care dependency:** Clinical staff across all hospital sites rely on NEXUS to access patient records at the point of care. A system outage during an active clinical shift means clinicians cannot access current medication lists, allergy records, lab results, or care plans. This is a direct patient safety risk.

2. **No viable manual alternative at scale:** While downtime procedures exist (paper-based fallback), these are not sustainable at the volume of daily transactions NEXUS supports (~50,000 per day across all sites). Extended downtime degrades care quality and creates documentation backlogs.

3. **Emergency and critical care impact:** NEXUS is used in emergency department workflows, surgical scheduling, and ICU monitoring. Unavailability during time-critical care events (e.g. emergency surgery, resuscitation) could directly contribute to adverse patient outcomes.

4. **Multi-site simultaneous impact:** Because NEXUS is centralised, a single availability failure affects all clinical sites simultaneously — not just one ward or building.

5. **Regulatory requirement:** HIPAA requires covered entities to maintain contingency plans and ensure system availability for the ongoing provision of healthcare services.

6. **Recovery complexity:** The hybrid architecture (AWS + on-premises) means recovery requires coordinated restoration across multiple environments — increasing recovery time and complexity.

**Note on planned downtime:** Scheduled maintenance windows (with advance notice and downtime procedures activated) are acceptable and do not constitute a violation of this impact level. Only unplanned or extended availability loss is rated HIGH.

**Availability Impact Level: HIGH**

---

## 5. Security Categorisation Result

### Individual Objective Ratings

| Security Objective | Impact Level | Determined By |
|---|---|---|
| Confidentiality | **HIGH** | PHI/PII breach risk; HIPAA liability; patient harm potential |
| Integrity | **HIGH** | Patient safety — clinical decision integrity; audit trail requirements |
| Availability | **HIGH** | Active clinical care dependency; multi-site simultaneous impact |

### Overall System Categorisation

Using the high-water mark principle defined in FIPS 199 — the overall system categorisation is determined by the highest impact level across all three objectives:

```
SC NEXUS = {(Confidentiality, HIGH), (Integrity, HIGH), (Availability, HIGH)}

Overall System Impact Level: HIGH
```

> The **high-water mark** rule means that if any single objective is rated HIGH, the overall system is HIGH. For NEXUS, all three objectives independently reach HIGH — making this a clearly and unambiguously HIGH impact system.

---

## 6. Implications of HIGH Categorisation

| Implication | Detail |
|---|---|
| **Control Baseline** | NIST SP 800-53 Rev 5 — HIGH baseline (the most comprehensive control set) |
| **Assessment Frequency** | Annual security assessment at minimum; continuous monitoring required |
| **Authorisation** | Full ATO required; no use of Ongoing Authorisation (O-ATO) shortcuts |
| **Incident Response** | HIGH-severity incident response plan required; 24/7 SOC coverage |
| **Backup and Recovery** | RTO and RPO targets must reflect clinical care dependency |
| **Penetration Testing** | Annual penetration test strongly recommended in addition to vulnerability scanning |
| **Supply Chain Risk** | All third-party components and integrations must be assessed |

---

## 7. Approval and Sign-off

| Role | Name | Signature | Date |
|---|---|---|---|
| ISSO | [Name] | _________________________ | 2025 |
| System Owner | [Name] | _________________________ | 2025 |
| ISSM | [Name] | _________________________ | 2025 |
| Authorising Official | [Name] | _________________________ | 2025 |

---

## 8. References

| Reference | Description |
|---|---|
| FIPS Publication 199 | Standards for Security Categorisation of Federal Information and Information Systems |
| NIST SP 800-60 Vol 1 Rev 1 | Guide for Mapping Types of Information and Information Systems to Security Categories |
| NIST SP 800-60 Vol 2 Rev 1 | Appendices — Information Type Categorisation Tables |
| NIST SP 800-53 Rev 5 | Security and Privacy Controls for Information Systems and Organisations |
| HIPAA Security Rule | 45 CFR Part 164, Subpart C |
| HITECH Act | Health Information Technology for Economic and Clinical Health Act (2009) |

---

*Document Owner: ISSO | Approved by: AO | Classification: Internal — Controlled*
