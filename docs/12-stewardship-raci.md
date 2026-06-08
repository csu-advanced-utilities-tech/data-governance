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
| Approve a new VEE rule | A | R | C | C | I |
| Accept an M2T mapping correction & update GIS | A | R | C | I | I |
| Grant/revoke data access | A | C | R | I | I |
| Resolve a data-quality exception | I | R | C | I | I |
| Approve schema change | A | C | R | C | I |
| Report KPIs | I | R | C | A | I |
| _TODO: add CSU-specific activities_ | | | | | |

## Vendor vs. CSU operational responsibilities (from the Master Agreement)

The Master Agreement defines who runs what between **Landis+Gyr (vendor)** and **CSU**. This is the
operational counterpart to the data-governance RACI above.

| Activity | Landis+Gyr | CSU |
|---|---|---|
| Operate &amp; monitor the RF network; network maintenance / RMA | **R, A** | C, I |
| Host, support &amp; maintain the Command Center head-end (SaaS) | **R, A** | C, I |
| Deliver reads to CSU; data-delivery monitoring &amp; SLA reporting | **R, A** | C, I |
| Endpoint install, replacement, or removal from service | C, I | **R, A** |
| Make-ready work &amp; joint-use pole-attachment agreements | C, I | **R, A** |
| Test &amp; approve system upgrades; CSU-side integration testing (MDMS) | C, I | **R, A** |
| Resolve individual endpoint↔network connectivity issues | **R, A** | C, I |
| Issue management, periodic reviews, strategic planning | **R, A** | C, I |

> Full RACI tables (field network ops, endpoints, SaaS, application ops, data delivery, upgrades,
> program management) live in the Master Agreement — see [Resources]({{ '/info/resources.html' | relative_url }}).

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
