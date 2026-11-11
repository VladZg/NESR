# Capella project

The zipped Capella project is kept here as `T3_MOD-001_Capella-Model.zip` (File → Export → Archive File in Capella, or zip the project folder). To open it: unzip, then in Capella use File → Import → Existing Projects into Workspace. The project folder inside the zip is `NESR-SCMS-layout8`; delete earlier `NESR-SCMS-layout*` projects from the workspace before importing, otherwise Capella keeps showing the previous version.

| CI | Item | Files | Owner | Version | Status |
| --- | --- | --- | --- | --- | --- |
| MOD-001 | Arcadia Capella model: Operational Analysis, System Analysis and Logical Architecture | [zip](T3_MOD-001_Capella-Model.zip) | Vladislav Zagorodnyuk | v0.2 | Draft |

Model content in v0.2: 20 diagrams; OA 23 entities, 28 activities, 11 operational capabilities; SA 22 actors, 71 leaf functions, 107 functional exchanges, 10 capabilities, 4 functional chains, 7 scenarios; LA 7 components, 14 actors, 71 functions, 48 component exchanges.

## v0.2 (2026-11-11): what was added

### 1. Logical Architecture, the new layer of the model

The Logical System is decomposed into 7 logical components; every system function is realized by a logical function and allocated to one of them.

| Component | Functions | Responsibility |
| --- | --- | --- |
| Data Acquisition | 4 | ship reports, SAR and weather data from the operators, protocol synchronisation, monitoring of sources and links |
| Data Fusion | 7 | normalisation, merging, mapping, data age marks, integrated current picture |
| Risk Assessment | 7 | route prediction, risk score, silent ships, ALARM, alternative routes |
| Reporting and Dashboards | 7 | operational, logistics and regulatory reports, ice chart, filtering by user role |
| Message Delivery | 4 | master-decision notice, delivery by priority class, resend, update check |
| Distress Handling | 2 | priority of the distress alert, rescue request |
| Security and Audit | 5 | authentication, encryption, decision log, audit export |

Four new diagrams: `[LAB]` logical components, actors and component exchanges; `[LCBD]` decomposition of the Logical System; `[LFBD]` logical function breakdown; `[LDFB]` data flow between logical functions. Traceability to the System Analysis is complete: FunctionRealization for every function, ComponentRealization for the system and the actors, PortRealization and FunctionalExchangeRealization for the ports and exchanges.

### 2. Corrections in the System Analysis

- **SAR and meteo data no longer go through the relay satellites.** Kondor-F and Arctic-M downlink to the ground segment of the satellite operators, and the operators pass the products to the system, as the interface requirement demands. Previously the imagery was routed through the low-rate Gonets relay.
- **GLONASS is modelled correctly.** The constellation is MEO, not GSO, and only broadcasts navigation signals; the position is computed by the on-board terminal ("Compute own position from GNSS signals") and goes into the ship report. The constellation no longer "receives a signal and estimates the location" of the ship.
- **Duplicated functions removed.** 14 functions that had been transferred one-to-one from the Operational Analysis and later superseded by detailed ones were deleted (for example "Process the raw data sets", "Formulate an order and send it", "Capture the downward signal"); their realization links were moved to the surviving functions, so all 28 operational activities stay realized. Leaf functions 85 → 71, functional exchanges 125 → 107.

### 3. Diagrams merged and reformatted

- The two architecture diagrams are merged into one: `[SAB] Architecture View of Navigation support (basic) scenario` now holds all 71 functions in 15 actor lanes, including the on-board terminal, the constellations and the gateways. The separate `[SAB] Satellite data path` diagram is gone.
- Edge labels in `[SAB]`, `[SDFB]`, `[LAB]` and `[LDFB]` no longer overlap the boxes or each other, and each label sits next to its own arrow.
- On `[LAB]` the component exchanges are drawn as rectilinear routes between the ports.

## Rules

- One zip per commit; do not commit the Capella workspace `.metadata` folder.
- After each model change, bump the MOD-001 version in the configuration register and re-export the changed diagrams.

## To fix in the next model version

- Project name typo: "montoring" → "monitoring".
- Requirement IDs quoted in the descriptions of capabilities and scenarios follow REQ-003 v0.3; after the renumbering to v0.5 (13 SR, 22 TR) they have to be re-checked.
- The model holds no requirements (the Requirements viewpoint is not used), so the trace "requirement → function" lives only in REQ-003.
- The Logical Architecture has no capability realizations, scenarios or functional chains yet.
- Diagram exports for the Logical Architecture are not in `../diagrams/3_Logical_Architecture/` yet; `[SAB]` is about 7000 × 3300 px and should be exported as SVG.
- Naming is inconsistent across the repository and the model: "SMCS" and "SCMS", and the system is called just "System" in the System Analysis.
