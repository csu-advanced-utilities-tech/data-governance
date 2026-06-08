---
layout: default
title: 5. OT/IT Landscape (Current State)
subtitle: The systems that produce, move, and consume meter data today.
---

<span class="badge draft">Draft — from Master Agreement</span>

> Sourced from the CSU–Landis+Gyr Master Agreement (2019). Vendor-operated components are
> **managed services**; CSU owns the downstream systems and field operations. See the
> vendor/CSU split in [Stewardship &amp; RACI]({{ '/12-stewardship-raci.html' | relative_url }}).

## System inventory

| System | Layer | Role | Operated by |
|---|---|---|---|
| Electric AMI meters, AMI Gas Modules, AMI Water Modules | OT (field) | Measure usage; capture reads, events, voltage | Landis+Gyr (equipment); CSU (field install/replace) |
| Gridstream RF mesh — endpoints, collectors, routers/gateways (Wi-SUN) | OT (field/network) | Backhaul reads and commands between meters and the head-end | Landis+Gyr (managed network services) |
| **Command Center** — Head-End System (HES) | IT (head-end) | System of record: collects reads, issues commands, stores AMI data | Landis+Gyr (hosted SaaS) |
| Smart Grid Gateway | IT (integration) | Receives data from the HES and feeds CSU systems | CSU |
| Meter Data Management System (MDMS) | IT | Stores validated reads; produces billing determinants | CSU |
| Billing / CIS | IT | Consumes MDMS determinants to bill customers | CSU _(system name TODO)_ |
| Field tools (Tech Studio / Tech Studio Adapter) | OT (field) | On-site read/configuration of endpoints | Landis+Gyr tooling; CSU field crews |

## Integration points

| Interface | Direction | Timing / SLA | Notes |
|---|---|---|---|
| HES → Smart Grid Gateway → MDMS | inbound to CSU | Electric reads by **5:00 a.m.**; gas/water by **7:00 a.m.** local on the Read Cycle Day | Billing Window = the 3 calendar days before the Read Cycle Day |
| Daily / interval reads | HES → CSU | Daily; intervals in 5/15/30/60-min increments (electric default 15-min) | Last **180 days** available on a rolling basis from the HES |
| Commands (reconnect/disconnect, demand reset) | CSU → HES → meter | Reconnect/disconnect ≥99% within 5 min; demand reset on Read Cycle Day | Batched (≤250 meters per request) |
| Hosting / data residency | — | — | HES hosted in vendor data centers; data must reside in the **continental U.S.** |

## OT/IT boundary &amp; responsibilities

- **Landis+Gyr (vendor side):** owns and operates the RF network and the Command Center head-end
  (hosted SaaS), monitors device health, delivers reads to CSU, and handles network RMA/maintenance.
- **CSU side:** owns endpoint field operations (install, replace, remove from service), make-ready
  work and pole-attachment agreements, the Smart Grid Gateway / MDMS integration, and acceptance
  testing of system upgrades.
- The handoff point is the **Smart Grid Gateway** — data crosses from vendor-managed to CSU-managed
  there.

> A visual of these flows belongs in
> [Architecture &amp; Lineage]({{ '/10-architecture-lineage.html' | relative_url }}).

---

### Source references
- **CSU–Landis+Gyr Master Agreement** (2019) — systems, network, integration timing _(confidential; see [Resources]({{ '/info/resources.html' | relative_url }}))_.
- NREL, *AMI Data Management* (fy22osti/83877) — reference AMI architecture.
