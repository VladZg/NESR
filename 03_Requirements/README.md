# 03 Requirements (PDR deliverable 3)

**Deliverable:** Clear set of technical requirements. **Owner:** Vladislav Zagorodnyuk.

| CI | Item | Files | Owner | Version | Status |
| --- | --- | --- | --- | --- | --- |
| REQ-001 | Mission statement, needs, goals, objectives and MOEs | [md](T3_REQ-001_Mission-Statement-and-NGO.md) | Jash Joshi | v0.3 | Draft |
| REQ-002 | Stakeholder register | [md](T3_REQ-002_Stakeholder-Register.md) | Jash Joshi | v0.3 | Draft |
| REQ-003 | System (SR) and technical (TR) requirements with traceability | [xlsx](T3_REQ-003_System-and-Technical-Requirements.xlsx) · [md](T3_REQ-003_System-and-Technical-Requirements.md) | Vladislav Zagorodnyuk | v0.5 | Draft |

File names, versions and reviews: see [CONTRIBUTING.md](../CONTRIBUTING.md).

## REQ-003 v0.5: updated requirements

`T3_REQ-003_System-and-Technical-Requirements.xlsx` is the **updated version (v0.5)**, which replaces v0.4. Changes:

- **Scope:** the system is the integrating software. Terminals, antennas, satellites and ground equipment come from third parties, so hardware requirements are removed and only the interfaces to them are specified. Frequencies and licences are the satellite operators' responsibility and are not specified.
- **Simplified wording:** shorter formal requirements, no references to interface documents (ICD).
- **System reqs:** 14 → 13. Removed SR-SM-01 and SR-GM-01 (maintenance staff). New SR-RG-02 (maritime regulations, SOLAS, IMO cyber risk, master's final decision). SR-RG-01 now covers only the information required by the NSR rules and the Polar Code.
- **Technical reqs:** 43 → 22, renumbered TR-1 to TR-22 without gaps. TR-1 to TR-18 are the critical requirements kept from v0.4, TR-19 to TR-22 are new (Polar Code information, audit log, master's decision, cyber security). Terminal requirements are now interface requirements (TR-1 ship reports, TR-16 distress alert). New column **Prototype**: Yes (green) = can be verified and validated on the prototype.
- **Stakeholders:** SM and GM removed, RG limited to maritime and navigation rules.
- **Sheets:** Review log and Open items removed. Traceability and Verification summary rebuilt for the new IDs.

Old TR numbers of v0.4 → new: 01 → 1, 02 → 2, 04 → 3, 05 → 4, 06 → 5, 07 → 6, 09 → 7, 12 → 8, 13 → 9, 17 → 10, 19 → 11, 21 → 12, 26 → 13, 27 → 14, 32 → 15, 34 → 16, 35 → 17, 36 → 18. The other v0.4 requirements (TR-03, 08, 10, 11, 14 to 16, 18, 20, 22 to 25, 28 to 31, 33, 37 to 43) were removed. Other CIs that cite TR numbers (for example the V&V plan) still use the v0.4 numbering until they are updated.

The md files were updated to match: REQ-003 md v0.5 (generated from the xlsx), REQ-002 v0.3 (stakeholders) and REQ-001 v0.3 (G1). If the md and the xlsx differ, the xlsx is the reference.
