# System and technical requirements

| CI | Version | Status | Owner | Updated |
| --- | --- | --- | --- | --- |
| REQ-003 | v0.4 | Draft | Vladislav Zagorodnyuk | 2026-11-03 |

Written to the NASA SE Handbook rules: one "shall" per requirement, measurable values, a verification method (T test, A analysis, I inspection, D demonstration) and a trace to a system requirement. IDs: SR-<stakeholder code>-NN (codes in [REQ-002](T3_REQ-002_Stakeholder-Register.md); SR-ALL = all users), TR-NN. TBR = value proposed, to be confirmed. The same content is in [the Excel file](T3_REQ-003_System-and-Technical-Requirements.xlsx) (with traceability matrix, verification summary and review log) and in the [shared doc](https://claude.ai/artifact/XdnaVzd9gVZ4JKDw3HB5Zk).

## System requirements (SR): 14

| ID | Stakeholder | Requirement | MOE (target) | Validation | Notes |
| --- | --- | --- | --- | --- | --- |
| SR-SC-01 | Ship crew | The system shall give the ship's bridge current ice information for the planned route at any time of day or night and in any weather. | Age of ice information on the bridge ≤ 24 h (TBR) for ≥ 95% of voyage time | A | Was SR-01. Open: Kondor-FKA revisit simulation (C10). |
| SR-SC-02 | Ship crew | The system shall warn the ship of ice and storm hazards on its planned route early enough to change course safely. | Warning ≥ 6 h before reaching the hazard zone in ≥ 90% of hazard events | A | Was SR-02. |
| SR-SC-03 | Ship crew | The system shall keep two-way communication between ship and shore available along the whole Northern Sea Route. | Each message delivered within the time of its message class (TR-35) for ≥ 95% (TBR) of messages in the service area (route ±20 nm and the ports of Murmansk and Arkhangelsk) | A, T | Was SR-03. Review M5, M6, C14, C23: classes instead of one 5 min figure; percentage to be set after the coverage simulation. |
| SR-OW-01 | Ship and cargo owners, Logistics Operators | The system shall let owners and logistics operators follow the position and ETA of their ships. | Position age ≤ 30 min (delay budget in TR-17); ETA error ≤ 6 h at 72 h ahead in ≥ 90% of voyages | A, D | Was SR-04. Review M4, M7. |
| SR-OW-02 | Ship and cargo owners | The system shall keep each owner's commercial data hidden from other owners and third parties. | 0 unauthorised data accesses in the acceptance penetration test | T | Was SR-10. |
| SR-PA-01 | Port Authorities | The system shall give Port Authorities a live picture of all connected ships on the Northern Sea Route. | ≥ 99% of connected ships shown; position age ≤ 30 min | T | Was SR-05. Review C8, C23: 100% → 99%, method D → T. |
| SR-PA-02 | Port Authorities | The system shall deliver Port Authority directives to all affected ships and confirm receipt. | ≥ 99% of affected ships: terminal receipt confirmed automatically ≤ 5 min after delivery; crew confirmation of ≥ 90% within 30 min (TBR) | D | Was SR-06. Review M7, C7: receipt by the terminal and confirmation by the crew are separate. |
| SR-DI-01 | Dispatcher | The system shall let the dispatcher decide on route changes quickly, based on alarms that can be trusted. | Decision ≤ 10 min after the alarm in ≥ 90% of operator trials; false alarm ratio ≤ 30% (TBR; target 10% after back-testing) | D, A | Was SR-07. The dispatcher approves recommendations; the master decides (C2). False alarm value aligned with TR-15 (M8). |
| SR-RS-01 | Rescue Services | The system shall pass distress information to Rescue Services quickly, with the ship's last known position and its time stamp. It supplements GMDSS and does not replace it. | Request received ≤ 2 min after the distress alert; position time-stamped and given with an uncertainty radius (TR-36) | T | Was SR-08. Review M9, C6: the 10 m figure is removed. |
| SR-SS-01 | Satellite Systems' Operators | The system shall request satellite data and relay services from the satellite operators only within the agreed capacity and through documented interfaces. | 0 requests above the agreed quota per month; interface documents signed with every operator before CDR | I, A | New (review C9, P-SR-A). |
| SR-RG-01 | Regulators, Port Authorities | The system shall support compliance with the NSR navigation rules and the Polar Code by providing the information they require, and shall itself meet the radio and marine equipment regulations that apply to it. | 0 non-conformities at regulatory inspection and in an audit of 100 route recommendations | I | Was SR-09. Review C5: the rules apply to ships and masters; the system supports compliance. |
| SR-SM-01 | Maintenance staff (on-board terminals) | The system shall let maintenance staff find and replace a failed on-board unit quickly. | Fault isolated to one replaceable unit in ≥ 90% of failures; repair ≤ 1 h | D | Was SR-11. Review C3: ground equipment is now SR-GM-01. |
| SR-GM-01 | Maintenance staff (ground equipment) | The system shall let maintenance staff find and repair a failed ground equipment unit quickly. | Fault isolated to one replaceable unit in ≥ 90% of failures; restored ≤ 4 h (TBR) | D | New (review C3, C9, P-SR-B). |
| SR-ALL-01 | All users | The system shall tell its users when information is missing or out of date, and keep working in a degraded mode when a link or data source is lost. | 100% of stale or missing data marked on all displays within 1 min (TBR); loss of the ALARM function shown to the dispatcher within 5 min (TBR) | T | New (review C18, P-SR-C). |

## Technical requirements (TR): 43

| ID | Type | Requirement | Rationale | Verif. | Traces to | TBR |
| --- | --- | --- | --- | --- | --- | --- |
| TR-01 | Functional | The on-board terminal shall send a ship data report (ship ID, GNSS position, course and speed over ground, heading, persons on board, sensor data per ICD-01) every 15 min by default, configurable from 5 to 15 min. | 15 min report interval + 5 min delivery + up to 10 min processing and display = 30 min position age limit (TR-17). | T | SR-OW-01, SR-PA-01, SR-RS-01 |  |
| TR-02 | Functional | The system shall produce ice charts from SAR data giving ice concentration, stage of development and form of ice, at a spatial resolution of 50 m or finer (5 m or finer in the NSR key straits). | WMO ice chart parameters; 50 m matches the RCM ice mode, Kondor-FKA images at up to 1 m. | A | SR-SC-01 |  |
| TR-03 | Functional | The system shall recompute the risk score (0 to 100) of each ship and of each 10 km route segment ahead of it within 15 min of new ice, weather or ship data. | Keeps risk current with the 15 min reporting cycle. | T | SR-SC-02, SR-DI-01 |  |
| TR-04 | Functional | The system shall raise an ALARM when a ship's risk score exceeds 70 (configurable) or its planned route enters a hazard zone within the next 24 h. | Starts the warning and route-change scenario (S2). | T | SR-SC-02, SR-DI-01 | TBR |
| TR-05 | Functional | Within 5 min of each ALARM, the system shall generate at least 2 alternative routes, each with ETA, distance, fuel estimate and risk score. | The dispatcher needs ranked options to decide within 10 min. | T | SR-SC-02, SR-DI-01 | TBR |
| TR-06 | Functional | The system shall send a route recommendation to a ship only after a dispatcher has approved it. | A named person stays accountable for every route decision; the master keeps the final decision (SOLAS V/34-1). | T | SR-DI-01, SR-RG-01 |  |
| TR-07 | Functional | The system shall resend each route update or directive that the on-board terminal has not acknowledged up to 3 times at 2 min intervals, then alert the dispatcher. | No silent delivery failure of safety messages. | T | SR-SC-03, SR-PA-02 |  |
| TR-08 | Functional | The system shall keep a tamper-evident log of all datasets, alarms, decisions and sent messages, time-stamped to UTC within ±1 s, for at least 5 years. | Accountability and incident investigation. | I | SR-RG-01 | TBR |
| TR-09 | Performance | Ship-to-shore and shore-to-ship messaging shall be available (a message can be sent and delivered within the time of its message class, TR-35) for ≥ 99.0% (TBR) of the time over any 30-day period at every point of the service area (route ±20 nm and the ports of Murmansk and Arkhangelsk), and on the whole of ≥ 95% (TBR) of voyages. | The 30 days is a statistics window, as in IMO A.915; the per-voyage figure is what the crew sees. Measured per route point by coverage and outage simulation. | A | SR-SC-03, SR-PA-01 | TBR |
| TR-10 | Performance | Route updates and directives shall reach the addressed ship within 15 min (TBR), and routine text messages within 30 min (TBR), for ≥ 95% (TBR) of messages (message classes in TR-35). | Keeps the dispatcher-to-ship loop short; one table of classes replaces the separate values. | T | SR-SC-03, SR-DI-01 | TBR |
| TR-11 | Performance | Hazard warnings shall reach affected ships within 10 min of the ALARM (message class "hazard warning", TR-35) for ≥ 95% of warnings, without waiting for dispatcher approval. | Warnings are information, not commands; RCM gives 10–30 min for maritime surveillance. | T | SR-SC-02 |  |
| TR-12 | Performance | Hazard warnings shall be issued at least 6 h before the ship's forecast entry into the hazard zone in ≥ 90% of hazard events. | Ships in ice need hours to re-route or wait for an icebreaker. Verifies the MOE of SR-SC-02 at system level. | A | SR-SC-02 |  |
| TR-13 | Performance | The age of ice information shown on the bridge shall not exceed 24 h (TBR) for ≥ 95% of voyage time. | Key TPM: SAR revisit time plus processing and delivery time. Verifies the MOE of SR-SC-01 at system level. | A | SR-SC-01 | TBR |
| TR-14 | Performance | The system shall publish an ice chart within 60 min of receiving a SAR product. | Ice drifts tens of kilometres per day; processing adds to information age. | T | SR-SC-01 |  |
| TR-15 | Performance | On the validation dataset (2024–2025 NSR navigation seasons), the ALARM function shall detect ≥ 90% (TBR) of hazard events with a false alarm ratio of no more than 30% (TBR). A hazard event is a ship entering a zone of dangerous ice or storm conditions as recorded in the ice charts and weather analyses. | Start values; to be tightened after back-testing (target false alarm ratio 10%, SR-DI-01). Detection value matches SR-SC-02. | A | SR-SC-02, SR-DI-01 | TBR |
| TR-16 | Performance | The ETA forecast error shall not exceed 6 h at 72 h ahead in ≥ 90% of voyages. | Back-tested on recorded 2024–2025 NSR voyages. Verifies the MOE of SR-OW-01 at system level. | A | SR-OW-01 | TBR |
| TR-17 | Performance | Ship positions shown on dashboards shall be no older than 30 min. | Verifies the MOE of SR-OW-01 and SR-PA-01. Delay budget: 15 min report interval (TR-01) + 5 min delivery + up to 10 min processing and display = 30 min. | T | SR-OW-01, SR-PA-01 |  |
| TR-18 | Performance | Port Authority directives shall be received by the on-board terminal of ≥ 99% of affected ships, with automatic receipt confirmed within 5 min after delivery, and confirmed by the crew of ≥ 90% (TBR) of affected ships within 30 min (TBR) of receipt. | Verifies the MOE of SR-PA-02 at system level. Terminal receipt is automatic; crew confirmation is a human response time. | T | SR-PA-02 | TBR |
| TR-19 | Performance | The system shall send a rescue request with ship ID, time-stamped last known position and its uncertainty radius (TR-36), time and persons on board to Rescue Services within 2 min of receiving a distress alert (message class "distress", TR-35). | Implements the emergency scenario (S6). The 10 m accuracy is removed: a ship moves about 600 m in 2 min and accuracy is a property of the ship GNSS receiver. | T | SR-RS-01 | TBR |
| TR-20 | Performance | The system shall track at least 500 ships at once and serve at least 50 concurrent operator sessions while meeting all latency requirements. | Margin for NSR traffic growth (37.8 Mt of cargo in 2024). | T | SR-OW-01, SR-PA-01, SR-PA-02 | TBR |
| TR-21 | Interface | The system shall receive SAR products (GeoTIFF, ICD-02) and meteorological data (WMO GRIB2, ICD-03) from the satellite operators' ground segments over secure terrestrial links of at least 100 Mbit/s (TBR). | SAR volumes are too large for the low-rate satellite relay. | T | SR-SC-01, SR-SC-02, SR-SS-01 | TBR |
| TR-22 | Environmental | The on-board antenna unit shall operate at air temperatures from −50 °C (TBR; Polar Service Temperature of the NSR winter) to +55 °C, in wind up to 30 m/s (TBR) and with up to 50 mm of snow or ice on the radome (TBR) or with a de-icing function, and shall survive wind of 60 m/s (TBR), ship motion and vibration per IEC 60945 (GOST R MEK 60945). | IEC 60945 exposed-equipment conditions, extended to Arctic winter; the Polar Code sets the Polar Service Temperature at least 10 °C below the lowest mean daily low. | T | SR-SC-03 | TBR |
| TR-23 | Reliability and maintainability | The ground platform shall have an operational availability of at least 99.9% per year (TBR) with a backup site, excluding no more than 8 h of planned maintenance. 'Operational' means that data ingest, risk assessment, alarm and dispatch all work. | Supports the 99.0% end-to-end messaging availability in a 30-day window (TR-09). 99.5% allows about 44 h of unplanned downtime per year. | A | SR-SC-03, SR-PA-01 | TBR |
| TR-24 | Reliability and maintainability | The on-board terminal shall have a mean time between failures of at least 20 000 h. | About one failure in 2.3 years of continuous use. | A | SR-SM-01, SR-SC-03 | TBR |
| TR-25 | Reliability and maintainability | Built-in test shall isolate at least 90% of on-board terminal failures to one line-replaceable unit that ship staff can replace within 1 h using on-board spares. | Ships may be weeks away from a port with service. | D | SR-SM-01 |  |
| TR-26 | Safety | The system shall mark ice information older than 24 h (TBR) as AGED and older than 48 h as DEGRADED on all displays. | Stale ice data shown as current is a navigation hazard; the 24 h limit equals TR-13. | T | SR-SC-01, SR-ALL-01 |  |
| TR-27 | Security | The system shall give each user access only to the data allowed by their role; owners shall see only their own ships. | Implements SR-OW-02. | T | SR-OW-02 |  |
| TR-28 | Security | All data links shall be encrypted with a GOST R 34.12-2015 cipher using keys of at least 256 bit. | Ship positions and cargo data are commercially sensitive. | I | SR-OW-02 |  |
| TR-29 | Regulatory | Route recommendations shall comply with the current NSR navigation rules and include the Polar Code Chapter 11 ice information (current extent and type of ice near the route). | Mandatory for ships on the NSR; Polar Code 11.3.3. | I | SR-RG-01, SR-SC-01 |  |
| TR-30 | Regulatory | All system radio links shall operate only in the frequency bands and power limits licensed by the national frequency authority. | ITU Radio Regulations and national law. | I | SR-RG-01 |  |
| TR-31 | Regulatory | The on-board terminal shall hold a type approval certificate, based on GOST R MEK 60945-2007 (IEC 60945) tests, from the Russian Maritime Register of Shipping or a recognised organisation of the flag state. | Required for installation on classed ships. | I | SR-RG-01 |  |
| TR-32 | Human factors | A dispatcher shall be able to review an ALARM and approve or reject a route change within 10 min, with all inputs on one screen, in ≥ 90% of trials. | Verifies the MOE of SR-DI-01 at system level. | D | SR-DI-01 |  |
| TR-33 | Environmental | Outdoor ground antennas and terminals shall operate at air temperatures from −50 °C to +40 °C (TBR), in wind up to 40 m/s (TBR) and with up to 50 mm of snow or ice on the radome (TBR), or shall be installed in a heated enclosure. | Same Arctic conditions as the ship antenna, for equipment at port or gateway sites. | T | SR-SC-03, SR-GM-01 | TBR |
| TR-34 | Functional | The on-board terminal shall send a distress alert with ship ID, time-stamped position and time within 30 s (TBR) of the SOS button being pressed. The service supplements, and does not replace, GMDSS. | Defines the input of TR-19. | T | SR-RS-01 | TBR |
| TR-35 | Performance | The system shall deliver messages within the time of their message class: distress 2 min, hazard warning 10 min, route update or directive 15 min (TBR), routine report 30 min (TBR); each for ≥ 95% (TBR) of messages, distress ≥ 99% (TBR). The time starts when the system releases the message. | One table instead of the different 2, 5, 10 and 15 min values in TR-09, TR-10, TR-11 and TR-19. | T | SR-SC-02, SR-SC-03, SR-PA-02, SR-RS-01 | TBR |
| TR-36 | Performance | A ship that has not reported for 30 min shall be shown with its last position and an uncertainty radius that grows with the estimated ice drift and ship speed, and the dispatcher shall be alerted after 60 min (TBR). A ship whose reported displacement is below N m per H hours shall be flagged as stationary (suggested start: 500 m per 3 h, TBR). | Tracking in drift terms instead of a 10 m accuracy; a waiting ship is not lost. | T | SR-OW-01, SR-PA-01, SR-RS-01 | TBR |
| TR-37 | Functional | The on-board terminal shall show each route recommendation to the master and record his acceptance or rejection with the time. | The master keeps final authority (SOLAS V/34-1); the decision enters the log (TR-08). | D | SR-DI-01, SR-RG-01 |  |
| TR-38 | Functional | The system shall show owners, logistics operators and Port Authorities the position, ETA and status of the ships they are authorised to see. | Functional requirement behind SR-OW-01, SR-PA-01 and SR-OW-02. | D | SR-OW-01, SR-OW-02, SR-PA-01 |  |
| TR-39 | Functional | The system shall send a Port Authority directive to all ships inside the area or on the routes named in the directive. | Functional requirement behind SR-PA-02 ('affected ships'). | T | SR-PA-02 |  |
| TR-40 | Safety | The system shall show the dispatcher a loss of the ALARM function, of a data source or of a link within 5 min (TBR). | No silent failure. | T | SR-DI-01, SR-ALL-01 | TBR |
| TR-41 | Safety | When a function, data source or link fails, the system shall continue in a degraded mode, keep showing the last valid data together with its age, and shall not present stale or missing data as current. | No silent failure: the user always knows what is out of date. | T | SR-ALL-01, SR-DI-01 |  |
| TR-42 | Interface | The system shall limit its requests to each satellite operator to the agreed monthly quota and shall log every request. | Quota and interfaces are fixed in the interface documents with each operator. | T | SR-SS-01 | TBR |
| TR-43 | Reliability and maintainability | Built-in test shall isolate at least 90% of ground equipment failures to one line-replaceable unit that can be replaced, restoring service within 4 h (TBR). | Ground sites in the Arctic are hard to reach. | D | SR-GM-01 | TBR |

## Traceability

| SR | Satisfied by |
| --- | --- |
| SR-SC-01 | TR-02, TR-13, TR-14, TR-21, TR-26, TR-29 |
| SR-SC-02 | TR-03, TR-04, TR-05, TR-11, TR-12, TR-15, TR-21, TR-35 |
| SR-SC-03 | TR-07, TR-09, TR-10, TR-22, TR-23, TR-24, TR-33, TR-35 |
| SR-OW-01 | TR-01, TR-16, TR-17, TR-20, TR-36, TR-38 |
| SR-OW-02 | TR-27, TR-28, TR-38 |
| SR-PA-01 | TR-01, TR-09, TR-17, TR-20, TR-23, TR-36, TR-38 |
| SR-PA-02 | TR-07, TR-18, TR-20, TR-35, TR-39 |
| SR-DI-01 | TR-03, TR-04, TR-05, TR-06, TR-10, TR-15, TR-32, TR-37, TR-40, TR-41 |
| SR-RS-01 | TR-01, TR-19, TR-34, TR-35, TR-36 |
| SR-SS-01 | TR-21, TR-42 |
| SR-RG-01 | TR-06, TR-08, TR-29, TR-30, TR-31, TR-37 |
| SR-SM-01 | TR-24, TR-25 |
| SR-GM-01 | TR-33, TR-43 |
| SR-ALL-01 | TR-26, TR-40, TR-41 |

## Verification summary

| Type | T | A | I | D | Total |
| --- | --- | --- | --- | --- | --- |
| Functional | 8 | 1 | 1 | 2 | 12 |
| Performance | 9 | 5 | 0 | 0 | 14 |
| Interface | 2 | 0 | 0 | 0 | 2 |
| Environmental | 2 | 0 | 0 | 0 | 2 |
| Reliability and maintainability | 0 | 2 | 0 | 2 | 4 |
| Safety | 3 | 0 | 0 | 0 | 3 |
| Security | 1 | 0 | 1 | 0 | 2 |
| Regulatory | 0 | 0 | 3 | 0 | 3 |
| Human factors | 0 | 0 | 0 | 1 | 1 |
| Total | 25 | 8 | 5 | 5 | 43 |

## Open items: 21

| Kind | Affects | Item | Owner |
| --- | --- | --- | --- |
| Value | SR-SC-01, TR-13 | Ice information age of 24 h: confirm with a Kondor-FKA revisit simulation over the NSR before status Agreed (the RCM benchmarks are for comparison only). | Analysis lead (assign) |
| Value | TR-21 | Ground link capacity of 100 Mbit/s: size from the daily SAR and meteo data volume. | Interface engineer (assign) |
| Value | Scope | Service area: define once as the route ±20 nm plus the ports of Murmansk and Arkhangelsk (list the ports), check against the official NSR water area, and use it in SR-SC-03, TR-09 and the map slide (slide says 64°N, earlier text 66°N and Kara Gates–Bering Strait). | Vladislav (Requirements/MBSE) |
| Assumption | Boundary | Data Analysis Centers' models are inside the system boundary; the SAB currently shows them as an external actor. | Vladislav (Requirements/MBSE) |
| Assumption | TR-21 | SAR and meteo data reach the system through the satellite operators' ground segments, not through Gonets/Sfera. | Interface engineer (assign) |
| Assumption | Interfaces | ICD-01 to ICD-06 are written by the interface engineer and baselined with the requirements. ICD-01 gets the field "persons on board". | Interface engineer (assign) |
| Assumption | Benchmarks | RCM benchmarks (daily 50 m ice, 10–30 min maritime latency) are used for comparison only; Kondor-FKA values replace them after the simulation. | Analysis lead (assign) |
| Decision | SR-SC-03, TR-09, TR-35 | Which satellites carry ship-shore messaging (Gonets, Sfera, GEO)? Run a coverage and latency simulation before fixing 95% / 99% and the class times. Review M5, M6. | Analysis lead (assign) |
| Decision | SR-DI-01, TR-15 | Back-test the ALARM function on the 2024–2025 season and tighten 90% / 30% (TBR) towards a 10% false alarm ratio; confirm the definition of a hazard event. Review M8. | Risk model owner (assign) |
| Value | TR-36, SR-RS-01 | Set N m per H h for the stationary flag (suggested 500 m per 3 h) and the 30 / 60 min limits for a silent ship. Review M9. | Analysis lead (assign) |
| Value | TR-22, TR-33 | Environmental profile for the on-board antenna and the ground terminals (temperature, wind, snow and ice, motion). Where will the ground terminals be? Review M10, M11. | Systems architect (assign) |
| Decision | Stakeholders | Scope of Icebreaker operators and NSR administration (no system requirement yet). Rebuild the "WHO" slide from the Stakeholders sheet. Review C1. | Vladislav (Requirements/MBSE) |
| Decision | SR-PA-02 | Who issues route-wide directives: Port Authorities (for their port) or the NSR administration? The table keeps the Port Authorities for now. Review C4. | Vladislav (Requirements/MBSE) |
| Decision | SR-DI-01, TR-06 | Who is the dispatcher (shipping company or NSR operations centre)? The system gives recommendations; the master keeps the final decision (SOLAS V/34-1). Review C2. | Vladislav (Requirements/MBSE) |
| Assumption | SR-RS-01, TR-34 | The service supplements GMDSS (SOLAS IV) and does not replace it. The distress alert comes from the SOS button on our terminal; forwarding of GMDSS alerts is open. Review C6. | Vladislav (Requirements/MBSE) |
| Decision | TR-03, TR-04 | Define the risk score (inputs, scale, model) or point to the risk model document; the threshold 70 is TBR. Review C22. | Risk model owner (assign) |
| Value | TR-20 | Peak number of ships in the NSR at one time and the margin for 500 ships / 50 sessions. Review C21. | Analysis lead (assign) |
| Decision | TR-28 | Is certification of the GOST R 34.12-2015 cryptography needed? Review C19. | Vladislav (Requirements/MBSE) |
| Decision | TR-17, TR-35 | Position reports need their own delivery class (about 5 min) to keep the 15 + 5 + 10 min budget; add it to TR-35 or change the budget. Review M5, M7. | Vladislav (Requirements/MBSE) |
| Decision | TR-42, TR-43 | Added so that SR-SS-01 and SR-GM-01 have two technical requirements each: confirm or replace. | Vladislav (Requirements/MBSE) |
| Decision | Risks | Link each of the top 3 risks of the risk register to at least one technical requirement and one verification (add a Risk column). Review C18. | Risk model owner (assign) |

## Revision history

| Version | Date | Author | Change |
| --- | --- | --- | --- |
| v0.3 | 2026-10-29 | Vladislav Zagorodnyuk | Reduced to 11 SR and 32 TR with concrete values |
| v0.4 | 2026-11-03 | Vladislav Zagorodnyuk | Review remarks applied (M1–M12, C1–C27; see the Review log sheet): SR IDs by stakeholder code, 14 SR (new SR-SS-01, SR-GM-01, SR-ALL-01), 43 TR (new TR-33…TR-43, message classes in TR-35), TBR marked, 21 open items |
