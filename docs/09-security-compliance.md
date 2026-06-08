---
layout: default
title: 9. Security & Compliance
subtitle: PII handling, access control, auditability, and the obligations in our vendor contract.
---

<span class="badge draft">Draft — from Master Agreement</span>

> **⚠️ Public-repo note.** This site is public. Keep this page to *policy and structure* — never
> add real customer data, credentials, or sensitive contract specifics. Some items below are
> drawn from the confidential Master Agreement; review before publishing externally.

## Data classification

| Class | Examples (catalog) | Handling requirement |
|---|---|---|
| Confidential — customer | ADDRESS, SERVICELOCATIONS, USERS | Per contract, customer names, addresses, phone numbers, usage, and financial info are **Confidential Information whether or not marked**; need-to-know access, masked in non-prod |
| Sensitive operational | ENDPOINTS, GPSLOCATIONS, COMMANDLOG | Need-to-know access |
| Internal | EVENTTYPES, STATUSCODES, code tables | Standard internal access |

## PII inventory

_TODO: enumerate PII-bearing columns (cross-reference the catalog's column metadata) and the
retention for each._ Note the contract's stance below limits PII exposure to the vendor head-end.

## Access control

- The Command Center head-end is reached through a **password-protected portal** under an
  **Enterprise Access License** (no per-seat limit); CSU manages its authorized users.
- The vendor maintains **provisioning/de-provisioning** that removes access on employee
  termination or role change.
- **Data residency:** CSU data must reside in the **continental U.S.** at all times.
- **PII minimization:** under the managed-services terms CSU agrees **not to send PII into the
  head-end** beyond what is necessary; if PII is mistakenly provided, CSU notifies the vendor and
  the parties remediate.

| Role | Read | Write | Admin |
|---|---|---|---|
| Data steward | Domain | Metadata | — |
| Operations | Operational tables | — | — |
| Billing | Read / interval data | — | — |
| DBA / admin | All | All | Yes |

_TODO: map to actual USERROLE values in the Command Center._

## Resilience &amp; recovery

- **RPO ≤ 1 hour** (maximum data loss) and **RTO ≤ 24 hours** (maximum recovery time) for the
  head-end, with disaster recovery to a geographically separate secondary data center.
- Vendor maintains a Business Continuity / Disaster Recovery plan and notifies CSU on activation.

## Auditability

- **CSU audit rights:** vendor keeps billing/payment records for **5 years**; CSU may audit
  (generally once per year with notice).
- **Physical security** (vendor data centers): badge/biometric access, video surveillance retained
  ~90 days, access logs retained ~60 days.
- _TODO: what CSU logs internally (edits to reads, PII access, command issuance via COMMANDLOG),
  where logs live, retention, and who reviews them._

## Compliance obligations

| Obligation | Source | Notes |
|---|---|---|
| Colorado Open Records Act (CORA) | C.R.S. § 24-72-201 et seq. | CSU is a public entity; shapes confidential-info handling &amp; disclosure |
| FACT Act | 15 U.S.C. § 1681 (2003) | Applies to customer financial/identity info when applicable |
| Software Security Rider | Master Agreement, Exhibit X | Vendor software security obligations |
| Data Security Rider | Master Agreement, Exhibit Z | Vendor data security obligations |
| Contractor Access Security Policy | Master Agreement, Exhibit D | Controls for vendor access to CSU premises/systems |
| Governing law / venue | Master Agreement | Colorado law; El Paso County District Court |

> **Framework note:** the [National Grid grid-edge report]({{ '/info/resources.html' | relative_url }})
> (a benchmark, not CSU) organizes its cybersecurity around the **NIST Cybersecurity Framework**
> (Identify / Protect / Detect / Respond &amp; Recover) — a useful model if CSU wants to map controls
> to a recognized framework. _TODO: confirm CSU's own information-security policy and any NERC CIP
> applicability._

---

### Source references
- **CSU–Landis+Gyr Master Agreement** (2019) — confidentiality, security riders, data residency, audit _(confidential)_.
- EPA, *AMI Guidance* (2021) — data security &amp; privacy expectations for AMI.
