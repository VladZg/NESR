# System and technical requirements

| CI | Version | Status | Owner | Updated |
| --- | --- | --- | --- | --- |
| REQ-003 | v0.5 | Draft | Vladislav Zagorodnyuk | 2026-11-06 |

Written to the NASA SE Handbook rules: one "shall" per requirement, measurable values, a verification method (T test, A analysis, I inspection, D demonstration) and a trace to a system requirement. IDs: SR-<stakeholder code>-NN (codes in [REQ-002](T3_REQ-002_Stakeholder-Register.md), SR-ALL = all users), TR-N. TBR = value proposed, to be confirmed. The same content is in [the Excel file](T3_REQ-003_System-and-Technical-Requirements.xlsx) (with the traceability matrix and verification summary).

**Scope.** The system is the integrating software. Terminals, antennas, satellites and ground equipment are supplied by third parties, so hardware requirements are not included, only the interfaces to them. Only critical requirements are kept. Prototype = Yes means the requirement can be verified and validated on our prototype (software with emulators of terminals and links); No means it needs real satellites, operator links or other hardware.

## System requirements (SR): 13

| ID | Stakeholder | Requirement | MOE (target) | Validation | Status |
| --- | --- | --- | --- | --- | --- |
| SR-SC-01 | Ship crew | The system shall give the ship's bridge current ice information for the planned route, day or night and in any weather. | Ice information on the bridge ≤ 24 h old for ≥ 95% of voyage time | A | Agreed |
| SR-SC-02 | Ship crew | The system shall warn the ship of ice and storm hazards on its route early enough to change course safely. | Warning ≥ 6 h before the hazard zone in ≥ 90% of hazard events | A | Agreed |
| SR-SC-03 | Ship crew | The system shall keep two-way ship-shore communication available along the whole Northern Sea Route. | ≥ 95% of messages delivered within their class time (TR-17) in the service area: 35 km around the route and the ports of Murmansk and Arkhangelsk | A, T | Agreed |
| SR-OW-01 | Ship and cargo owners, Logistics Operators | The system shall let owners and logistics operators follow the position and ETA of their ships. | Position ≤ 30 min old (TR-10), ETA error ≤ 6 h at 72 h ahead in ≥ 90% of voyages | A, D | Agreed |
| SR-OW-02 | Ship and cargo owners | The system shall keep each owner's commercial data hidden from other owners and third parties. | 0 unauthorised data accesses | T | Agreed |
| SR-PA-01 | Port Authorities | The system shall give Port Authorities a live picture of all connected ships on the Northern Sea Route. | ≥ 99% of connected ships shown, position ≤ 30 min old | T | Agreed |
| SR-PA-02 | Port Authorities | The system shall deliver Port Authority directives to all affected ships and confirm receipt. | ≥ 99% of affected ships confirm receipt automatically within 5 min, crews of ≥ 90% confirm within 30 min | D | Agreed |
| SR-DI-01 | Dispatcher | The system shall let the dispatcher decide on route changes quickly, based on alarms that can be trusted. | Decision ≤ 10 min after an alarm in ≥ 90% of trials, false alarm ratio ≤ 30% (target 10%) | D, A | Agreed |
| SR-RS-01 | Rescue Services | The system shall pass distress information, with the ship's time-stamped last known position, to Rescue Services quickly. | Request received ≤ 2 min after the distress alert, with time-stamped position and uncertainty radius (TR-18) | T | Agreed |
| SR-SS-01 | Satellite Systems' Operators | The system shall request satellite data and relay services only within the agreed capacity and through documented interfaces. | 0 requests above the agreed monthly quota, interface documents signed with every operator before CDR | I, A | Agreed |
| SR-RG-01 | Regulators, Port Authorities | The system shall provide the information that the NSR rules and the Polar Code require for planning and conducting a voyage in ice. | 0 non-conformities at regulatory inspection and in an audit of 100 route recommendations | I | Agreed |
| SR-RG-02 | Regulators | The system shall comply with the maritime regulations that apply to it, including SOLAS and the IMO rules on maritime cyber risk, and shall leave the final navigation decision with the master. | 0 open non-conformities in the review by the classification society and in the inspection by the maritime administration before operation | I | Agreed |
| SR-ALL-01 | All users | The system shall tell users when information is missing or out of date, and keep working in a degraded mode when a link or data source is lost. | 100% of stale or missing data marked within 1 min, loss of the ALARM function shown to the dispatcher within 5 min | T | Agreed |

## Technical requirements (TR): 22

| ID | Type | Requirement | Rationale | Verif. | Prototype | Traces to | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- |
| TR-1 | Interface | The system shall receive ship reports from the on-board terminals (ship ID, position, course, speed, heading, persons on board) at intervals of 5 to 15 min, and shall reject and log any report that is incomplete or malformed. | First part of the 30 min position age budget (TR-10). The terminal is supplied by its manufacturer, the system defines only the interface. | T | Yes | SR-OW-01, SR-PA-01, SR-RS-01 | Verified with a terminal emulator, not with real terminals. |
| TR-2 | Functional | The system shall publish an ice chart within 60 min of receiving a SAR product, at 50 m resolution or finer (5 m in the NSR key straits). | The processing time is part of the 24 h ice information age (TR-9). 50 m matches the RCM ice mode. | T | Yes | SR-SC-01 | Resolution is checked by analysis of the SAR input. |
| TR-3 | Functional | Within 15 min of new ice, weather or ship data, the system shall raise an ALARM to the dispatcher and send a hazard warning to the affected ships when a ship's risk score exceeds 70 or its route enters a hazard zone within 24 h. | Starts the warning and route-change scenario. A warning is information, so it needs no approval. | T | Yes | SR-SC-02, SR-DI-01 |  |
| TR-4 | Functional | Within 5 min of an ALARM, the system shall offer the dispatcher at least 2 alternative routes, each with distance, fuel estimate and risk score. | Gives the dispatcher options to decide within 10 min (TR-15). | T | Yes | SR-SC-02, SR-DI-01 |  |
| TR-5 | Functional | The system shall send a route recommendation to a ship only after a dispatcher has approved it. | A named person is accountable. The master keeps the final decision. | T | Yes | SR-DI-01, SR-RG-02 |  |
| TR-6 | Functional | If the on-board terminal does not acknowledge a route recommendation or directive, the system shall resend it up to 3 times at 2 min intervals and then alert the dispatcher. | No silent loss of safety messages. | T | Yes | SR-SC-03, SR-PA-02 |  |
| TR-7 | Performance | Ship-shore messaging shall be available ≥ 99.0% of the time in any 30-day period at every point of the service area (35 km around the route and the ports of Murmansk and Arkhangelsk), and on ≥ 95% of voyages. Available means delivery within the message class time (TR-17). | 30-day window as in IMO A.915. The per-voyage figure is what the crew sees. | A | No | SR-SC-03, SR-PA-01 | Needs the real relay satellites. |
| TR-8 | Performance | On the 2024–2025 NSR season data, the ALARM function shall detect ≥ 90% of hazard events at least 6 h before the ship enters the hazard zone, with a false alarm ratio of no more than 30%. | Ships in ice need hours to re-route. 30% is a start value, the target is 10% after back-testing. | A | Yes | SR-SC-02, SR-DI-01 | Hazard event: a ship entering dangerous ice or storm conditions recorded in the ice charts and weather analyses. |
| TR-9 | Performance | Ice information shown on the bridge shall be no older than 24 h for ≥ 95% of voyage time. | SAR revisit time + processing (TR-2) + delivery (TR-17). | A | Yes | SR-SC-01 | Confirm with the Kondor-FKA revisit simulation. |
| TR-10 | Performance | Ship positions shown on dashboards shall be no older than 30 min. | Budget: 15 min report interval (TR-1) + 5 min delivery (TR-17) + 10 min processing and display. | T | Yes | SR-OW-01, SR-PA-01 |  |
| TR-11 | Performance | Within 2 min of a distress alert, the system shall send Rescue Services a request with ship ID, time-stamped last position, its uncertainty radius (TR-18) and persons on board. | A ship moves about 600 m in 2 min, so the position carries its time and uncertainty. | T | Yes | SR-RS-01 |  |
| TR-12 | Interface | The system shall receive SAR products and weather data from the satellite operators' ground segments over terrestrial links of at least 100 Mbit/s. | SAR volumes are too large for the satellite relay. | T | No | SR-SC-01, SR-SC-02, SR-SS-01 | Needs the operators' real links. |
| TR-13 | Safety | The system shall mark ice information older than 24 h as AGED and older than 48 h as DEGRADED, and shall show the last valid data with its age when a data source or link fails. | Stale data shown as current is a navigation hazard. | T | Yes | SR-SC-01, SR-ALL-01, SR-DI-01 |  |
| TR-14 | Security | The system shall show each user only the data allowed by their role: owners and logistics operators see their own ships, Port Authorities see all connected ships. | Commercial data stays with its owner. | T | Yes | SR-OW-01, SR-OW-02, SR-PA-01 |  |
| TR-15 | Human factors | A dispatcher shall be able to review an ALARM and approve or reject a route change within 10 min, with all inputs on one screen, in ≥ 90% of trials. | Verifies the MOE of SR-DI-01. | D | Yes | SR-DI-01 |  |
| TR-16 | Interface | The system shall receive a distress alert from an on-board terminal (ship ID, time-stamped position), handle it before all other messages and show it to the dispatcher within 30 s of receipt. | Input of TR-11. The SOS button belongs to the terminal, not to this system. | T | Yes | SR-RS-01 | On the prototype with a terminal emulator. |
| TR-17 | Performance | The system shall deliver messages within the time of their class, counted from release: distress 2 min (≥ 99%), hazard warning 10 min, position report 5 min, route recommendation or directive 15 min, routine message 30 min, each for ≥ 95%. | One table for all delivery times. The position report class keeps the TR-10 budget. | T | Yes | SR-SC-02, SR-SC-03, SR-PA-02, SR-RS-01, SR-DI-01 | On the prototype with a link emulator. |
| TR-18 | Performance | A ship that has not reported for 30 min shall be shown at its last position with an uncertainty radius that grows with ice drift and ship speed, and the dispatcher shall be alerted after 60 min. | Tracks a silent ship in drift terms instead of a 10 m accuracy. | T | Yes | SR-OW-01, SR-PA-01, SR-RS-01 | Stationary-ship flag still to be defined. |
| TR-19 | Regulatory | For every planned route, the system shall show the ice and weather information along the route that the Polar Code requires for voyage planning, with the age of each item. | The Polar Code requires ice and weather information to be taken into account in voyage planning in polar waters. The exact list is agreed with the classification society. | I | Yes | SR-SC-01, SR-RG-01 | Checklist inspection of the prototype screens and reports. |
| TR-20 | Regulatory | The system shall record every recommendation, directive, approval and alert with its time and the user who made it, keep the records for at least 5 years, and export them for an audit. | Lets a regulator check how each route decision was made (SR-RG-01). | T | Yes | SR-RG-01, SR-RG-02 | Retention period to be confirmed with the regulator. |
| TR-21 | Regulatory | Every route recommendation shown to a ship shall state that the master keeps the final decision, and the system shall record whether the master accepts or rejects it. | SOLAS V/34-1 protects the master's professional judgement, so the system gives advice and does not command. | T | Yes | SR-DI-01, SR-RG-02 | On the prototype with a ship terminal emulator. |
| TR-22 | Security | The system shall authenticate every user and every connected terminal, encrypt all messages in transit and keep a log of security events, so that a ship operator can include the system in its cyber risk management. | IMO resolution MSC.428(98) requires cyber risks to be addressed in the ship operator's safety management system. | I | Yes | SR-OW-02, SR-RG-02 | Inspection of the design against a cyber security checklist, the penetration test is in TR-14. |

## Traceability

Rows are technical requirements, columns are system requirements. X = the TR helps to meet the SR.

| TR \ SR | SR-SC-01 | SR-SC-02 | SR-SC-03 | SR-OW-01 | SR-OW-02 | SR-PA-01 | SR-PA-02 | SR-DI-01 | SR-RS-01 | SR-SS-01 | SR-RG-01 | SR-RG-02 | SR-ALL-01 | Count |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| TR-1 |  |  |  | X |  | X |  |  | X |  |  |  |  | 3 |
| TR-2 | X |  |  |  |  |  |  |  |  |  |  |  |  | 1 |
| TR-3 |  | X |  |  |  |  |  | X |  |  |  |  |  | 2 |
| TR-4 |  | X |  |  |  |  |  | X |  |  |  |  |  | 2 |
| TR-5 |  |  |  |  |  |  |  | X |  |  |  | X |  | 2 |
| TR-6 |  |  | X |  |  |  | X |  |  |  |  |  |  | 2 |
| TR-7 |  |  | X |  |  | X |  |  |  |  |  |  |  | 2 |
| TR-8 |  | X |  |  |  |  |  | X |  |  |  |  |  | 2 |
| TR-9 | X |  |  |  |  |  |  |  |  |  |  |  |  | 1 |
| TR-10 |  |  |  | X |  | X |  |  |  |  |  |  |  | 2 |
| TR-11 |  |  |  |  |  |  |  |  | X |  |  |  |  | 1 |
| TR-12 | X | X |  |  |  |  |  |  |  | X |  |  |  | 3 |
| TR-13 | X |  |  |  |  |  |  | X |  |  |  |  | X | 3 |
| TR-14 |  |  |  | X | X | X |  |  |  |  |  |  |  | 3 |
| TR-15 |  |  |  |  |  |  |  | X |  |  |  |  |  | 1 |
| TR-16 |  |  |  |  |  |  |  |  | X |  |  |  |  | 1 |
| TR-17 |  | X | X |  |  |  | X | X | X |  |  |  |  | 5 |
| TR-18 |  |  |  | X |  | X |  |  | X |  |  |  |  | 3 |
| TR-19 | X |  |  |  |  |  |  |  |  |  | X |  |  | 2 |
| TR-20 |  |  |  |  |  |  |  |  |  |  | X | X |  | 2 |
| TR-21 |  |  |  |  |  |  |  | X |  |  |  | X |  | 2 |
| TR-22 |  |  |  |  | X |  |  |  |  |  |  | X |  | 2 |
| Covered by | 5 | 5 | 3 | 4 | 2 | 5 | 2 | 8 | 5 | 1 | 2 | 4 | 1 |  |

Uncovered SR: 0. Untraced TR: 0.

## Verification summary

| Type | Test (T) | Analysis (A) | Inspection (I) | Demonstration (D) | Total |
| --- | --- | --- | --- | --- | --- |
| Functional | 5 | 0 | 0 | 0 | 5 |
| Performance | 4 | 3 | 0 | 0 | 7 |
| Interface | 3 | 0 | 0 | 0 | 3 |
| Safety | 1 | 0 | 0 | 0 | 1 |
| Security | 1 | 0 | 1 | 0 | 2 |
| Regulatory | 2 | 0 | 1 | 0 | 3 |
| Human factors | 0 | 0 | 0 | 1 | 1 |
| Total | 16 | 3 | 2 | 1 | 22 |

Where two methods apply, the main one is counted and the other is named in the Notes column.

## Revision history

| Version | Date | Author | Change |
| --- | --- | --- | --- |
| v0.3 | 2026-10-29 | Vladislav Zagorodnyuk | Reduced to 11 SR and 32 TR with concrete values |
| v0.4 | 2026-11-03 | Vladislav Zagorodnyuk | Review remarks applied (M1–M12, C1–C27): SR IDs by stakeholder code, 14 SR (new SR-SS-01, SR-GM-01, SR-ALL-01), 43 TR (new TR-33…TR-43, message classes in TR-35), TBR marked, 21 open items |
| v0.5 | 2026-11-06 | Vladislav Zagorodnyuk | Simplified wording, kept only the critical requirements for the system software and its interfaces: 13 SR and 22 TR renumbered TR-1 to TR-22. Hardware requirements and maintenance staff (SR-SM-01, SR-GM-01, TR-22, TR-25 of v0.4) removed, terminal requirements rewritten as interface requirements (TR-1, TR-16), maritime regulations added (SR-RG-02, TR-19 to TR-22), column Prototype added. Sheets Review log and Open items removed |
