---
layout: default
title: 12. Stewardship Roles & RACI
subtitle: Who is Responsible, Accountable, Consulted, and Informed.
---

<span class="badge placeholder">Placeholder</span>

## Role definitions

| Role | Definition |
|---|---|
| Data Owner | Accountable for a domain's data; sets policy and approves access. |
| Data Steward | Day-to-day quality, definitions, and dictionary upkeep for a domain. |
| Data Custodian | Operates the systems/DB that store the data (e.g. DBA). |
| Data Consumer | Uses the data (billing, ops, analytics). |

## RACI matrix

**R**esponsible · **A**ccountable · **C**onsulted · **I**nformed

| Activity | Data Owner | Steward | Custodian (DBA) | Governance Council | Consumer |
|---|---|---|---|---|---|
| Define table/column metadata | A | R | C | I | C |
| Approve a new VEE / M2T rule | A | R | C | C | I |
| Grant/revoke data access | A | C | R | I | I |
| Resolve a data-quality exception | I | R | C | I | I |
| Approve schema change | A | C | R | C | I |
| Report KPIs | I | R | C | A | I |
| _TODO: add CSU-specific activities_ | | | | | |

## Steward assignments by domain

_TODO: fill from [Scope & Data Domains]({{ '/02-scope-and-domains.html' | relative_url }})
once owners are confirmed._

| Domain | Owner | Steward |
|---|---|---|
| Premises & Locations | _TODO_ | _TODO_ |
| Endpoints & Meters | _TODO_ | _TODO_ |
| Interval & Register Reads | _TODO_ | _TODO_ |
| _..._ | | |

---

### Source references
- EPA, *AMI Guidance* (2021) — stewardship and accountability roles.
