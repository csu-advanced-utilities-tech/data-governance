---
layout: default
title: 3. Governance Operating Model
subtitle: How data-governance decisions get made, by whom, and how often.
---

<span class="badge draft">Draft</span>

This model has **two layers**: how CSU governs its own data internally, and how the **vendor
relationship is governed** under the Master Agreement. Both are described below.

## Operating principles

1. **Business-owned, steward-maintained, council-governed** — data is owned by the business area,
   kept current day-to-day by stewards, and policy is set by a cross-functional council.
2. **Document once, in the open** — definitions and rules live in this hub, not in inboxes.
3. **Quality is measured, not assumed** — every quality rule maps to a KPI and a lifecycle stage.
4. **Least-privilege access** — access is need-to-know and reviewed (see
   [Security & Compliance]({{ '/09-security-compliance.html' | relative_url }})).

## Internal governance bodies _(proposed)_

| Body | Mandate | Members _(TODO: name)_ | Cadence |
|---|---|---|---|
| Data Governance Council | Sets policy, approves standards, resolves escalations | Sponsor + domain owners + Procurement/Contract, Security | Monthly _(proposed)_ |
| Stewardship Working Group | Catalog upkeep, VEE rules, data-quality exceptions | Domain stewards + DBA | Biweekly _(proposed)_ |

## Internal decision rights

| Decision type | Proposes | Approves | Informed |
|---|---|---|---|
| New / changed VEE rule | Steward | Council | Billing, Ops |
| Schema / dictionary change | Steward / DBA | Owner | Council |
| Access-policy change | Owner | Council | Security, Vendor |
| Accept M2T mapping correction | Steward | Owner | GIS, Ops |

## Vendor / contract governance (from the Master Agreement)

Changes to the AMI service itself are governed by the contract, not by this council. Key mechanisms:

| Mechanism | What it's for |
|---|---|
| **Task Order** | Authorizes a specific scope of work under the master contract |
| **Purchase Order** | Buys standalone equipment / parts |
| **Change Order / Work Change Directive** | Adds, deletes, or revises work; the formal way to change scope |
| **Written Amendment** | Changes the agreement terms; signed by both parties |

- **Contract owner / notice point:** CSU **Procurement & Contract Services Manager**.
- **Audit rights:** CSU may audit vendor records (generally annually); records retained ~5 years.
- **Dispute resolution:** good-faith negotiation → **non-binding mediation** → litigation in
  **El Paso County District Court** (Colorado law).
- **Service-level enforcement:** missed SLAs carry **service credits**, and persistent failure
  (three consecutive months) gives CSU a **termination right** — track via
  [KPIs]({{ '/13-kpis.html' | relative_url }}).
- **Continuity:** change-of-control notice; termination for convenience with notice; appropriation-of-funds limits (a public-entity protection).
- **Key personnel:** CSU may request replacement of vendor key personnel.

## Standards & policies (register)

_TODO: list governing documents (naming standards, retention policy, access policy) with links and
owners. Candidates: data-classification policy, VEE rule register, access-review SOP._

## Escalation path

**Steward → Stewardship Working Group → Data Governance Council → Sponsor.** Contract/vendor issues
escalate through **Procurement & Contract Services** per the Master Agreement.

---

### Source references
- **CSU–Landis+Gyr Master Agreement** (2019) — change control, dispute resolution, audit, key personnel _(confidential)_.
- EPA, *AMI Guidance* (2021) — governance roles for AMI programs.
