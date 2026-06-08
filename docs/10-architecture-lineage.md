---
layout: default
title: 10. Architecture & Lineage Diagrams
subtitle: Text-based (Mermaid) architecture and data-lineage diagrams.
---

<span class="badge draft">Draft</span>

> Diagrams here are **text-based** (Mermaid) so they version-control cleanly and render
> automatically on the site. Edit the fenced ` ```mermaid ` blocks below.

## High-level data flow

Reflects the actual CSU / Landis+Gyr architecture (see
[OT/IT Landscape]({{ '/05-ot-it-landscape.html' | relative_url }})).

```mermaid
flowchart LR
  subgraph FIELD[Field - OT]
    M[Meters & Endpoints<br/>electric / gas / water]
    NET[Gridstream RF mesh<br/>Wi-SUN: collectors, routers, gateways]
  end
  subgraph VENDOR[Landis+Gyr - hosted]
    HES[(Command Center<br/>Head-End System)]
  end
  subgraph CSU[CSU - IT]
    SGG[Smart Grid Gateway]
    MDMS[(MDMS<br/>validated reads)]
    BILL[Billing / CIS]
  end
  M -->|reads, events, voltage| NET
  NET -->|backhaul| HES
  HES -->|reads daily / interval / billing| SGG
  SGG --> MDMS
  MDMS -->|VEE| Q{Validated?}
  Q -->|yes| BILL
  Q -->|no| EX[Exception queue]
  EX -->|estimate / edit / field visit| MDMS
  CSU -.commands: reconnect/disconnect, demand reset.-> HES
  M -.voltage.-> M2T[M2T voltage analytics]
```

## Domain entity relationships

_TODO: confirm against the catalog's `metadata/relationships.csv`._

```mermaid
erDiagram
  ADDRESS ||--o{ SERVICELOCATIONS : "located at"
  SERVICELOCATIONS ||--o{ ENDPOINTS : "has"
  ENDPOINTS ||--o{ METERS : "hosts"
  ENDPOINTS ||--o{ INTERVALDATA : "produces"
  METERS ||--o{ METERCONFIGURATION : "configured by"
  ENDPOINTS ||--o{ ENDPOINTSTATUSCODEHISTORY : "logs"
```

## Lineage: a billing determinant

A worked example — interval consumption from meter to bill:

```mermaid
flowchart LR
  A[Meter register/interval read] --> B[Gridstream backhaul]
  B --> C[(Command Center HES)]
  C --> D[Smart Grid Gateway]
  D --> E[(MDMS)]
  E --> F[VEE validation/estimation]
  F --> G[Billing determinant<br/>e.g. monthly kWh]
  G --> H[Billing / CIS]
```

_TODO: pick one concrete field (e.g. `INTERVALDATA` kWh) and annotate the exact tables, the VEE
rules applied, and the destination, so lineage is concrete rather than abstract._

---

### Source references
- **CSU–Landis+Gyr Master Agreement** (2019) — system topology and data flow _(confidential)_.
- Catalog `metadata/relationships.csv` — authoritative table relationships.
- NREL, *AMI Data Management* (fy22osti/83877) — reference architecture patterns.
