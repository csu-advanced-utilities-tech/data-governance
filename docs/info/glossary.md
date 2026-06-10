---
layout: default
title: Glossary
subtitle: Technical and data terms used across this site, in plain English.
---

> Skim this whenever a word is unfamiliar. Definitions are intentionally simple, not formal.

## Tech & GitHub terms

| Term | Plain-English meaning |
|---|---|
| **GitHub** | A website where teams store files (especially text and code), track every change, and collaborate. It hosts both of our sites. |
| **Organization** | A shared GitHub account for a team. Ours is `csu-advanced-utilities-tech`; our repositories live inside it. |
| **Repository ("repo")** | A project folder on GitHub. We have two: `data-governance` (this Hub) and `command-center-data-catalog` (the Catalog). |
| **Git** | The underlying technology that records the history of changes to files. GitHub is built on top of it. |
| **Commit** | A single saved change, with a short note describing it. Like a labeled checkpoint you can always return to. |
| **Branch** | A safe, separate copy of the files where you can make changes without affecting the live version. |
| **`main`** | The primary branch — what the live website is published from. |
| **Pull request (PR)** | A proposal to merge your branch's changes into `main`, so they can be reviewed before going live. |
| **Merge** | Combining approved changes into `main` (which then publishes them). |
| **Issue** | A note on GitHub describing a task, bug, or suggestion — a way to ask for a change without editing files. |
| **Clone** | Downloading a copy of a repository to your own computer (only needed for advanced editing). |
| **Markdown** | A simple way to format text using symbols (e.g. `**bold**`, `## Heading`). The Hub pages are written in it. |
| **CSV** | A plain spreadsheet file (comma-separated values). The Catalog's table/column descriptions are stored this way. |
| **Python** | A programming language. A small Python program turns the Catalog's CSVs into web pages. |
| **Jekyll** | A tool that automatically turns the Hub's Markdown files into web pages. |
| **GitHub Pages** | GitHub's free service that publishes our files as a live public website. |
| **Static site** | A website made of pre-built pages (no database, very fast and cheap to host). Both our sites are static. |
| **Build / pipeline** | The automated step that turns source files (Markdown or CSV) into the finished web pages. |

## Data & utility terms

| Term | Plain-English meaning |
|---|---|
| **Data governance** | The agreed rules and roles for keeping data accurate, secure, well-understood, and trusted. The purpose of this Hub. |
| **AMI** | Advanced Metering Infrastructure — the smart meters, network, and systems that collect usage data automatically. |
| **Command Center** | The **head-end system (HES)** for our AMI program — Landis+Gyr's control software that collects, commands, and stores meter/endpoint data. It is hosted by the vendor and is our system of record. The Data Catalog documents its database. |
| **Landis+Gyr** | Our AMI vendor (Landis+Gyr Technology, Inc.). Under a 2019 Master Agreement they provide the meters, network, the Command Center head-end, and managed services. |
| **Head-End System (HES)** | The central software that talks to all the meters — collects reads, sends commands, and hands data downstream. For us, the HES is Command Center. |
| **Gridstream** | Landis+Gyr's AMI communications network (the radio-frequency mesh, often using the Wi-SUN standard) that carries data between meters and the head-end. |
| **Wi-SUN** | An open wireless standard for utility field-area networks; the radio protocol the AMI mesh uses to backhaul meter data. |
| **Endpoint / Meter / Collector** | The field devices: meters measure usage, endpoints communicate, collectors/routers/gateways relay the data back to the head-end. |
| **MDMS (Meter Data Management System)** | CSU's system that stores and manages validated meter reads and produces billing determinants; it receives data from the head-end via the Smart Grid Gateway. |
| **Smart Grid Gateway** | CSU's integration layer that receives meter data from the Command Center head-end and feeds it into CSU systems (e.g. the MDMS). |
| **SLA (Service Level Agreement)** | A contracted performance commitment (e.g. "99.5% of billing reads delivered on time"), often with service credits if missed. Our SLAs live in the Master Agreement. |
| **CORA** | Colorado Open Records Act — the public-records law CSU is subject to, which shapes how confidential contract and customer information is handled. |
| **Metadata** | "Data about the data" — e.g. a table's purpose, or what a column means. The Catalog is essentially organized metadata. |
| **Data dictionary** | A reference listing every table and column and what it means. That's the Catalog. |
| **Data domain** | A grouping of related data by business area (e.g. "Endpoints & Meters", "Plans & Schedules"). |
| **VEE** | Validation, Estimation, Editing — the standard process for checking and correcting meter reads before they're used. |
| **M2T (Meter-to-Transformer)** | A CSU project that uses AMI meter voltage data to build voltage "signature" shapes, then correlation and clustering to group meters by likely transformer — and compares the result to the GIS map to confirm or recommend corrections to which transformer each meter is mapped to. |
| **GIS** | Geographic Information System — the mapping system that records the electric network's physical layout, including which meters connect to which transformers. M2T checks this map against AMI data. |
| **Lineage** | The traceable path data takes from its source through transformations to where it's used. |
| **Data steward** | The person responsible day-to-day for a domain's data quality and definitions. |
| **Data owner** | The person accountable for a domain's data and who approves access to it. |
| **RACI** | A chart of who is **R**esponsible, **A**ccountable, **C**onsulted, and **I**nformed for each activity. |
| **KPI** | Key Performance Indicator — a metric we track to measure data health or program success. |
| **Consumer Portal (Accelerated Innovations)** | The customer-facing web/mobile portal, hosted by vendor Accelerated Innovations, where customers view their energy usage; fed CSU data over SFTP. |
| **SFTP** | Secure File Transfer Protocol (port 22) — the encrypted channel that moves customer and meter files from CSU to the Consumer Portal. |
| **CIS (Customer Information System)** | CSU's system of customer accounts and billing info; the source of customer data (names, addresses) shared with the portal. |
| **MV-90** | An interval meter-data collection/translation system used to extract interval reads from Command Center into files. |
| **CMEP** | Common Meter Export Protocol — a standard file format for exporting (AMR) interval meter data. |
| **MultiSpeak / CIM** | Common utility data-exchange standards (MultiSpeak; Common Information Model) used as file/message formats between systems. |
| **Scalar vs. interval read** | A scalar (register) read is a cumulative total (e.g., total kWh); an interval read is usage within a fixed window (e.g., 15 minutes). |
| **MMM** | CSU's daily meter-monitoring exception report — coded rules (NVM, STL, DIV, etc.) that flag meters with data or device problems for investigation. See the [Data-Quality Framework]({{ '/08-data-quality-framework.html' | relative_url }}). *(Acronym to be confirmed.)* |
| **SPID** | An endpoint's collector/SPU association; "has SPID" means the meter is assigned to a collector and on the network. *(Confirm exact meaning.)* |
| **WOP (In Work Order Process)** | Flag on an MMM rule indicating it is active in production and can generate a work order. |
| **dbsync** | The CIS DB-sync file — customer/meter data synced from the Customer Information System; some MMM rules cross-check it. |
| **DIV** | The MMM theft-detection rule: flags disconnected meters still drawing load-side voltage, or "no-usage" meters that suddenly read — replacing the older ECO rule. |

Missing a term? Add it via [How to Contribute]({{ '/info/contributing.html' | relative_url }}) or open an Issue.
