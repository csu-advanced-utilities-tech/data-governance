---
layout: default
title: 10. Architecture & Lineage Diagrams
subtitle: Text-based (Mermaid) architecture and data-lineage diagrams.
---

<span class="badge placeholder">Placeholder</span>

> Diagrams here are **text-based** (Mermaid) so they version-control cleanly and render
> automatically on the site. Edit the fenced ` ```mermaid ` blocks below.

## High-level data flow

```mermaid
flowchart LR
  M[Meters / Endpoints] -->|reads, events| C[Collectors / RF network]
  C -->|packets| CC[(Command Center DB)]
  CC -->|VEE| Q{Validated?}
  Q -->|yes| MDM[(MDM / system of record)]
  Q -->|no| EX[Exception queue]
  EX -->|estimate / edit| MDM
  MDM --> BILL[Billing]
  CC --> ARCH[(Archive)]
```

## Domain entity relationships

_TODO: seed from the catalog's `metadata/relationships.csv`. Example skeleton:_

```mermaid
erDiagram
  SERVICELOCATIONS ||--o{ ENDPOINTS : "has"
  ENDPOINTS ||--o{ METERS : "hosts"
  ENDPOINTS ||--o{ INTERVALDATA : "produces"
  METERS ||--o{ METERCONFIGURATION : "configured by"
  ADDRESS ||--o{ SERVICELOCATIONS : "located at"
```

## Lineage: a billing determinant

_TODO: trace one critical field end-to-end (source table/column → transformations → VEE
rules applied → destination), so lineage is concrete rather than abstract._

---

### Source references
- Catalog `metadata/relationships.csv` — authoritative table relationships.
- NREL, *AMI Data Management* (fy22osti/83877) — reference architecture patterns.
