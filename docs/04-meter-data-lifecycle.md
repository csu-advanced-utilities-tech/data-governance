---
layout: default
title: 4. Meter-Data Lifecycle Governance
subtitle: Governance controls at each stage from meter to archive.
---

<span class="badge placeholder">Placeholder</span>

> The lifecycle is the backbone of this hub: every quality rule, control, and KPI attaches
> to one of these stages.

## Lifecycle stages

| Stage | What happens | Key tables | Primary controls | Owner |
|---|---|---|---|---|
| 1. Collection | Meter/endpoint captures interval & register reads | INTERVALDATA, IDREADINGLOGS | Read-schedule adherence, comms health | _TODO_ |
| 2. Transport / Ingest | Collectors relay packets into Command Center | COLLECTORS, COMMANDLOG, PACKETTYPES | Completeness checks, missing-read detection | _TODO_ |
| 3. Validation (V) | Reads checked against validity rules | INTERVALDATA, EVENTLOG | VEE validation rules → [Data-Quality]({{ '/08-data-quality-framework.html' | relative_url }}) | _TODO_ |
| 4. Estimation (E) | Missing/invalid reads estimated | INTERVALDATALATESTVALUES | Estimation methods, flagging | _TODO_ |
| 5. Editing (E) | Authorized correction of reads | _TODO_ | Audit trail, dual control | _TODO_ |
| 6. Storage / MDM | Validated data persisted as system of record | INTERVALDATALATESTVALUES, IDREADINGLATESTVALUES | Retention, integrity | _TODO_ |
| 7. Billing handoff | Data released to billing | BILLINGCYCLES, PLANSCHEDULES | Billing-determinant sign-off | _TODO_ |
| 8. Archive / Purge | Aged data archived or purged | DATABASE_MAINT_ARCHIVE | Retention policy, legal hold | _TODO_ |

## VEE at a glance

**VEE = Validation, Estimation, Editing** — the industry-standard meter-data quality
process. Detailed rule definitions live in the
[Data-Quality Framework]({{ '/08-data-quality-framework.html' | relative_url }});
this page governs *where in the lifecycle* each control applies and who owns it.

## Retention & disposition

_TODO: retention periods per data class; archival and purge triggers; legal-hold handling._

---

### Source references
- EPA, *AMI System Requirements Specification & Guidance* (2021) — meter-data handling & VEE expectations.
- DOE, *Leveraging AMI Networks and Data* (2019) — operational use of AMI data across the lifecycle.
- NREL, *AMI Data Management* (fy22osti/83877) — storage and MDM practices.
