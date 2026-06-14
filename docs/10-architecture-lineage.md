---
layout: default
title: 10. Architecture & Lineage Diagrams
subtitle: Text-based (Mermaid) architecture and data-lineage diagrams.
---

<span class="badge draft">Draft</span>

> Diagrams here are **text-based** (Mermaid) so they version-control cleanly and render
> automatically on the site. **Tip: click any diagram to enlarge it.** Edit the fenced
> ` ```mermaid ` blocks below.

## End-to-end process flow (endpoint → C2M billing)

The high-level path a meter read travels from the field to a customer bill. Color bands show who owns
each stage. **Click the diagram to enlarge it.**

```mermaid
flowchart LR
  M["Meter<br/>register / usage read taken"]
  EP["Endpoint / module<br/>captures the read"]
  MESH["RF mesh network<br/>Gridstream / Wi-SUN (self-healing)"]
  GW["Routers and gateway<br/>aggregate and backhaul"]
  HES["Head-End System = Command Center<br/>receives and stores reads"]
  FF["Command Center<br/>generates flat files (EMED / CMEP)"]
  SFTP["SFTP transfer<br/>Secure FTP, port 22"]
  C2M["CSU loads into C2M<br/>MDM + VEE (Oracle Customer To Meter)"]
  BILL["Billing"]

  M --> EP --> MESH --> GW --> HES --> FF --> SFTP --> C2M --> BILL

  classDef field fill:#eff6ff,stroke:#2563eb,color:#111827;
  classDef net   fill:#ecfeff,stroke:#0891b2,color:#111827;
  classDef lg    fill:#ecfdf5,stroke:#059669,color:#111827;
  classDef xfer  fill:#fffbeb,stroke:#b45309,color:#111827;
  classDef csu   fill:#eef2ff,stroke:#4338ca,color:#111827;

  class M,EP field;
  class MESH,GW net;
  class HES,FF lg;
  class SFTP xfer;
  class C2M,BILL csu;
```

**Legend:** blue = field (meter / endpoint) · teal = AMI network (Gridstream / Wi-SUN mesh, routers,
gateway) · green = Landis+Gyr head-end (Command Center) · amber = file transfer (SFTP) · indigo = CSU
(C2M). **C2M** (Oracle Customer To Meter) is a single system whose **SGG** ingests the files, **MDM**
validates and stores them (VEE), and **CC&B** produces the bill. For the detailed system view and the
Consumer-Portal feed, see the diagrams below.

## High-level data flow

Reflects the actual CSU / Landis+Gyr architecture (see
[OT/IT Landscape]({{ '/05-ot-it-landscape.html' | relative_url }})).

```mermaid
flowchart LR
  subgraph FIELD["Field (OT)"]
    M["Meters and Endpoints<br/>electric, gas, water"]
    NET["Gridstream RF mesh (Wi-SUN)<br/>collectors, routers, gateways"]
  end
  subgraph VENDOR["Landis+Gyr (hosted)"]
    HES[("Command Center<br/>Head-End System")]
  end
  subgraph CSUZONE["CSU (IT)"]
    SGG["Smart Grid Gateway"]
    MDMS[("MDMS<br/>validated reads")]
    BILL["Billing / CIS"]
  end
  M -->|"reads, events, voltage"| NET
  NET -->|backhaul| HES
  HES -->|"reads: daily, interval, billing"| SGG
  SGG --> MDMS
  MDMS -->|VEE| Q{Validated?}
  Q -->|yes| BILL
  Q -->|no| EX["Exception queue"]
  EX -->|"estimate, edit, field visit"| MDMS
  SGG -.->|"commands: reconnect, demand reset"| HES
  M -.->|voltage| M2T["M2T voltage analytics"]
```

## Consumer Portal integration (Accelerated Innovations / SFTP)

How CSU customer and meter data reaches the customer-facing **Consumer Portal** (hosted by
Accelerated Innovations) over **Secure FTP (port 22)**, through firewalls on both sides.

```mermaid
flowchart TB
  CUST["Customers<br/>web & mobile app"]
  subgraph AI["Accelerated Innovations (hosted)"]
    WEB["Consumer Portal<br/>Web Server"]
    API["Consumer Portal<br/>API Server"]
    SFTP["SFTP<br/>(Secure FTP, port 22)"]
    DAQ["Consumer Portal<br/>Data Acquisition Service"]
    PFW["Portal Database<br/>Firewall"]
    PDB[("Consumer Portal<br/>Database Server")]
  end
  subgraph UTIL["CSU (utility)"]
    UFW["Utility Firewall"]
    CIS["CIS System"]
    HE["AMI Head End"]
    CC[("Command Center<br/>(USC / MV-90 exports)")]
  end
  CUST --> WEB
  CUST --> API
  WEB <--> PFW
  API <--> PFW
  PFW <--> PDB
  DAQ --> PDB
  SFTP --> DAQ
  UFW -->|"Secure FTP port 22<br/>CIM / MultiSpeak / files"| SFTP
  CIS -->|"Customer Data<br/>(DB sync file)"| UFW
  HE --> CC
  CC -->|"Daily Reads &amp; Interval Data<br/>(MV-90)"| UFW
```

**Data sources feeding the portal:**

| Source | Data | Format / tool |
|---|---|---|
| CIS System | Customer data (accounts, names, addresses) | DB sync file |
| AMI Head End → Command Center | Daily (scalar) reads | USC / MV-90 |
| AMI Head End → Command Center | Interval data | MV-90 |

> The vendor can support **either a customer-hosted SFTP or an AI-hosted SFTP** endpoint. The
> file-transfer cadence is documented in
> [Meter-Data Lifecycle]({{ '/04-meter-data-lifecycle.html' | relative_url }}).

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
