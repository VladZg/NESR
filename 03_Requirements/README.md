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

Where the v0.4 requirements went (v0.4 → v0.5): TR-01 → TR-1, TR-02 and TR-14 → TR-2, TR-03 and TR-04 → TR-3, TR-05 → TR-4, TR-06 → TR-5, TR-07 → TR-6, TR-09 → TR-7, TR-12 and TR-15 → TR-8, TR-13 → TR-9, TR-17 → TR-10, TR-19 → TR-11, TR-21 → TR-12, TR-26 → TR-13, TR-27 → TR-14, TR-32 → TR-15, TR-34 → TR-16, TR-10, TR-11, TR-35 → TR-17, TR-36 → TR-18, TR-29 → TR-19, TR-08 → TR-20, TR-28 → TR-22. No longer in the set: TR-16, TR-18, TR-20 (v0.4), the hardware and maintenance requirements (TR-22 to TR-25, TR-31, TR-33), TR-30 (frequencies, the operators' responsibility) and TR-37 to TR-43. Older SR-01 to SR-11 IDs of v0.3 became SR-<stakeholder code>-NN in v0.4.

The md files were updated to match: REQ-003 md v0.5 (generated from the xlsx), REQ-002 v0.3 (stakeholders) and REQ-001 v0.3 (G1). If the md and the xlsx differ, the xlsx is the reference.
