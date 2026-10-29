# System verification and validation plan

| CI | Version | Status | Owner | Updated |
| --- | --- | --- | --- | --- |
| VV-002 | v0.1 | Draft | Mikhail Timofeenko | 2026-10-29 |

> Starter text. Complete events, dates and facilities before PDR.

## 1. Purpose

Show that NESR SCMS meets its technical requirements (verification) and that it satisfies the stakeholders' needs in its operational environment (validation).

## 2. Verification approach

- Every technical requirement has one method: Test, Analysis, Inspection or Demonstration. The matrix is [VCRM](T3_VV-001_VCRM.xlsx).
- Levels: on-board terminal, ground platform, system end to end.

| Event | Method | Requirements | Facility |
| --- | --- | --- | --- |
| Coverage and availability simulation | A | TR-09, TR-13 | Python, orbit propagation |
| Latency budget | A | TR-10, TR-11, TR-14 | Spreadsheet model |
| Terminal environmental tests | T | TR-22, TR-31 | Climatic chamber (IEC 60945) |
| End-to-end message test via relay | T | TR-07, TR-10, TR-18, TR-19 | Ground platform + relay + terminal |
| Alarm model back-test | A | TR-12, TR-15, TR-16 | Recorded 2024–2025 voyages |
| Operator trials | D | TR-25, TR-32 | Dispatch console mock-up |
| Document inspection | I | TR-02, TR-08, TR-28 to TR-31 | Design documents |

## 3. Validation approach

- Replay of recorded 2024–2025 NSR voyages with historical ice and weather: check the MOEs of SR-01, SR-02, SR-04.
- Operator trials with dispatchers and ship officers: check SR-03, SR-07.
- Stakeholder review of ConOps scenarios S1 to S6.

## 4. Responsibilities and schedule (TODO)

Verification lead: Mikhail Timofeenko. Requirement owners support the events for their requirements.

## Revision history

| Version | Date | Author | Change |
| --- | --- | --- | --- |
| v0.1 | 2026-10-29 | Mikhail Timofeenko | First version in the repository |
