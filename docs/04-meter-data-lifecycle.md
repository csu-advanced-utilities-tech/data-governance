---
layout: default
title: 4. Meter-Data Lifecycle Governance
subtitle: Governance controls at each stage from meter to archive.
---

<span class="badge draft">Draft</span>

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

## Daily file-extract &amp; transfer schedule

Reads and billing files are pulled from Command Center / the AMI head end on an automated daily
schedule and delivered downstream (billing document server and the
[Consumer Portal]({{ '/10-architecture-lineage.html' | relative_url }}) via SFTP). The schedule
below is from the file-transfer scheduler; statuses are a sample run (they reset each day).

**Legend:** *EGW* = electric/gas/water interval files · *Scalar* = cumulative register reads ·
*CMEP* = Common Meter Export Protocol (AMR interval) · *AMRLSF* = AMR load/scalar file.

| Trigger | Job | Type | Sample status |
|---|---|---|---|
| 1:10 AM | AMI EGW Interval File Get (12 AM) | Interval | Completed |
| 3:20 AM | AMI Electric Scalar File Get (1 AM) | Scalar | Completed |
| 4:20 AM | AMI Electric Scalar File Get (3 AM) | Scalar | Completed |
| 5:20 AM | AMI EGW Interval File Get (4 AM) | Interval | Completed |
| 6:30 AM | AMI Electric Scalar File Get (5 AM) | Scalar | Completed |
| ~6 AM | AMI W (water) Scalar File Get (6 AM) | Scalar | Completed |
| 7:20 AM | AMR billing upload → Doc Server (external) | Billing | Completed |
| 8:20 AM | AMI EG Scalar File Get (7 AM) | Scalar | Completed |
| ~8 AM | AMI Event File Get (8 AM) | Events | Completed |
| 9:20 AM | AMI EGW Interval File Get (8 AM) | Interval | Completed |
| 10:24 AM | AMI Electric Scalar File Get (9 AM) | Scalar | Completed |
| 11:20 AM | Daily Reads (AMR Scalar) Get (10 AM); AMI Electric Scalar (11 AM); AMR billing upload | Scalar / Billing | Completed |
| 12:33 PM | CM-AMRLSF File Get; CMEP (AMR Interval) Get; AMI EGW Interval File Get (12 PM) | Scalar / Interval | Completed → waiting |
| 4:35 PM | AMI EGW Interval File Get (4 PM) | Interval | Waiting on dependencies |
| 8:20 PM | AMI EGW Interval File Get (8 PM) | Interval | Waiting on dependencies |

> **Pattern:** interval files (EGW) run roughly every 4 hours (12 AM, 4 AM, 8 AM, 12 PM, 4 PM, 8 PM);
> scalar/register files run hourly through the morning; billing uploads run mid-morning. A failed or
> late **Get** here is a completeness risk — tie it to the
> [data-timeliness KPI]({{ '/13-kpis.html' | relative_url }}). _TODO: confirm scheduler/tool and owner._

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
