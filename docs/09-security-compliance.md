---
layout: default
title: 9. Security & Compliance
subtitle: PII handling, access control, and auditability for meter data.
---

<span class="badge placeholder">Placeholder</span>

## Data classification

| Class | Examples (catalog) | Handling requirement |
|---|---|---|
| PII / customer | ADDRESS, SERVICELOCATIONS, USERS | Restricted access, masking in non-prod |
| Sensitive operational | ENDPOINTS, GPSLOCATIONS, COMMANDLOG | Need-to-know access |
| Internal | EVENTTYPES, STATUSCODES, code tables | Standard internal access |
| _TODO_ | _TODO_ | _TODO_ |

## PII inventory

_TODO: enumerate PII-bearing columns (cross-reference the catalog's column metadata) and
the lawful basis / retention for each._

## Access control

| Role | Read | Write | Admin |
|---|---|---|---|
| Data steward | Domain | Metadata | — |
| Operations | Operational tables | — | — |
| Billing | Read/interval data | — | — |
| DBA / admin | All | All | Yes |

_TODO: map to actual USERROLE values in the Command Center._

## Auditability

_TODO: what is logged (edits to reads, access to PII, command issuance via COMMANDLOG),
where audit logs live, retention, and who reviews them._

## Compliance obligations

_TODO: applicable regulations/standards (e.g. utility data-privacy rules, NERC/CIP if in
scope, internal audit requirements)._

---

### Source references
- EPA, *AMI Guidance* (2021) — data security & privacy expectations for AMI.
- _TODO: CSU information-security policy; applicable state utility privacy rules._
