---
layout: default
title: 8. Data-Quality Framework
subtitle: Quality dimensions, VEE rules, the MMM monitoring register, and Meter-to-Transformer (M2T).
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

## MMM monitoring rule register

The **MMM exception report** is CSU's daily meter-monitoring scan: a set of coded rules that query
Command Center data to flag meters with a data or device problem for investigation (and, where
applicable, a work order). This register is the authoritative list of rules and their criteria.
_TODO: confirm what "MMM" stands for and the report's owner/cadence._

**Common filters:** *not in inventory* = `statuscodeid` ≠ 1 · *has SPID* = endpoint has a
collector/SPU association (i.e. on-network) · *dbsync* = the CIS DB-sync file (see
[OT/IT Landscape]({{ '/05-ot-it-landscape.html' | relative_url }})) · meter types: 1 = electric,
2 = water, 3 = gas, 4 = unspecified, 5 = router. Event/data-definition IDs map to the
[Data Dictionary](https://csu-advanced-utilities-tech.github.io/command-center-data-catalog/index.html).

> **How this register is maintained.** *Current criteria* is what runs in production today.
> *Proposed / notes* tracks changes being workshopped and a planned implementation date; once a change
> ships, the proposed criteria becomes the current criteria and the note is cleared — so the table
> always shows the live rule set. SQL implementations belong in the
> [Code Catalog]({{ '/07-code-catalog.html' | relative_url }}).

| Code | Active | Identifies | Current criteria | Proposed / notes |
|---|---|---|---|---|
| NVM | Yes | Nonvolatile-memory problems | Electric/unspecified (1,4); not in inventory; has SPID; ≥2 "Nonvolatile memory failure detected" (event 2041) in last 7 days | |
| RVR | Yes | Reverse rotation on non-solar meters | Electric (1); not in inventory; has SPID; ≥3 "Reverse Rotation detected" (event 2277) in last 6 days; in dbsync where meter not like %PHOTO% OR route id ends in 09; dbsync insert in last 4 days | |
| MAG | Yes | LEEP devices with stuck magnets | Types 1,2,3,4; not in inventory; has SPID; distinct event days in last 5 days with "RF Water Stuck magnet switch" (4120) / "RF Gas Stuck magnet switch" (3120) | |
| COF | Yes | Gas meters with cover removed after install | Gas (3); not in inventory; has SPID; ≥2 days after last install; ≥2 distinct event days in last 2 days: "RF Gas Cover off" (3121) / "Cover off flag" (3356) | |
| LBF | Yes | Low-battery meters not reading (for replacement) | Water/Gas (2,3); not in inventory; has SPID; ≥2 events in last 4 days: Gas (3124) / Water (4124) / "Water Meter Low Battery" (6249); AND no latest value date OR last value date before today | |
| BWF | Yes | Water flowing backward through the meter | Water (2); not in inventory; has SPID; values decrease 5 consecutive days; ≥1 day's reverse flow > 2 units | |
| EEO | Yes | Repeated power outages / restores | Electric/unspecified (1,4); not in inventory; has SPID; ≥10 outages (event 3) OR 0 outages and ≥10 restores (event 4), all within the day before yesterday | |
| ORP | Yes | Meters without a service location | Types 1,2,3,4; not in inventory now; NO SPID; was in Inventory > 14 days ago | |
| CED | Yes | Read value has more digits than module dials | Types 1,2,3,4; not in inventory; has SPID; latest read value has more digits than the meter is configured to allow | |
| AAA | Yes | Water meters throwing cutwire flags | Water (2); has SPID; midnight reads identical across past 3 days OR > 12 interval records with attributes (1,9,33,65,97,105,129,161,193,225) on any of past 3 days | |
| IVR | Yes | Water meters flagged invalid reads | Water (2); has SPID; midnight reads not null across past 5 days OR ≥12 interval records with attributes (128,160,192,224) yesterday | |
| ECO | No | Possible theft (legacy) | Electric/unspecified (1,4); not in inventory; has SPID; status disconnected (26); first and last read after disconnect not equal | Deprecated — replaced by DIV; good to remove |
| STL | Yes | Meters not reading (stale) | Electric (datadefinition 1): not in inventory/lost; has SPID; no reads for 7 days. Water/gas (datadefinition 29890,1939,26605,26603): same, no reads for 14 days | |
| NEG | Yes | Negative read values | Types 1,2,3,4; not in inventory (statuscodeid≠1); has SPID; latest read negative; latest read after last install | |
| SNN | Yes | Meters not going Normal | Types 1,2,3,4; not in inventory or normal; has a latest read value after last install | |
| GSS | Yes | Gas stuck-sensor events | Gas (3); not in inventory; has SPID; "RF Gas Stuck sensor switch" (3119) on both of past 2 days; event > 2 days after last install | |
| GTS | Yes | Gas tilt-switch events | Gas (3); not in inventory; has SPID; "RF Gas Tilt switch" (3125) on both of past 2 days; event > 2 days after last install | |
| NNR | Yes | No read since initial install (vs STL) | Electric/water/gas (1,2,3); Normal; has SPID; no latest read value recorded; installed ≥ 14 days ago | |
| NINE | Yes | Water 999999 reads with no problem flag | Water (2); has SPID; > 1 999999 interval reads with attribute NOT in (1,9,33,65,97,105,129,161,193,225,128,160,192,224) on either of past 2 days | |
| ZER | No | Zero consumption | Water (2): has SPID; current read = 2-week-old read and both ≠ 999999. Other types: has SPID; current read = 2-week-old read | |
| BADI | Yes | Water non-999999 reads with problem flags | Water (2); has SPID; > 1 non-999999 interval reads with attribute in (1,9,33,65,97,105,129,161,193,225,128,160,192,224) on either of past 2 days | |
| FLIP | Yes | Rapid status switching | Electric/water/gas (1,2,3); has SPID; not in inventory; > 14 status changes in past 14 days | |
| NOMR | Yes | Missing meter-number association | datadefinition 1,29890,1939,26605,26603; not in inventory; meter number null; endpoint not archived; last install earlier than 3 days ago | |
| ZERG | Yes | Gas no consumption since install (vs ZER) | Gas (3); has SPID; first read after install ≥ 14 days ago; total consumption since first read < 5 units | |
| EDA | Yes | Gas External Device Alarm events | Gas (3); not in inventory; has SPID; "RF Gas External Device Alarm" (4589) on both of past 2 days; event > 2 days after last install | |
| DIV | Yes | Possible theft (current) | Disconnected-switch status but load-side voltage > 85% of line-side voltage; OR gas/electric marked no-usage in dbsync but today's read ≠ yesterday's; OR water marked no-usage in dbsync but today's read ≠ yesterday's; today's & yesterday's reads ≠ 999999 | |

> **Cross-links:** these rules map onto the [quality dimensions](#quality-dimensions) above (e.g. STL/NNR →
> completeness; NEG/CED → validity; BWF/AAA/IVR → accuracy/consistency) and feed the exception queue
> below. **DIV** uses load-side vs. line-side voltage — the same voltage-analytics family as
> [M2T](#m2t--meter-to-transformer-mapping-validation).

## Exception handling

- **Detection:** the **MMM monitoring rules** above (plus the connectivity process) are the primary
  way problem meters are flagged each day.
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
- **CSU MMM Criteria Table** — the monitoring rule register reproduced above (internal working sheet).
- EPA, *AMI Guidance* (2021) — VEE expectations and data-quality controls.
- DOE, *Leveraging AMI Networks and Data* (2019) — validation of estimated vs. actual reads.
