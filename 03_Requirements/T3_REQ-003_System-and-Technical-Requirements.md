# System and technical requirements

| CI | Version | Status | Owner | Updated |
| --- | --- | --- | --- | --- |
| REQ-003 | v0.3 | Draft | Vladislav Zagorodnyuk | 2026-10-29 |

Written to the NASA SE Handbook rules: one "shall" per requirement, measurable values, one verification method (T test, A analysis, I inspection, D demonstration) and a trace to a system requirement. The same content is in [the Excel file](T3_REQ-003_System-and-Technical-Requirements.xlsx) (with traceability matrix) and in the [shared doc](https://claude.ai/artifact/XdnaVzd9gVZ4JKDw3HB5Zk).

## System requirements (SR)

| ID | Stakeholder | Requirement | MOE (target) | Validation |
| --- | --- | --- | --- | --- |
| SR-01 | Ship operators | The system shall give the ship's bridge current ice information for the planned route at any time of day or night and in any weather. | Age of ice information on the bridge ≤ 24 h (TBR) for ≥ 95% of voyage time | A |
| SR-02 | Ship operators | The system shall warn the ship of ice and storm hazards on its planned route early enough to change course safely. | Warning ≥ 6 h before reaching the hazard zone in ≥ 90% of hazard events | A |
| SR-03 | Ship operators | The system shall keep two-way communication between ship and shore available along the whole Northern Sea Route. | ≥ 99% of messages delivered within 5 min anywhere in the service area | D |
| SR-04 | Ship and cargo owners, Logistics Operators | The system shall let owners and logistics operators follow the position and ETA of their ships. | Position age ≤ 30 min; ETA error ≤ 6 h at 72 h ahead in ≥ 90% of voyages | A, D |
| SR-05 | Port Authorities | The system shall give Port Authorities a live picture of all connected ships on the Northern Sea Route. | 100% of connected ships shown; position age ≤ 30 min | D |
| SR-06 | Port Authorities | The system shall deliver Port Authority directives to all affected ships and confirm receipt. | ≥ 99% of affected ships acknowledge within 30 min | D |
| SR-07 | Dispatcher | The system shall let the dispatcher decide on route changes quickly, based on alarms that can be trusted. | Decision ≤ 10 min after the alarm in ≥ 90% of operator trials; false alarm ratio ≤ 10% | D, A |
| SR-08 | Rescue Services | The system shall pass distress information to Rescue Services quickly and with an accurate position. | Request received ≤ 2 min after the distress alert; position error ≤ 10 m (95%) | T |
| SR-09 | Regulators, Port Authorities | The system shall comply with the NSR navigation rules, the Polar Code and the radio and marine equipment regulations that apply to it. | 0 non-conformities at regulatory inspection and in an audit of 100 route recommendations | I |
| SR-10 | Ship and cargo owners | The system shall keep each owner's commercial data hidden from other owners and third parties. | 0 unauthorised data accesses in the acceptance penetration test | T |
| SR-11 | Maintenance staff | The system shall let maintenance staff find and replace a failed on-board unit quickly. | Fault isolated to one replaceable unit in ≥ 90% of failures; repair ≤ 1 h | D |

## Technical requirements (TR)

| ID | Type | Requirement | Rationale | Verif. | Traces to |
| --- | --- | --- | --- | --- | --- |
| TR-01 | Functional | The on-board terminal shall send a ship data report (ship ID, GNSS position, course and speed over ground, heading, sensor data per ICD-01) every 15 min by default, configurable from 5 to 60 min. | 15 min keeps displayed positions within the 30 min age limit. | T | SR-04, SR-05, SR-08 |
| TR-02 | Functional | The system shall produce ice charts from SAR data giving ice concentration, stage of development and form of ice, at a spatial resolution of 50 m or finer (5 m or finer in the NSR key straits). | WMO ice chart parameters; 50 m matches the RCM ice mode, Kondor-FKA images at up to 1 m. | I | SR-01 |
| TR-03 | Functional | The system shall recompute the risk score (0 to 100) of each ship and of each 10 km route segment ahead of it within 15 min of new ice, weather or ship data. | Keeps risk current with the 15 min reporting cycle. | T | SR-02, SR-07 |
| TR-04 | Functional | The system shall raise an ALARM when a ship's risk score exceeds 70 (configurable) or its planned route enters a hazard zone within the next 24 h. | Starts the warning and route-change scenario (S2). | T | SR-02, SR-07 |
| TR-05 | Functional | Within 5 min of each ALARM, the system shall generate at least 2 alternative routes, each with ETA, distance, fuel estimate and risk score. | The dispatcher needs ranked options to decide within 10 min. | T | SR-02, SR-07 |
| TR-06 | Functional | The system shall send a route change to a ship only after a dispatcher has approved it. | A named person stays accountable for every route decision. | T | SR-07, SR-09 |
| TR-07 | Functional | The system shall resend each route update or directive that the on-board terminal has not acknowledged up to 3 times at 2 min intervals, then alert the dispatcher. | No silent delivery failure of safety messages. | T | SR-03, SR-06 |
| TR-08 | Functional | The system shall keep a tamper-evident log of all datasets, alarms, decisions and sent messages, time-stamped to UTC within ±1 s, for at least 5 years. | Accountability and incident investigation. | I | SR-09 |
| TR-09 | Performance | Ship-to-shore and shore-to-ship messaging shall be available ≥ 99.0% of the time over any 30-day period everywhere on the NSR between 66°N and 82°N. | Covers high-latitude legs; verified by coverage and outage simulation. | A | SR-03, SR-05 |
| TR-10 | Performance | Route updates and text messages shall reach the addressed ship within 5 min for ≥ 99% of messages. | Keeps the dispatcher-to-ship loop short. | T | SR-03, SR-07 |
| TR-11 | Performance | Hazard warnings shall reach affected ships within 10 min of the ALARM for ≥ 95% of warnings, without waiting for dispatcher approval. | Warnings are information, not commands; RCM gives 10–30 min for maritime surveillance. | T | SR-02 |
| TR-12 | Performance | Hazard warnings shall be issued at least 6 h before the ship's forecast entry into the hazard zone in ≥ 90% of hazard events. | Ships in ice need hours to re-route or wait for an icebreaker. | A | SR-02 |
| TR-13 | Performance | The age of ice information shown on the bridge shall not exceed 24 h (TBR) for ≥ 95% of voyage time. | Key TPM: SAR revisit time plus processing and delivery time. | A | SR-01 |
| TR-14 | Performance | The system shall publish an ice chart within 60 min of receiving a SAR product. | Ice drifts tens of kilometres per day; processing adds to information age. | T | SR-01 |
| TR-15 | Performance | The ALARM function shall detect ≥ 95% of hazard events with a false alarm ratio of no more than 10% on the validation dataset. | Balances safety against dispatcher trust in alarms. | A | SR-02, SR-07 |
| TR-16 | Performance | The ETA forecast error shall not exceed 6 h at 72 h ahead in ≥ 90% of voyages. | Back-tested on recorded 2024–2025 NSR voyages. | A | SR-04 |
| TR-17 | Performance | Ship positions shown on dashboards shall be no older than 30 min. | Directly measures SR-04 and SR-05. | T | SR-04, SR-05 |
| TR-18 | Performance | Port Authority directives shall be acknowledged by ≥ 99% of affected ships within 30 min of release. | Directly measures SR-06. | T | SR-06 |
| TR-19 | Performance | The system shall send a rescue request with ship ID, GNSS position (error ≤ 10 m, 95%), time and persons on board to Rescue Services within 2 min of receiving a distress alert. | Implements the emergency scenario (S6). | T | SR-08 |
| TR-20 | Performance | The system shall track at least 500 ships at once and serve at least 50 concurrent operator sessions while meeting all latency requirements. | Margin for NSR traffic growth (37.8 Mt of cargo in 2024). | T | SR-05 |
| TR-21 | Interface | The system shall receive SAR products (GeoTIFF, ICD-02) and meteorological data (WMO GRIB2, ICD-03) from the satellite operators' ground segments over secure terrestrial links of at least 100 Mbit/s (TBR). | SAR volumes are too large for the low-rate satellite relay. | T | SR-01, SR-02 |
| TR-22 | Environmental | The on-board antenna unit shall operate at air temperatures from −40 °C to +55 °C. | IEC 60945 exposed-equipment conditions, extended to Arctic winter. | T | SR-03 |
| TR-23 | Reliability and maintainability | The ground platform shall have an operational availability of at least 99.5% per year, excluding no more than 8 h of planned maintenance. | Supports the 99.0% end-to-end messaging availability. | A | SR-03, SR-05 |
| TR-24 | Reliability and maintainability | The on-board terminal shall have a mean time between failures of at least 20 000 h. | About one failure in 2.3 years of continuous use. | A | SR-11 |
| TR-25 | Reliability and maintainability | Built-in test shall isolate at least 90% of on-board terminal failures to one line-replaceable unit that ship staff can replace within 1 h using on-board spares. | Ships may be weeks away from a port with service. | D | SR-11 |
| TR-26 | Safety | The system shall mark ice information older than 48 h as DEGRADED on all displays. | Stale ice data shown as current is a navigation hazard. | T | SR-01 |
| TR-27 | Security | The system shall give each user access only to the data allowed by their role; owners shall see only their own ships. | Directly implements SR-10. | T | SR-10 |
| TR-28 | Security | All data links shall be encrypted with a nationally approved algorithm using keys of at least 256 bit. | Ship positions and cargo data are commercially sensitive. | I | SR-10 |
| TR-29 | Regulatory | Route recommendations shall comply with the current NSR navigation rules and include the Polar Code Chapter 11 ice information (current extent and type of ice near the route). | Mandatory for ships on the NSR; Polar Code 11.3.3. | I | SR-09, SR-01 |
| TR-30 | Regulatory | All system radio links shall operate only in the frequency bands and power limits licensed by the national frequency authority. | ITU Radio Regulations and national law. | I | SR-09 |
| TR-31 | Regulatory | The on-board terminal shall hold a type approval certificate, based on IEC 60945 tests, from the Russian Maritime Register of Shipping or the flag state's classification society. | Required for installation on classed ships. | I | SR-09 |
| TR-32 | Human factors | A dispatcher shall be able to review an ALARM and approve or reject a route change within 10 min, with all inputs on one screen, in ≥ 90% of trials. | Directly measures SR-07. | D | SR-07 |

## Traceability

| SR | Satisfied by |
| --- | --- |
| SR-01 | TR-02, TR-13, TR-14, TR-21, TR-26, TR-29 |
| SR-02 | TR-03, TR-04, TR-05, TR-11, TR-12, TR-15, TR-21 |
| SR-03 | TR-07, TR-09, TR-10, TR-22, TR-23 |
| SR-04 | TR-01, TR-16, TR-17 |
| SR-05 | TR-01, TR-09, TR-17, TR-20, TR-23 |
| SR-06 | TR-07, TR-18 |
| SR-07 | TR-03, TR-04, TR-05, TR-06, TR-10, TR-15, TR-32 |
| SR-08 | TR-01, TR-19 |
| SR-09 | TR-06, TR-08, TR-29, TR-30, TR-31 |
| SR-10 | TR-27, TR-28 |
| SR-11 | TR-24, TR-25 |

**Open values (TBR):** TR-13 ice information age 24 h (confirm with SIM-001); TR-21 ground link 100 Mbit/s (size from data volume).

## Revision history

| Version | Date | Author | Change |
| --- | --- | --- | --- |
| v0.3 | 2026-10-29 | Vladislav Zagorodnyuk | Reduced to 11 SR and 32 TR with concrete values |
