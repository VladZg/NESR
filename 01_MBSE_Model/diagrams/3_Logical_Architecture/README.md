# Logical Architecture (in the model, exports pending)

The layer is built in Capella, in the project zip `../../capella/T3_MOD-001_Capella-Model.zip` v0.2. What that version contains:

- [x] System Analysis functions transitioned to the Logical Architecture: 71 leaf logical functions, 107 functional exchanges, realization links to the system functions.
- [x] LCBD: the Logical System decomposed into 7 logical components (Data Acquisition, Data Fusion, Risk Assessment, Reporting and Dashboards, Message Delivery, Distress Handling, Security and Audit).
- [x] LFBD: logical function breakdown.
- [x] LDFB: data flow between the logical functions.
- [x] LAB: the 7 components with their allocated functions, 14 logical actors and 48 component exchanges.
- [ ] Highlight the functional chains S1, S2 and S6 on the LAB (no functional chains at the Logical Architecture level yet).
- [ ] Export the diagrams into this folder.

Export as `T3_MOD-010_LAB-Logical-Architecture.png`, `T3_MOD-011_LCBD-Logical-Components.png`, `T3_MOD-012_LFBD-Logical-Functions.png`, `T3_MOD-013_LDFB-Logical-Data-Flow.svg`. The LAB and the LDFB are large, so export them as SVG.

| CI | Item | Files | Owner | Version | Status |
| --- | --- | --- | --- | --- | --- |
| MOD-010 | Logical architecture (LAB, LCBD, LFBD, LDFB) in Capella | in [the project zip](../../capella/T3_MOD-001_Capella-Model.zip), png/svg to add | Victoria Kulikova | v0.2 | In model, exports pending |
