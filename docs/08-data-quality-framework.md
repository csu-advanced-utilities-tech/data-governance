---
layout: default
title: 8. Data-Quality Framework
subtitle: Quality dimensions, VEE rules, and the M2T stipulation.
---

<span class="badge placeholder">Placeholder</span>

## Quality dimensions

We assess meter data across standard dimensions. _TODO: confirm/trim for CSU._

| Dimension | Definition | Example check |
|---|---|---|
| Completeness | All expected reads present | No gaps vs. read schedule |
| Validity | Values within plausible range | Reads within meter limits |
| Consistency | Agreement across related data | Register vs. interval totals reconcile |
| Timeliness | Data arrives within SLA | Reads landed before billing window |
| Uniqueness | No duplicate reads | One read per interval per endpoint |
| Accuracy | Reflects true consumption | Estimated vs. actual variance |

## VEE rule register

**Validation → Estimation → Editing.** Each rule has an ID, the dimension it protects, the
trigger, the action, and an owner. This register is the authoritative list; the
[lifecycle page]({{ '/04-meter-data-lifecycle.html' | relative_url }}) maps where each runs.

| Rule ID | Type (V/E/E) | Dimension | Trigger condition | Action | Owner |
|---|---|---|---|---|---|
| V-001 | Validation | Validity | Read above meter max | Flag + reject | _TODO_ |
| V-002 | Validation | Completeness | Missing interval(s) | Flag for estimation | _TODO_ |
| E-001 | Estimation | Completeness | Flagged gap | Apply estimation method _TODO_ | _TODO_ |
| ED-001 | Editing | Accuracy | Authorized correction | Edit w/ audit trail | _TODO_ |
| _..._ | | | | | |

## M2T stipulation

> **M2T:** _TODO — capture the exact definition and rule text of the M2T stipulation here,
> including which reads it applies to, the tolerance/threshold, and the disposition when a
> read fails it._ This section is reserved so M2T is governed alongside the VEE rules rather
> than living in tribal knowledge.

## Exception handling

_TODO: how flagged/failed reads are queued, reviewed, and resolved; SLA for clearing
exceptions; link to the exception-rate KPI in [KPIs]({{ '/13-kpis.html' | relative_url }})._

---

### Source references
- EPA, *AMI Guidance* (2021) — VEE expectations and data-quality controls.
- DOE, *Leveraging AMI Networks and Data* (2019) — validation of estimated vs. actual reads.
