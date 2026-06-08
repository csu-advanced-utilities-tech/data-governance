---
layout: default
title: 8. Data-Quality Framework
subtitle: Quality dimensions, VEE rules, and the Meter-to-Transformer (M2T) initiative.
---

<span class="badge draft">Draft</span>

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

## M2T — Meter-to-Transformer mapping validation

**M2T (Meter-to-Transformer)** is a data-correctness initiative that uses AMI data to verify
the accuracy of the GIS network model — specifically, which transformer each meter is
connected to.

**How it works:**

1. Pull **voltage data** from AMI meters.
2. Build a **voltage signature shape** for each meter.
3. Run **correlation and clustering** to group meters that behave as if they share a
   transformer.
4. **Compare the clusters to the current GIS mappings.**
5. Output a **confirmation** that a mapping is correct, or a **recommendation** for what
   should be corrected.

**Why it belongs here:** the accuracy of meter-to-transformer (and meter-to-GIS)
associations is a data-quality concern — incorrect topology degrades load analysis, outage
management, and any analytics that depend on the network model. M2T turns AMI data into an
independent check on that topology.

> **Status:** active project led by the data team. _TODO: link to the M2T methodology/repo,
> capture the correlation/clustering approach and thresholds used, and define how confirmed
> vs. recommended-correction results are tracked and fed back to the GIS team._

Coverage and correction outcomes are tracked as a KPI — see
[KPIs & Metrics]({{ '/13-kpis.html' | relative_url }}).

## What counts as an "expected" read (exclusions)

Quality percentages are only fair if we agree on the denominator. The Master Agreement defines
conditions that are **excluded** from performance calculations — i.e. a missing read in these cases
is *not* counted as a quality failure. Stewards should apply the same logic to CSU-side metrics:

- Customer **tamper or physical damage** to equipment; meter not replaced after damage.
- **Meter not energized**, or a line-side disconnect de-energized it.
- **RF interference** from third-party devices outside FCC limits.
- CSU **make-ready / pole-attachment / fiber backhaul** not completed after vendor notice.
- Endpoints flagged for a **field visit / exchange** (awaiting truck roll).
- Database relationship between meter and customer record **not correctly established** by CSU.
- **Force majeure**, or equipment/software **not supplied by the vendor**.

> These exclusions are the boundary between a *vendor* data-quality issue and a *CSU* one — useful
> when triaging the exception queue.

## Connectivity investigation lifecycle (contracted)

For meters that stop reporting, the contract defines a concrete process we can mirror:

1. **Identify** meters failing to communicate for **7 consecutive days**.
2. **Triage within 14 days** — determine whether the cause is the **network** or the **meter**.
3. **Resolve network connectivity within 60 days** (meter issues route to a field visit / RMA).

## Exception handling

- **Queue:** reads that fail validation (or meters flagged by the connectivity process) land in an
  **exception queue**, tagged by rule ID and likely cause (vendor vs. CSU, per the exclusions above).
- **Triage & resolve:** stewards confirm the cause, apply an estimation rule or route to a field
  visit / RMA, and record the disposition with an audit trail.
- **Service-level link:** unresolved vendor-side issues that breach an SLA carry **service credits**
  under the contract (amounts omitted here); CSU-side exceptions are tracked as the **VEE exception
  rate** and **time-to-resolve** KPIs in [KPIs & Metrics]({{ '/13-kpis.html' | relative_url }}).
- _TODO: define the CSU SLA for clearing an exception, and who reviews the queue and how often._

---

### Source references
- EPA, *AMI Guidance* (2021) — VEE expectations and data-quality controls.
- DOE, *Leveraging AMI Networks and Data* (2019) — validation of estimated vs. actual reads.
