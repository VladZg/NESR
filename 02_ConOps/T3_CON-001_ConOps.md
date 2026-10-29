# Concept of operations (ConOps)

| CI | Version | Status | Owner | Updated |
| --- | --- | --- | --- | --- |
| CON-001 | v0.1 | Draft | Jash Joshi | 2026-10-29 |

> Starter text. Sections marked TODO are to be completed before PDR.

## 1. Purpose and scope

Describes how NESR SCMS is used by its stakeholders along the Northern Sea Route, in nominal, degraded and emergency situations.

## 2. Mission

See [mission statement and NGO](../03_Requirements/T3_REQ-001_Mission-Statement-and-NGO.md).

## 3. Operational environment

- NSR water area, 66°N to 82°N, Kara Gates to Bering Strait.
- Polar night for months, frequent cloud and fog: ice must be observed by SAR.
- Air temperatures down to about −40 °C; icing of deck equipment.
- Sparse terrestrial infrastructure; geostationary satellites low on the horizon above about 75°N.

## 4. System overview

The system of interest is the ground integration platform and the on-board terminal. It uses Kondor-FKA (SAR), Arktika-M (meteorology), Gonets/Sfera (relay) and GLONASS (navigation). Context: [CSA diagram](../01_MBSE_Model/diagrams/2_System_Analysis/T3_MOD-005_CSA-Contextual-System-Actors.png); scenario map: [T3_CON-002_Scenario-Map.svg](T3_CON-002_Scenario-Map.svg).

## 5. Operational scenarios

| ID | Scenario | Trigger | Main steps | Outcome |
| --- | --- | --- | --- | --- |
| S1 | Nominal monitoring cycle | Every ship report (15 min) | Ship data → relay → ingest and merge → situational picture → risk scores → dispatcher approval → update to ship | Ship continues the route with current information |
| S2 | Ice or storm ALARM | Risk score > 70 or hazard within 24 h | ALARM → route alternatives → dispatcher decision → route change sent; hazard warning sent at once | Ship re-routes ≥ 6 h before the hazard |
| S3 | Reporting | Formatted data package | Regulatory dashboard (Port Authorities), mission dashboard (Logistics Operators) | Authorities and logistics see status |
| S4 | Regulatory update | Port Authority directive | Directive checked into next update package → ships acknowledge | ≥ 99% of ships acknowledge within 30 min |
| S5 | SAR and meteo acquisition | Satellite pass / imaging request | Kondor-FKA and Arktika-M data via ground segments → ice chart within 60 min | Fresh ice chart for the route |
| S6 | Emergency | Distress alert or critical risk | Rescue request → Rescue Services → status to dispatcher and ship | Request delivered ≤ 2 min |

## 6. Modes

| Mode | Condition | System behaviour |
| --- | --- | --- |
| Nominal | All feeds and links available | Scenarios S1 to S5 |
| Degraded: stale ice data | No SAR for a segment > 48 h | Products marked DEGRADED |
| Degraded: link outage | Relay or gateway unavailable | Messages buffered and resent; bridge alarm |
| Emergency | Distress alert | S6 has priority |

## 7. A day of operation (TODO)

Timeline of one ship transit through the Vilkitsky Strait, showing data flows and decisions.

## 8. Constraints and assumptions

- Satellite constellations are external systems; data quotas are agreed with their operators.
- The system supports, but does not replace, GMDSS distress communication.
- The master keeps responsibility for navigation; routes are decision support.

## Revision history

| Version | Date | Author | Change |
| --- | --- | --- | --- |
| v0.1 | 2026-10-29 | Jash Joshi | First version in the repository |
