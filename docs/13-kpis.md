---
layout: default
title: 13. KPIs & Success Metrics
subtitle: How we measure data health and the success of the program.
---

<span class="badge placeholder">Placeholder</span>

## Data-health KPIs

| KPI | Definition | Source | Baseline | Target | Owner |
|---|---|---|---|---|---|
| Read completeness % | Reads received ÷ reads expected | INTERVALDATA vs. READ_SCHEDULE | _TODO_ | _TODO_ | _TODO_ |
| Estimated read % | Estimated ÷ total reads | VEE flags | _TODO_ | _TODO_ | _TODO_ |
| VEE exception rate | Exceptions ÷ total reads | Exception queue | _TODO_ | _TODO_ | _TODO_ |
| Time-to-resolve exception | Avg. hours to clear an exception | Exception queue | _TODO_ | _TODO_ | _TODO_ |
| Endpoint comms success % | Endpoints reporting on schedule | COLLECTORSTATS, ENDPOINTSTATUSCODEHISTORY | _TODO_ | _TODO_ | _TODO_ |
| Data timeliness | % reads landed before billing window | BILLINGCYCLES | _TODO_ | _TODO_ | _TODO_ |

## Program KPIs

| KPI | Definition | Target |
|---|---|---|
| Catalog coverage % | Tables/columns documented ÷ total | _TODO_ |
| Domains with named steward | Count ÷ total domains | _TODO_ |
| VEE rules published | Rules in the VEE register | _TODO_ |
| M2T mappings validated % | Meter-to-transformer mappings confirmed or corrected via M2T ÷ total | _TODO_ |

## Reporting cadence

_TODO: who reports, to whom, how often, and where the dashboard lives. Tie exception/quality
KPIs back to [Data-Quality]({{ '/08-data-quality-framework.html' | relative_url }})._

---

### Source references
- DOE, *Leveraging AMI Networks and Data* (2019) — AMI performance and value metrics.
- EPA, *AMI Guidance* (2021) — data-quality measurement expectations.
