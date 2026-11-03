# Stakeholder register

| CI | Version | Status | Owner | Updated |
| --- | --- | --- | --- | --- |
| REQ-002 | v0.2 | Draft | Jash Joshi | 2026-11-03 |

| Code | Stakeholder | Role in the system | Main concern |
| --- | --- | --- | --- |
| SC | Ship crew (captain and bridge team) | Send ship data, receive route recommendations and warnings; the master keeps the final decision (SOLAS V/34-1) | Safe passage through ice, day or night, in any weather |
| OW | Ship and cargo owners | Receive voyage status and route decisions | Schedule, fuel cost, cargo safety, data confidentiality |
| LO | Logistics Operators | Plan and follow voyages on the mission dashboard | Predictable ETAs, early warning of delays |
| PA | Port Authorities | Issue navigation and safety directives, watch traffic | Safety and rule compliance on the whole route |
| DI | Dispatcher | Approves route recommendations and sends them to ships; the master decides | Clear, trustworthy information |
| RS | Rescue Services | Coordinate and carry out search and rescue; receive rescue requests; report resource availability | Fast, accurate distress data |
| SS | Satellite Systems' Operators | Provide SAR, meteo, relay and navigation services | Requests within capacity, clear interfaces |
| RG | Regulators (frequency authority, classification society) | Control and verify that the system meets government and international requirements (certification, frequency licensing, inspection) | Compliance with radio and marine equipment rules |
| SM | Maintenance staff (on-board terminals) | Keep the on-board terminals working | Fast fault finding and repair |
| GM | Maintenance staff (ground equipment) | Keep ground antennas, terminals and the ground platform working | Fast fault finding and repair |

The Data Analysis Centers are treated as part of the system. Icebreaker operators and the NSR administration are candidate stakeholders; their scope is an open item (review C1), and they have no system requirement yet. The Stakeholders sheet of the [REQ-003 Excel file](T3_REQ-003_System-and-Technical-Requirements.xlsx) is the master list. Stakeholder requirements (SR) are in [REQ-003](T3_REQ-003_System-and-Technical-Requirements.md).

## Revision history

| Version | Date | Author | Change |
| --- | --- | --- | --- |
| v0.1 | 2026-10-29 | Jash Joshi | First version in the repository |
| v0.2 | 2026-11-03 | Vladislav Zagorodnyuk | Aligned with REQ-003 v0.4: SO → SC (ship crew, master keeps the final decision), MS split into SM (on-board) and GM (ground), roles of DI, RS and RG updated (review M1–M3, C1–C3) |
