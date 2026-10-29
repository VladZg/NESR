# Project management plan

| CI | Version | Status | Owner | Updated |
| --- | --- | --- | --- | --- |
| MGT-003 | v0.1 | Draft | Jash Joshi | 2026-10-29 |

> Starter text. Complete dates and resources before PDR.

## 1. Scope and objectives

Bring NESR SCMS to the Preliminary Design Review with the 9 PDR deliverables of the course, following the NASA SE Handbook processes.

## 2. Organisation and roles

| Member | Role | Responsible for |
| --- | --- | --- |
| Vladislav Zagorodnyuk | MBSE and Requirements Engineer | Capella model (OA, SA) and diagrams; system and technical requirements; IDEF0 A4; simulations |
| Victoria Kulikova | Functional & Interface Engineer and Architecture | IDEF0 A-0 and A0; logical architecture; N2; ICDs; interface management plan |
| Jash Joshi | Stakeholders and Documentation Engineer, configuration manager (proposed) | Mission and NGO; stakeholders; ConOps; project management plan and WBS; CM/DM plan |
| Mikhail Timofeenko | Safety, Risk, Reliability, Verification and Validation Engineer | Risk analysis; FMEA; reliability; V&V plans; maritime compliance check |

## 3. Work breakdown structure

The WBS is in [T3_MGT-006_WBS.xlsx](T3_MGT-006_WBS.xlsx). Top level: 1.1 project management, 1.2 systems engineering, 1.3 analysis and simulation, 1.4 ground platform, 1.5 on-board terminal, 1.6 external interfaces, 1.7 safety, risk and reliability, 1.8 verification and validation, 1.9 regulatory compliance, 1.10 reviews.

## 4. Schedule and milestones (TODO: dates)

| Milestone | Date | Exit criteria |
| --- | --- | --- |
| SRR | YYYY-MM-DD | System requirements and ConOps agreed; tag `srr-baseline` |
| PDR | YYYY-MM-DD | 9 deliverables at v1.0; tag `pdr-v1.0` |

## 5. Deliverables

| # | PDR deliverable | Owner | Folder |
| --- | --- | --- | --- |
| 1 | MBSE model in Arcadia-Capella: stakeholders, operational analysis, system analysis, logical architecture | Vladislav Zagorodnyuk | `01_MBSE_Model` |
| 2 | ConOps of the proposed system | Jash Joshi | `02_ConOps` |
| 3 | Clear set of technical requirements | Vladislav Zagorodnyuk | `03_Requirements` |
| 4 | Project management plan including WBS | Jash Joshi | `04_Project_Management` |
| 5 | Risk analysis | Mikhail Timofeenko | `05_Risk_Analysis` |
| 6 | System verification and validation plans | Mikhail Timofeenko | `06_Verification_Validation` |
| 7 | Interface management plan | Victoria Kulikova | `07_Interface_Management` |
| 8 | Configuration management and data management baseline plan | Jash Joshi | `08_Configuration_Data_Management` |
| 9 | Compliance check with maritime regulations | Mikhail Timofeenko | `09_Maritime_Compliance` |

## 6. Task management and communication

- Tasks: GitHub Issues with labels `pdr:<n>`, `owner:<name>`, milestone `PDR`; board Todo → In progress → In review → Done.
- Weekly team meeting: review the board, blockers and risks; minutes as an issue comment.
- Rules for files, versions and reviews: [CONTRIBUTING.md](../CONTRIBUTING.md).

## 7. Related plans

Risk: [05_Risk_Analysis](../05_Risk_Analysis/) · V&V: [06_Verification_Validation](../06_Verification_Validation/) · Interfaces: [07_Interface_Management](../07_Interface_Management/) · CM/DM: [08_Configuration_Data_Management](../08_Configuration_Data_Management/)

## Revision history

| Version | Date | Author | Change |
| --- | --- | --- | --- |
| v0.1 | 2026-10-29 | Jash Joshi | First version in the repository |
