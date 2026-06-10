---
layout: default
title: Data Governance Hub
subtitle: Governance, lineage, quality, and stewardship for the Command Center meter-data program.
---

This hub is the single source of truth for how the Command Center meter-data program is
governed — who owns what, how data flows and is validated, and how we measure success.
The live **Data Dictionary** is maintained in the
[command-center-data-catalog]({{ "https://csu-advanced-utilities-tech.github.io/command-center-data-catalog/index.html" }}) site and linked from the navigation. The **Code Catalog** is a growing library of reusable SQL queries for that database.

<div class="cards">

  <a class="card" href="{{ '/01-executive-summary.html' | relative_url }}">
    <div class="card-num">01</div><h3>Executive Summary</h3>
    <p>The one-page "why this matters" for leadership.</p>
  </a>

  <a class="card" href="{{ '/02-scope-and-domains.html' | relative_url }}">
    <div class="card-num">02</div><h3>Scope &amp; Data Domains</h3>
    <p>What's in and out of scope, and the data domains we govern.</p>
  </a>

  <a class="card" href="{{ '/03-governance-operating-model.html' | relative_url }}">
    <div class="card-num">03</div><h3>Governance Operating Model</h3>
    <p>Decision rights, forums, and how governance runs day to day.</p>
  </a>

  <a class="card" href="{{ '/04-meter-data-lifecycle.html' | relative_url }}">
    <div class="card-num">04</div><h3>Meter-Data Lifecycle</h3>
    <p>Collection → ingest → VEE → storage → billing → archive.</p>
  </a>

  <a class="card" href="{{ '/05-ot-it-landscape.html' | relative_url }}">
    <div class="card-num">05</div><h3>OT/IT Landscape</h3>
    <p>Current-state inventory of systems and integration points.</p>
  </a>

  <a class="card" href="https://csu-advanced-utilities-tech.github.io/command-center-data-catalog/index.html" target="_blank" rel="noopener">
    <div class="card-num">06 ↗</div><h3>Data Dictionary</h3>
    <p>Live table &amp; column catalog (separate repo).</p>
  </a>

  <a class="card" href="{{ '/07-code-catalog.html' | relative_url }}">
    <div class="card-num">07</div><h3>Code Catalog</h3>
    <p>Reusable SQL queries and snippets for the Command Center database.</p>
  </a>

  <a class="card" href="{{ '/08-data-quality-framework.html' | relative_url }}">
    <div class="card-num">08</div><h3>Data-Quality Framework</h3>
    <p>VEE rules, the MMM monitoring register, M2T validation, and quality dimensions.</p>
  </a>

  <a class="card" href="{{ '/09-security-compliance.html' | relative_url }}">
    <div class="card-num">09</div><h3>Security &amp; Compliance</h3>
    <p>PII handling, access control, and auditability.</p>
  </a>

  <a class="card" href="{{ '/10-architecture-lineage.html' | relative_url }}">
    <div class="card-num">10</div><h3>Architecture &amp; Lineage</h3>
    <p>Text-based architecture and data-lineage diagrams.</p>
  </a>

  <a class="card" href="{{ '/11-implementation-roadmap.html' | relative_url }}">
    <div class="card-num">11</div><h3>Implementation Roadmap</h3>
    <p>Phased plan for the current data initiative.</p>
  </a>

  <a class="card" href="{{ '/12-stewardship-raci.html' | relative_url }}">
    <div class="card-num">12</div><h3>Stewardship &amp; RACI</h3>
    <p>Roles, responsibilities, and the RACI matrix.</p>
  </a>

  <a class="card" href="{{ '/13-kpis.html' | relative_url }}">
    <div class="card-num">13</div><h3>KPIs &amp; Success Metrics</h3>
    <p>How we measure data health and program success.</p>
  </a>

</div>

## Status legend

Each section page carries a status badge:
<span class="badge placeholder">Placeholder</span>
<span class="badge draft">Draft</span>
<span class="badge review">In review</span>
<span class="badge approved">Approved</span>

## New here? Start with the Information Portal

The **[Information Portal]({{ '/info/index.html' | relative_url }})** explains — in plain
language — how this site is built and hosted, [how to contribute]({{ '/info/contributing.html' | relative_url }})
(no coding required), an [FAQ]({{ '/info/faq.html' | relative_url }}), a
[Glossary]({{ '/info/glossary.html' | relative_url }}) of terms, and the
[Resources &amp; References]({{ '/info/resources.html' | relative_url }}) library behind this hub.
It's the best place to start if you're new to GitHub.
