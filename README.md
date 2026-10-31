# NESR SCMS

**Satellite monitoring and communication system for the Northern Sea Route**

Team 3 project, Systems Engineering course (Skoltech, 2026/2027). Topic: *Satellite communication and observation along the sea route in all weather conditions with monitoring of ice conditions.*

## Product card

| | |
| --- | --- |
| **What it is** | An information service that gives ships on the Northern Sea Route (NSR) all-weather ice charts, hazard warnings and ship-to-shore communication, and gives shore operators a live picture of traffic. |
| **Mission statement** | Provide vessels and maritime operators along the Northern Sea Route with continuous communication and timely, all-weather sea-ice information, enabling safe, efficient and year-round Arctic navigation. |
| **Problem** | NSR cargo reached a record 37.8 Mt in 2024, but ice limits the season; geostationary satellites sit low on the horizon above about 75°N, and optical imaging fails in cloud and polar night. |
| **Users** | Ship operators, ship and cargo owners, logistics operators, Port Authorities, dispatchers, Rescue Services. |
| **System of interest** | Ground integration platform (data ingest, ice charts, risk analytics, dashboards, dispatch, logging) and the on-board ship terminal. |
| **External systems** | Kondor-FKA (SAR ice imaging), Arktika-M (meteorology), Gonets/Sfera (satellite relay), GLONASS (navigation). |
| **Service area** | NSR water area and the nine designated Russian Artic Ports 64°N to 82°N, Murmansk and Arkhangelsk to Bering Strait.|
| **Lifecycle phase** | Pre-Phase A / Phase A (NASA), working towards PDR. |

**Key performance targets** (from [technical requirements](03_Requirements/T3_REQ-003_System-and-Technical-Requirements.md)):

| Measure | Target |
| --- | --- |
| Age of ice information on the bridge | ≤ 24 h for ≥ 95% of voyage time (TBR) |
| Ship-to-shore messaging availability, 66–82°N | ≥ 99.0% over any 30 days |
| Route update delivery | ≤ 5 min for ≥ 99% of messages |
| Hazard warning lead time | ≥ 6 h in ≥ 90% of hazard events |
| Rescue request to Rescue Services | ≤ 2 min, position error ≤ 10 m |
| ALARM detection / false alarm ratio | ≥ 95% / ≤ 10% |

**Operational scenarios** (see [ConOps](02_ConOps/T3_CON-001_ConOps.md)): S1 nominal monitoring, S2 ice or storm ALARM and route change, S3 reporting to authorities and logistics, S4 regulatory update, S5 SAR and meteo acquisition, S6 emergency and rescue.

## Authors

| Name | Role | Responsible for |
| --- | --- | --- |
| Vladislav Zagorodnyuk | MBSE and Requirements Engineer | Capella model (OA, SA) and diagrams; system and technical requirements; IDEF0 A4; simulations |
| Victoria Kulikova | Functional & Interface Engineer and Architecture | IDEF0 A-0 and A0; logical architecture; N2; ICDs; interface management plan |
| Jash Joshi | Stakeholders and Documentation Engineer, configuration manager (proposed) | Mission and NGO; stakeholders; ConOps; project management plan and WBS; CM/DM plan |
| Mikhail Timofeenko | Safety, Risk, Reliability, Verification and Validation Engineer | Risk analysis; FMEA; reliability; V&V plans; maritime compliance check |

Configuration manager: Jash Joshi (proposed). Backup for model and requirements files: Vladislav Zagorodnyuk.

## PDR deliverables

| # | Deliverable | Folder | Owner | Status |
| --- | --- | --- | --- | --- |
| 1 | MBSE model in Arcadia-Capella: stakeholders, operational analysis, system analysis, logical architecture | [01_MBSE_Model](01_MBSE_Model/) | Vladislav Zagorodnyuk | Draft |
| 2 | ConOps of the proposed system | [02_ConOps](02_ConOps/) | Jash Joshi | Draft |
| 3 | Clear set of technical requirements | [03_Requirements](03_Requirements/) | Vladislav Zagorodnyuk | Draft |
| 4 | Project management plan including WBS | [04_Project_Management](04_Project_Management/) | Jash Joshi | Draft |
| 5 | Risk analysis | [05_Risk_Analysis](05_Risk_Analysis/) | Mikhail Timofeenko | Draft |
| 6 | System verification and validation plans | [06_Verification_Validation](06_Verification_Validation/) | Mikhail Timofeenko | Draft |
| 7 | Interface management plan | [07_Interface_Management](07_Interface_Management/) | Victoria Kulikova | Draft |
| 8 | Configuration management and data management baseline plan | [08_Configuration_Data_Management](08_Configuration_Data_Management/) | Jash Joshi | Draft |
| 9 | Compliance check with maritime regulations | [09_Maritime_Compliance](09_Maritime_Compliance/) | Mikhail Timofeenko | Draft |

## Repository map

```
01_MBSE_Model/                 PDR 1: Capella project, diagrams (OA, SA, LA), IDEF0
02_ConOps/                     PDR 2: concept of operations, scenario map
03_Requirements/               PDR 3: mission and NGO, stakeholders, SR/TR requirements
04_Project_Management/         PDR 4: project management plan, WBS
05_Risk_Analysis/              PDR 5: risk register, FMEA, reliability
06_Verification_Validation/    PDR 6: V&V plan, VCRM
07_Interface_Management/       PDR 7: interface management plan, N2, ICDs
08_Configuration_Data_Management/  PDR 8: CM/DM plan, configuration register
09_Maritime_Compliance/        PDR 9: compliance matrix
analysis/                      simulations and trade studies
problem-sets/                  course homework, one folder per problem set
reviews/                       review packages (PDR presentation)
references/                    handbooks, standards, reference missions
.github/                       issue and pull request templates
scripts/                       one-time GitHub setup (labels, milestone, issues, project board)
```

## How we work

- Tasks live in **GitHub Issues** and on the project board; every change links to an issue.
- File names, versions, branches and reviews follow [CONTRIBUTING.md](CONTRIBUTING.md).
- Every file in the repository is listed in the [configuration register](08_Configuration_Data_Management/T3_MGT-001_Configuration-Register.xlsx).
- Baselines are git tags and GitHub Releases, recorded in [CHANGELOG.md](CHANGELOG.md).
