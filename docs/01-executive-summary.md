---
layout: default
title: 1. Executive Summary
subtitle: The one-page case for governing Command Center meter data.
---

<span class="badge draft">Draft</span>

> **Purpose.** A single page a director or VP can read in two minutes: what this program
> is, why it matters, what "good" looks like, and what we're asking for.

## What this is

Colorado Springs Utilities runs an Advanced Metering Infrastructure (AMI) program under a 20-year
agreement with **Landis+Gyr**. The vendor's **Command Center** head-end system is our system of
record for meter, endpoint, and interval data, which flows to CSU's Meter Data Management System for
billing and operations. **This initiative establishes formal governance over that data** — so it is
accurate, secure, well-understood, and trusted by everyone who relies on it.

## Why it matters

- **Billing integrity** — meter data drives revenue; bad or late data is lost or disputed revenue.
- **Operational visibility** — outage, voltage, and asset decisions depend on trustworthy reads and
  endpoint status.
- **Regulatory & audit readiness** — as a public entity (subject to CORA) we need defensible data
  lineage, access controls, and retention.
- **Unlocking analytics** — clean, well-mapped data is the foundation for initiatives like
  [Meter-to-Transformer (M2T)]({{ '/08-data-quality-framework.html' | relative_url }}) validation,
  voltage monitoring, and outage analytics.

## Current state (honest snapshot)

- The **AMI solution is deployed** and the head-end delivers reads against contracted service levels.
- A **data catalog exists** (43 tables) but is **~1 table documented** — most descriptions are still empty.
- There is **no published VEE rule register** yet, and **domain ownership/stewardship is still informal**.
- This governance hub is newly stood up; most sections are first-draft.

## Target state

- A **fully documented data dictionary** and **code catalog**.
- A **published VEE / data-quality rule set** and M2T validation feeding GIS corrections.
- **Named owners and stewards** for every data domain, with a working RACI.
- **KPIs tracked against the contracted SLAs**, reported on a regular cadence.

## What we're asking for

- **Sponsorship** of the governance operating model.
- A modest, recurring **time commitment from named stewards** to document and maintain their domains.
- A few **decisions** on access policy, retention, and reporting cadence (see
  [Governance Operating Model]({{ '/03-governance-operating-model.html' | relative_url }})).

---

### Source references
- **CSU–Landis+Gyr Master Agreement** (2019) — program scope and system of record _(confidential)_.
- EPA, *AMI Guidance* (2021); NREL, *AMI Data Management* (fy22osti/83877) — industry framing.
