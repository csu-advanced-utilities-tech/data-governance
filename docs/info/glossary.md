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
| **Command Center** | The system that is our system of record for AMI meter, endpoint, and reading data. |
| **Endpoint / Meter / Collector** | The field devices: meters measure usage, endpoints communicate, collectors relay the data back to the Command Center. |
| **Metadata** | "Data about the data" — e.g. a table's purpose, or what a column means. The Catalog is essentially organized metadata. |
| **Data dictionary** | A reference listing every table and column and what it means. That's the Catalog. |
| **Data domain** | A grouping of related data by business area (e.g. "Endpoints & Meters", "Plans & Schedules"). |
| **VEE** | Validation, Estimation, Editing — the standard process for checking and correcting meter reads before they're used. |
| **M2T** | A specific CSU meter-data rule/stipulation, documented in the Data-Quality Framework section *(definition to be confirmed)*. |
| **Lineage** | The traceable path data takes from its source through transformations to where it's used. |
| **Data steward** | The person responsible day-to-day for a domain's data quality and definitions. |
| **Data owner** | The person accountable for a domain's data and who approves access to it. |
| **RACI** | A chart of who is **R**esponsible, **A**ccountable, **C**onsulted, and **I**nformed for each activity. |
| **KPI** | Key Performance Indicator — a metric we track to measure data health or program success. |

Missing a term? Add it via [How to Contribute]({{ '/info/contributing.html' | relative_url }}) or open an Issue.
