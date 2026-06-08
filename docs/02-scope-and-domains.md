---
layout: default
title: 2. Scope & Data Domains
subtitle: What we govern, what we don't, and how the data is organized into domains.
---

<span class="badge draft">Draft</span>

## Program context

The AMI program runs under a **20-year Master Agreement with Landis+Gyr** (executed 2019). It covers
electric AMI meters and AMI-enabled gas and water modules, the Gridstream RF network, the
**Command Center** head-end, and managed services. That contract scopes much of what we govern here.

## In scope

- All data persisted in the **Command Center** head-end database (the [Data Dictionary](https://csu-advanced-utilities-tech.github.io/command-center-data-catalog/index.html) documents it).
- Reads delivered to CSU (billing, daily, interval) via the Smart Grid Gateway into the **MDMS**.
- The metadata catalog and the VEE / data-quality rules applied to that data.

## Out of scope (for now)

- Downstream **billing / CIS** internals (interfaces only).
- **GIS** internals (referenced by [M2T]({{ '/08-data-quality-framework.html' | relative_url }}), governed elsewhere).
- Vendor-internal head-end implementation (Landis+Gyr managed service).

## Data domains

Domains group the catalogued tables into business areas. The grouping below is seeded from
the 51 tables in the [Data Dictionary](https://csu-advanced-utilities-tech.github.io/command-center-data-catalog/index.html);
confirm owners and refine as the catalog is filled in.

| Domain | Representative tables | Business owner | Steward |
|---|---|---|---|
| Premises & Locations | ADDRESS, SERVICELOCATIONS, GPSLOCATIONS | _TODO_ | _TODO_ |
| Endpoints & Meters | ENDPOINTS, METERS, ENDPOINTMODELS, METERCONFIGURATION, ENDPOINTMETERCONFIGURATION, RFENDPOINTPROPERTIES | _TODO_ | _TODO_ |
| Network / Collection | COLLECTORS, COLLECTORSTATS, RSSDEVICES | _TODO_ | _TODO_ |
| Interval & Register Reads | INTERVALDATA, INTERVALDATALATESTVALUES, INTERVALTYPES, IDREADINGLOGS, IDREADINGLATESTVALUES | _TODO_ | _TODO_ |
| Commands & Control | COMMANDLOG, COMMANDSSENT, COMMANDRESPONSE, COMMANDTYPES, COMMANDSTATUSCODES, PACKETTYPES | _TODO_ | _TODO_ |
| Events, Errors & Status | EVENTLOG, EVENTTYPES, ERRORLOG, ERRORTYPES, STATUSCODES, ENDPOINTSTATUSCODEHISTORY | _TODO_ | _TODO_ |
| Plans & Schedules | PLANS, PLANTYPES, PLANSCHEDULES, READ_SCHEDULE, BILLINGCYCLES | _TODO_ | _TODO_ |
| Grouping & Org | GROUPS, GROUPTYPES, ENDPOINTGROUPASSOC | _TODO_ | _TODO_ |
| Access & Admin | USERS, USERROLE, DATADEFINITIONS, DATABASE_MAINT_ARCHIVE, ENDPOINTDEPLOYMENTSTATISTICS, ENDPOINTNOTES | _TODO_ | _TODO_ |

> Domain ownership feeds directly into the [Stewardship & RACI]({{ '/12-stewardship-raci.html' | relative_url }}) matrix.

---

### Source references
- NREL, *AMI Data Management* (fy22osti/83877) — domain decomposition for AMI data.
- EPA, *AMI Guidance* (2021) — meter-data scope definitions.
