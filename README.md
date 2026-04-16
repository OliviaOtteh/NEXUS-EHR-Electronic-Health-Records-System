
## NEXUS EHR (Electronic Health Records System)
A simulated NIST RMF portfolio project for Nexus, a fictional Integrated Health Records System (IHR). Covers system categorization, control selection, SSP, risk assessment, POA&M, ATO, and continuous monitoring. Built for learning purposes only.


## **OBJECTIVE**

This project simulates an end-to-end NIST Risk Management Framework (RMF) authorization process for Nexus, a fictional Integrated Health Records System (IHR). The primary focus is to demonstrate practical understanding of system categorization, security control selection, implementation, assessment, authorization, and continuous monitoring of a healthcare system that processes Protected Health Information (PHI) and Personally Identifiable Information (PII).

This hands-on project is designed to build and demonstrate real-world GRC and security documentation skills in a healthcare compliance context.


## **SKILLS LEARNED**

- Practical application of the NIST RMF lifecycle from categorization to continuous monitoring
- Understanding of FIPS 199 system categorization for healthcare systems
- Ability to select and tailor security controls from NIST SP 800-53 Rev 5
- Development of System Security Plan (SSP) documentation
- Risk assessment and risk register development for a healthcare environment
- Security Assessment Plan (SAP) and Security Assessment Report (SAR) writing
- POA&M tracking and remediation planning
- Understanding of HIPAA Security Rule requirements and how they map to NIST controls
- Authorization to Operate (ATO) package development
- Continuous monitoring strategy and scheduling

---

## **TOOLS USED**

| Tool | Purpose |
|------|---------|
| **NIST SP 800-53 Rev 5** | Security control selection and tailoring |
| **FIPS 199** | System categorization |
| **NIST SP 800-60 Vol. 1 & 2** | Information type identification |
| **NIST SP 800-30** | Risk assessment methodology |
| **draw.io** | Network and data flow diagrams |
| **Microsoft Word / Markdown** | Security documentation |
| **GitHub** | Project hosting and version control |
| **NIST RMF Cybersecurity Framework** | Overall project structure |

---

## **1. SYSTEM DESCRIPTION**

Nexus is a hybrid Integrated Health Records System designed to support comprehensive healthcare operations across multi-site clinical environments. The system enables healthcare providers to manage patient records, lab results, referrals, appointments, billing, and clinical documentation in a secure and centralized environment.

Nexus processes, stores, and transmits sensitive health information including Protected Health Information (PHI) and Personally Identifiable Information (PII), making security and compliance a critical priority.

---

## **2. SYSTEM PURPOSE AND MISSION**

The primary mission of Nexus is to:

- Support patient registration and demographic management
- Enable multi-provider appointment scheduling and referral tracking
- Maintain and manage integrated health records across care facilities
- Facilitate billing, insurance coordination, and claims processing
- Support clinical documentation and lab result management
- Generate operational, clinical, and compliance reports
- Maintain comprehensive audit logs for security and regulatory purposes

---

## **3. SYSTEM USERS**

| User Role | Description |
|-----------|-------------|
| **Patients** | Access personal health records, lab results, and appointments via patient portal |
| **Physicians** | View and update patient records, order labs, and document treatment plans |
| **Nurses** | Access patient information, administer medications, and update care notes |
| **Lab Technicians** | Enter and manage diagnostic results within the system |
| **Administrative Staff** | Manage scheduling, referrals, and patient registration |
| **Billing Staff** | Process billing, insurance claims, and financial records |
| **System Administrators** | Manage system configuration, user accounts, and integrations |
| **Security Team** | Monitor system security, respond to incidents, and conduct audits |

---

## **4. SYSTEM ENVIRONMENT**

Nexus operates in a **hybrid environment** consisting of:

| Component | Environment |
|-----------|-------------|
| Web Application Server | Cloud-hosted (Azure) |
| Database Server | On-Premise |
| Authentication Service | Cloud-hosted (Azure Active Directory) |
| Lab Integration Gateway | On-Premise |
| Audit Logging Server | On-Premise |
| Backup Server | Cloud-hosted (Azure) |
| Admin Workstations | On-Premise |
| Clinician Endpoints | On-Premise |
| Patient Portal | Cloud-hosted (Azure) |

---

## **5. DATA HANDLED BY NEXUS**

| Data Type | Description | Sensitivity |
|-----------|-------------|-------------|
| **PHI** | Protected Health Information including diagnoses and treatment records | High |
| **PII** | Personally Identifiable Information including SSN and contact data | High |
| **Lab Results** | Diagnostic and pathology data | High |
| **Billing Data** | Insurance records, payment information, and claims | High |
| **Referral Data** | Inter-provider referral and specialist coordination records | High |
| **Clinical Notes** | Provider-authored treatment documentation | High |
| **Appointment Data** | Scheduling and visit records | Moderate |
| **Audit Logs** | System activity and access records | Moderate |
| **Authentication Data** | Login credentials and session tokens | High |

---

## **6. SYSTEM COMPONENTS**

| Component | Function |
|-----------|----------|
| **Web Application Server** | Hosts the Nexus user interface and application logic |
| **Database Server** | Stores patient records, lab data, billing, and system data |
| **Authentication Service** | Manages user identity verification and role-based access control |
| **Lab Integration Gateway** | Facilitates secure data exchange with external lab systems |
| **Audit Logging Server** | Captures and retains all system activity logs |
| **Backup Server** | Maintains encrypted, redundant backups of critical system data |
| **Patient Portal** | Provides patients with secure access to their records and appointments |
| **Admin Workstations** | Used by IT and security staff to manage and monitor the system |
| **Clinician Endpoints** | Devices used by physicians, nurses, and lab staff to access Nexus |

---

## **7. COMPLIANCE AND REGULATORY SCOPE**

| Framework / Regulation | Relevance |
|------------------------|-----------|
| **HIPAA** | Nexus processes PHI and must comply with the HIPAA Security Rule |
| **NIST SP 800-53 Rev 5** | Primary control framework for RMF authorization |
| **FIPS 199** | Used to categorize Nexus based on data sensitivity and impact levels |
| **NIST SP 800-60** | Used to identify information types processed by Nexus |
| **GDPR** | Applicable where Nexus handles data belonging to EU-based individuals |
| **HL7 / FHIR** | Healthcare interoperability standards governing data exchange |

---

## **STEPS**

### **STEP 1 — SYSTEM OVERVIEW AND BOUNDARY DEFINITION**
Definition of what Nexus is, who uses it, what data it handles, and where the system boundary begins and ends.

*Ref 1: Architecture Diagram*
[![Architecture Diagram](./diagrams/Architecture_Diagram.png)](./diagrams/Architecture_Diagram.png)

---

### **STEP 2 — SYSTEM CATEGORIZATION**
Categorize Nexus using FIPS 199 and NIST SP 800-60 based on the sensitivity of data handled.

*Ref 2: FIPS 199 Categorization Table*
![Categorization Table](./diagrams/FIPS199_Table.png)

---

### **STEP 3 — CONTROL SELECTION**
Select and tailor security controls from NIST SP 800-53 Rev 5 based on Nexus's High impact categorization.

*Ref 3: Control Baseline Summary*
![Control Baseline](./diagrams/Control_Baseline.png)

---

### **STEP 4 — SYSTEM SECURITY PLAN**
Document how each selected control is implemented within Nexus.

*Ref 4: SSP Cover Page*
![SSP](./diagrams/SSP_Cover.png)

---

### **STEP 5 — RISK ASSESSMENT**
Identify threats and vulnerabilities specific to a multi-site healthcare environment and rate them by likelihood and impact.

*Ref 5: Risk Register*
![Risk Register](./diagrams/Risk_Register.png)

---

### **STEP 6 — SECURITY ASSESSMENT**
Develop a SAP and SAR to test whether Nexus's controls are working as intended.

*Ref 6: SAR Findings Summary*
![SAR](./diagrams/SAR_Findings.png)

---

### **STEP 7 — POA&M**
Track all findings and weaknesses with remediation plans and target completion dates.

*Ref 7: POA&M Tracker*
![POAM](./diagrams/POAM_Tracker.png)

---

### **STEP 8 — AUTHORIZATION**
Compile the full ATO package and make an authorization recommendation based on Nexus's risk posture.

*Ref 8: Authorization Recommendation*
![ATO](./diagrams/ATO_Recommendation.png)

---

### **STEP 9 — CONTINUOUS MONITORING**
Document how Nexus will be monitored on an ongoing basis after authorization.

*Ref 9: Continuous Monitoring Schedule*
![ConMon](./diagrams/ConMon_Schedule.png)

---

## **KEY ASSUMPTIONS**

- Nexus is a fictional system created for portfolio and learning purposes
- All data, scenarios, and documentation are simulated
- Security controls are selected based on a High impact baseline
- The hybrid environment assumes Microsoft Azure as the cloud service provider
- No real PHI or PII is used anywhere in this project

---

## **DOCUMENT CONTROL**

| Field | Detail |
|-------|--------|
| **Author** | [Your Name] |
| **Created** | [Date] |
| **Last Updated** | [Date] |
| **Next Review** | [Date] |
| **Version** | 1.0 |

---

> ⚠️ **DISCLAIMER**
> Nexus is a fictional system created solely for educational and portfolio demonstration purposes. All data, scenarios, and documentation within this project are simulated and do not represent any real organization, system, or individual.
