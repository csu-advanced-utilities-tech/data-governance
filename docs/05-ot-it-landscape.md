---
layout: default
title: 5. OT/IT Landscape (Current State)
subtitle: The systems that produce, move, and consume meter data today.
---

<span class="badge placeholder">Placeholder</span>

## System inventory

| System | Layer | Role | Owner | Integration in / out |
|---|---|---|---|---|
| Meters / Endpoints | OT (field) | Capture reads & events | _TODO_ | → RF network |
| Collectors / RF network | OT | Relay reads to head-end | _TODO_ | meters → Command Center |
| Command Center | IT (head-end) | System of record (AMI) | _TODO_ | collectors → MDM/billing |
| MDM / Billing | IT | Billing determinants | _TODO_ | Command Center → CIS |
| _TODO: CIS / GIS / analytics_ | IT | _TODO_ | _TODO_ | _TODO_ |

## Integration points

_TODO: list each interface — protocol, frequency, data volume, and the failure modes that
matter for data quality._

## OT/IT boundary & responsibilities

_TODO: who owns each side of the OT/IT line; where security zones change (see
[Security & Compliance]({{ '/09-security-compliance.html' | relative_url }}))._

> A visual of these flows belongs in
> [Architecture & Lineage]({{ '/10-architecture-lineage.html' | relative_url }}).

---

### Source references
- NREL, *AMI Data Management* (fy22osti/83877) — reference AMI architecture.
- DOE, *Leveraging AMI Networks and Data* (2019) — head-end / network topology.
