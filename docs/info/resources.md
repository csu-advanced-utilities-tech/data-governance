---
layout: default
title: Resources & References
subtitle: The source documents behind this hub — a short summary of each, with a link to read more.
---

> Each entry gives a **two-line summary** so you get the gist without leaving the page. Use
> **Open document →** to read the full source, or expand **"Fuller summary"** for more detail.
> Section pages across the hub cite these by short name in their *Source references* block.

## External guidance

<div class="resource">
  <h3>EPA — AMI System Requirements Specification &amp; Guidance</h3>
  <p class="meta">U.S. EPA · 2021 · PDF (industry guidance)</p>
  <p>Federal guidance on specifying and operating Advanced Metering Infrastructure, including
  expectations for meter-data handling and the Validation, Estimation &amp; Editing (VEE) process.
  We use it as the baseline for our lifecycle and data-quality sections.</p>
  <p><a href="https://www.epa.gov/sites/default/files/2021-03/documents/srs_ami_guidance_20210223_508_complete.pdf" target="_blank" rel="noopener"><strong>Open document →</strong></a></p>
  <details>
    <summary>Fuller summary &amp; where it's used</summary>
    <p>Informs: <a href="{{ '/04-meter-data-lifecycle.html' | relative_url }}">Meter-Data Lifecycle</a>,
    <a href="{{ '/08-data-quality-framework.html' | relative_url }}">Data-Quality Framework</a>,
    <a href="{{ '/02-scope-and-domains.html' | relative_url }}">Scope &amp; Domains</a>. Key takeaways: define
    VEE rules explicitly; treat meter reads as billing-grade only after validation; document data
    handling end-to-end.</p>
  </details>
</div>

<div class="resource">
  <h3>DOE — Leveraging AMI Networks and Data</h3>
  <p class="meta">U.S. Department of Energy · 2019 · PDF</p>
  <p>How utilities can extract operational value from AMI networks and data — including using
  <strong>voltage data</strong> for grid insight, which connects directly to our Meter-to-Transformer
  (M2T) work. We use it for KPIs and lifecycle value.</p>
  <p><a href="https://www.energy.gov/" target="_blank" rel="noopener"><strong>Open document →</strong></a>
  <span class="muted">(the original link was truncated — replace with the full energy.gov URL when available)</span></p>
  <details>
    <summary>Fuller summary &amp; where it's used</summary>
    <p>Informs: <a href="{{ '/13-kpis.html' | relative_url }}">KPIs &amp; Metrics</a>,
    <a href="{{ '/04-meter-data-lifecycle.html' | relative_url }}">Meter-Data Lifecycle</a>, and the
    voltage-analytics rationale behind <a href="{{ '/08-data-quality-framework.html' | relative_url }}">M2T</a>.</p>
  </details>
</div>

<div class="resource">
  <h3>NREL — AMI Data Management</h3>
  <p class="meta">National Renewable Energy Laboratory · TP fy22osti/83877 · PDF</p>
  <p>A reference architecture and set of practices for managing AMI data at scale — head-end,
  storage, and meter-data management. We use it for our architecture and domain decomposition.</p>
  <p><a href="https://docs.nrel.gov/docs/fy22osti/83877.pdf" target="_blank" rel="noopener"><strong>Open document →</strong></a></p>
  <details>
    <summary>Fuller summary &amp; where it's used</summary>
    <p>Informs: <a href="{{ '/05-ot-it-landscape.html' | relative_url }}">OT/IT Landscape</a>,
    <a href="{{ '/10-architecture-lineage.html' | relative_url }}">Architecture &amp; Lineage</a>,
    <a href="{{ '/02-scope-and-domains.html' | relative_url }}">Scope &amp; Domains</a>.</p>
  </details>
</div>

<div class="resource">
  <h3>National Grid — AMI Grid-Edge Computing Report</h3>
  <p class="meta">Niagara Mohawk d/b/a National Grid · NY PSC Docket 20-M-0082 · March 2022 · PDF</p>
  <p>A utility's plan for <strong>next-generation AMI with grid-edge computing</strong> — analytics run
  on the meter itself. We hold it as an industry <em>benchmark</em> for advanced AMI use cases; it is
  <strong>not</strong> a description of CSU's current Landis+Gyr system.</p>
  <p><a href="{{ '/assets/pdfs/AMI-grid-edge-computing-report.pdf' | relative_url }}"><strong>Open document →</strong></a>
  <span class="muted">(add the PDF at <code>docs/assets/pdfs/AMI-grid-edge-computing-report.pdf</code> to enable this link)</span></p>
  <details>
    <summary>Fuller summary &amp; why it matters to us</summary>
    <p>The report describes meters that run sandboxed apps (an "Edge Intelligence Card") alongside an
    isolated metrology engine, enabling use cases such as <strong>Grid Mapping / Locational Awareness</strong>
    (deriving each meter's transformer/feeder — directly relevant to
    <a href="{{ '/08-data-quality-framework.html' | relative_url }}">M2T</a>), <strong>Intelligent Voltage
    Monitoring</strong>, distributed outage detection, and theft/high-impedance detection. It frames
    cybersecurity around the <strong>NIST Cybersecurity Framework</strong> (Identify / Protect / Detect /
    Respond &amp; Recover) and discusses platform governance and customer/third-party data access
    (Green Button, HAN). Useful as a forward-looking comparison for our roadmap and for the analytics
    ambitions behind M2T and voltage monitoring.</p>
  </details>
</div>

## Internal — authoritative source documents

<div class="resource confidential">
  <h3>Landis+Gyr — Command Center Data Extracts (white paper) <span class="badge draft">Confidential</span></h3>
  <p class="meta">Landis+Gyr · 2018 · vendor white paper (proprietary &amp; confidential)</p>
  <p>Explains how reads are extracted from Command Center — Conventional (once-a-day register / EMED),
  Interval (once-a-day load profile / CMEP), and the Incremental Daily / Interval / Periodic extracts —
  plus formats, scheduling, gap reconciliation, and on-demand reads.</p>
  <p><strong>⚠️ Confidential — do not publish.</strong> Vendor-proprietary; not linked or stored on this
  public site. The operational concepts are summarized in
  <a href="{{ '/04-meter-data-lifecycle.html' | relative_url }}">Meter-Data Lifecycle</a>.</p>
</div>

<div class="resource confidential">
  <h3>CSU ↔ Landis+Gyr — AMI Master Agreement <span class="badge draft">Confidential</span></h3>
  <p class="meta">Colorado Springs Utilities &amp; Landis+Gyr Technology, Inc. · executed July 10, 2019 · 20-year term</p>
  <p>The contract governing our AMI program. It is the <strong>authoritative internal source</strong> for the
  vendor relationship, system architecture (the <strong>Command Center</strong> head-end system), data-delivery
  SLAs, security obligations, and the vendor/utility responsibility split (RACI) used throughout this hub.</p>
  <p><strong>⚠️ Confidential — do not publish.</strong> This document is bound by the contract's
  confidentiality terms and is <strong>not</strong> linked or stored on this public site. It is held in CSU's
  internal contract repository (CSU Procurement &amp; Contract Services).</p>
  <details>
    <summary>What it informs across the hub</summary>
    <p><a href="{{ '/05-ot-it-landscape.html' | relative_url }}">OT/IT Landscape</a> (systems &amp; network),
    <a href="{{ '/04-meter-data-lifecycle.html' | relative_url }}">Meter-Data Lifecycle</a> (delivery timing),
    <a href="{{ '/09-security-compliance.html' | relative_url }}">Security &amp; Compliance</a> (CORA, riders, data residency),
    <a href="{{ '/12-stewardship-raci.html' | relative_url }}">Stewardship &amp; RACI</a> (vendor vs. CSU split),
    <a href="{{ '/13-kpis.html' | relative_url }}">KPIs</a> (contracted SLA targets),
    <a href="{{ '/11-implementation-roadmap.html' | relative_url }}">Roadmap</a> (term, zone deployment).</p>
  </details>
</div>

---

_To add a publicly-shareable PDF to this page, drop it in `docs/assets/pdfs/` and link to it with
`{% raw %}{{ '/assets/pdfs/your-file.pdf' | relative_url }}{% endraw %}`. Never add confidential documents — this repo is public._
