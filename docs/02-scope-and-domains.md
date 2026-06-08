---
layout: default
title: 2. Scope & Data Domains
subtitle: What we govern, what we don't, and how the data is organized into domains.
---

<span class="badge placeholder">Placeholder</span>

## In scope

_TODO: e.g. all data persisted in the Command Center database; the metadata catalog;
VEE/quality rules applied to that data._

## Out of scope (for now)

_TODO: e.g. downstream billing system internals, GIS, customer CRM — note interfaces only._

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
