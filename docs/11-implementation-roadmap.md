---
layout: default
title: 11. Current Data Implementation Roadmap
subtitle: Phased plan for standing up data governance and filling the catalog.
---

<span class="badge placeholder">Placeholder</span>

## Phases

| Phase | Goal | Key deliverables | Target | Status |
|---|---|---|---|---|
| 0. Foundation | Hub + catalog stood up | This site live; catalog rendering | _TODO_ | In progress |
| 1. Catalog fill | Document the 51 tables | Table + column descriptions, owners | _TODO_ | Not started |
| 2. Quality rules | Publish VEE register; integrate M2T validation | [Data-Quality]({{ '/08-data-quality-framework.html' | relative_url }}) populated | _TODO_ | Not started |
| 3. Roles & RACI | Named stewards per domain | [RACI]({{ '/12-stewardship-raci.html' | relative_url }}) signed off | _TODO_ | Not started |
| 4. KPIs live | Baseline + targets reported | [KPIs]({{ '/13-kpis.html' | relative_url }}) tracked | _TODO_ | Not started |

## Contract &amp; deployment context

- The program runs under a **20-year Master Agreement with Landis+Gyr** (executed July 10, 2019).
- Field deployment is **zone-based**: a zone reaches **Zone Acceptance** when ~99% of its equipment
  is deployed, tested, and communicating with the head-end, then transitions to managed services.
- CSU holds a **termination-for-SLA-failure right** if contracted service levels are missed for three
  consecutive months — a backstop worth tracking against the [KPIs]({{ '/13-kpis.html' | relative_url }}).

## Milestones &amp; dependencies

_TODO: call out dependencies (e.g. catalog fill depends on DBA extract; KPIs depend on
quality rules). Convert any relative dates to absolute dates._

## Risks & assumptions

_TODO: e.g. steward availability, access to production metadata, tooling decisions._

---

### Source references
- DOE, *Leveraging AMI Networks and Data* (2019) — phased AMI value realization.
