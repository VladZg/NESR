# Interface management plan

| CI | Version | Status | Owner | Updated |
| --- | --- | --- | --- | --- |
| ARC-009 | v0.1 | Draft | Victoria Kulikova | 2026-10-29 |

> Starter text. Complete the ICDs and the N2 diagram before PDR.

## 1. Purpose

Identify, define, control and verify all interfaces of NESR SCMS.

## 2. Roles

Interface manager: Victoria Kulikova. Owners of both sides of an interface agree its ICD; the configuration manager baselines it.

## 3. Interface list

| ID | Between | Type | ICD | Owner | Status |
| --- | --- | --- | --- | --- | --- |
| IF-01 | On-board terminal ↔ ship sensors and GNSS | Data (IEC 61162-1) | ICD-01 | Victoria Kulikova | Open |
| IF-02 | On-board terminal ↔ Gonets/Sfera relay | RF, messages | ICD-04 | Victoria Kulikova | Open |
| IF-03 | Ground platform ↔ Gonets/Sfera gateways | Data, terrestrial | ICD-04 | Victoria Kulikova | Open |
| IF-04 | Ground platform ↔ Kondor-FKA ground segment | SAR products (GeoTIFF) | ICD-02 | Victoria Kulikova | Open |
| IF-05 | Ground platform ↔ Arktika-M / hydrometeorological service | Meteo data (GRIB2) | ICD-03 | Victoria Kulikova | Open |
| IF-06 | Ground platform ↔ Port Authorities | Secure web API | ICD-05 | Victoria Kulikova | Open |
| IF-07 | Ground platform ↔ Rescue Services | Rescue requests, voice backup | ICD-06 | Victoria Kulikova | Open |

## 4. Process

1. **Identify:** N2 diagram from the SAB and LAB exchanges.
2. **Define:** one ICD per interface (data items, formats, rates, timing, protocols, security).
3. **Control:** ICDs are CIs; changes go through change requests (see CONTRIBUTING.md).
4. **Verify:** interface tests in the V&V plan.

## 5. ICD outline

Purpose · parties · data items and formats · timing and volumes · protocols and security · error handling · verification.

## Revision history

| Version | Date | Author | Change |
| --- | --- | --- | --- |
| v0.1 | 2026-10-29 | Victoria Kulikova | First version in the repository |
