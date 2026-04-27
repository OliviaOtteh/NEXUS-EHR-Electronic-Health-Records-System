# Step 2 — Categorise
### NEXUS Electronic Health Records System | NIST SP 800-37 Rev 2

> **Purpose:** Determine the security impact level of NEXUS using FIPS 199 and NIST SP 800-60. The categorisation result drives the control baseline selected in Step 3.

---

## Overview

Security categorisation is the process of determining how harmful a security breach of NEXUS would be — to the organisation, to patients, and to the wider healthcare system. The result is expressed as an impact level (LOW, MODERATE, or HIGH) across three security objectives: Confidentiality, Integrity, and Availability.

For NEXUS, this categorisation is straightforward but critically important. The system processes PHI and PII, supports active clinical care, and operates across a hybrid environment. Any breach or failure has the potential to directly harm patients — making this one of the highest-impact civilian system categorisations possible.

---

## Categorisation Result

```
SC NEXUS = {(Confidentiality, HIGH), (Integrity, HIGH), (Availability, HIGH)}

Overall Impact Level: HIGH
```

---

## Step 2 Deliverables

| Document | Description | Status |
|---|---|---|
| [FIPS 199 Worksheet](./fips199-worksheet.md) | Security categorisation across all three objectives | ✅ Complete |
| [Data Inventory](./data-inventory.md) | Full inventory of information types processed by NEXUS | ✅ Complete |
| [SSP Draft](./ssp-draft.md) | System Security Plan — initial draft incorporating categorisation | ✅ Complete |

---

## Step 2 Completion Checklist

- [x] All information types processed by NEXUS identified per NIST SP 800-60 Vol 2
- [x] Confidentiality impact level determined and justified
- [x] Integrity impact level determined and justified
- [x] Availability impact level determined and justified
- [x] Overall system impact level determined (HIGH)
- [x] Categorisation reviewed and approved by ISSO and System Owner
- [x] Data inventory complete
- [x] SSP draft initiated with categorisation section complete

---

## Next Step

➡️ [Step 3 — Select Controls](../03-select/)
