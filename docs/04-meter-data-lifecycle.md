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

## Data-delivery timing &amp; SLAs (from the Master Agreement)

These are the contracted delivery commitments from Landis+Gyr; the data-quality dimensions above
sit on top of them.

| Data set | Delivered by | Availability target (SLA) |
|---|---|---|
| Monthly billing reads | Electric 5:00 a.m. / gas &amp; water 7:00 a.m. on the Read Cycle Day | ≥ 99.5% |
| Daily meter reads | Electric 5:00 a.m. / gas &amp; water 7:00 a.m. each day | ≥ 99.5% (monthly avg) |
| Interval reads (5/15/30/60-min) | Same windows | ≥ 98.5% (monthly avg) |

- **Billing Window:** the three calendar days before the Read Cycle Day; a read is "available" if
  delivered within that window.
- Data flows HES → CSU **Smart Grid Gateway** → **MDMS** (see
  [OT/IT Landscape]({{ '/05-ot-it-landscape.html' | relative_url }})). Targets are tracked as
  [KPIs]({{ '/13-kpis.html' | relative_url }}).

## Retention &amp; disposition

- **At the head-end:** the last **180 days** of daily/interval reads are available on a rolling basis.
- **Contract records:** billing-related records are retained for **5 years** (audit provision).
- _TODO: CSU MDMS retention periods per data class; archival and purge triggers (link to
  `DATABASE_MAINT_ARCHIVE`); legal-hold handling._

---

### Source references
- EPA, *AMI System Requirements Specification & Guidance* (2021) — meter-data handling & VEE expectations.
- DOE, *Leveraging AMI Networks and Data* (2019) — operational use of AMI data across the lifecycle.
- NREL, *AMI Data Management* (fy22osti/83877) — storage and MDM practices.
