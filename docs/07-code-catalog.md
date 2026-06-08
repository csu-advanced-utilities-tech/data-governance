---
layout: default
title: 7. Code Catalog
subtitle: Reusable SQL queries and snippets for the Command Center database.
---

<span class="badge draft">Draft</span>

> A shared library of **good, reusable queries** against the Command Center (`centralservices`)
> database — so a query someone has already perfected can be reused instead of rebuilt. Pair it
> with the [Data Dictionary](https://csu-advanced-utilities-tech.github.io/command-center-data-catalog/index.html),
> which explains the tables and columns these queries use.
>
> Each query below expands to show the SQL. To add one, see
> [Contributing a query](#contributing-a-query).

## Reference codes (cheat sheet)

Handy IDs used in the filters below (confirm against the Data Dictionary):

| Field | Common values |
|---|---|
| `METERS.metertypeid` | 1 = electric · 2 = water · 3 = gas · 4 = unspecified · 5 = router |
| `STATUSCODES.statuscodeid` | 8 = Normal · 1 = Inventory · 6 = Lost (also Discovered) |
| `PACKETTYPES.packettypeid` | 8 = Published · 9 = Gap Analysis |
| `DATADEFINITIONS.datadefinitionid` | 1 = kWh · 613 = kWh Rcvd · 1072 = kW3 |
| `GROUPTYPES.grouptypeid` | 70 = Collector · 34 = RF Virtual Addressing · 13 = Scheduled Reads · 15 = User Defined |

> **Naming convention:** `centralservices.TABLENAME.column` (schema . table . field).

---

## Query library

<details>
<summary>Meters &amp; Endpoints — status, model, service location</summary>

Returns one row per endpoint with meter number, status, model, service location, and DCW version.

```sql
SELECT METERS.meterno,                       -- the meter's name (written on the meter)
       STATUSCODES.name        AS status,    -- Normal, Discovered, Lost, etc.
       ENDPOINTS.serialnumber,               -- comms module LAN ID
       ENDPOINTS.laststatuschanged,
       ENDPOINTS.lastbillableread,
       ENDPOINTMODELS.name     AS model,
       SERVICELOCATIONS.servloc,
       RFENDPOINTPROPERTIES.dcwversion
FROM centralservices.ENDPOINTS
JOIN      centralservices.METERS              ON ENDPOINTS.meterid    = METERS.meterid
JOIN      centralservices.STATUSCODES         ON ENDPOINTS.statuscodeid = STATUSCODES.statuscodeid
LEFT JOIN centralservices.BILLINGCYCLES       ON BILLINGCYCLES.billingcycleid = METERS.billingcycleid
LEFT JOIN centralservices.SERVICELOCATIONS    ON METERS.servicelocationid = SERVICELOCATIONS.servicelocationid
LEFT JOIN centralservices.ENDPOINTMODELS      ON ENDPOINTS.hwmodelid  = ENDPOINTMODELS.endpointmodelid
JOIN      centralservices.RFENDPOINTPROPERTIES ON ENDPOINTS.endpointid = RFENDPOINTPROPERTIES.endpointid;
```
</details>

<details>
<summary>Meters &amp; Collectors — with latitude &amp; longitude</summary>

Returns each meter, its collector, status, last billable read, and GPS coordinates.

```sql
SELECT METERS.meterno,
       COLLECTORS.name        AS collector_name,
       STATUSCODES.name       AS status,
       ENDPOINTS.lastbillableread,
       SERVICELOCATIONS.servloc,
       GPSLOCATIONS.latitude,
       GPSLOCATIONS.longitude
FROM centralservices.ENDPOINTS
JOIN      centralservices.METERS           ON ENDPOINTS.meterid = METERS.meterid
LEFT JOIN centralservices.COLLECTORS       ON ENDPOINTS.spuid   = COLLECTORS.collectorid
JOIN      centralservices.STATUSCODES      ON ENDPOINTS.statuscodeid = STATUSCODES.statuscodeid
LEFT JOIN centralservices.SERVICELOCATIONS ON SERVICELOCATIONS.servicelocationid = METERS.servicelocationid
LEFT JOIN centralservices.GPSLOCATIONS     ON SERVICELOCATIONS.gpslocationid = GPSLOCATIONS.gpslocationid;
```
</details>

<details>
<summary>Self-read count — days with good reads per meter (last 10 days)</summary>

Counts the number of days each Normal meter returned a published kWh self-read in the last 10 days.

```sql
SELECT METERS.meterno AS meter,
       COUNT(IDREADINGLOGS.readingdate) AS count_reads
FROM centralservices.METERS
JOIN centralservices.ENDPOINTS     ON ENDPOINTS.meterid = METERS.meterid
JOIN centralservices.IDREADINGLOGS ON METERS.meterid    = IDREADINGLOGS.meterid
WHERE IDREADINGLOGS.readingdate > TRUNC(SYSDATE) - 10
  AND ENDPOINTS.statuscodeid     = 8   -- Normal
  AND IDREADINGLOGS.packettypeid = 8   -- Published
  AND IDREADINGLOGS.datadefinitionid = 1   -- kWh
GROUP BY METERS.meterno
HAVING COUNT(IDREADINGLOGS.readingdate) >= 5
ORDER BY METERS.meterno;
```
</details>

<details>
<summary>Interval data — count of intervals per meter (yesterday)</summary>

Counts interval (load-profile) reads per meter for the previous day. 96 = a full day of 15-minute kWh.

```sql
SELECT METERS.meterno,
       PACKETTYPES.name AS packet_type,
       COUNT(INTERVALDATA.intervalstartdate) AS intvcount
FROM centralservices.METERS
LEFT JOIN centralservices.INTERVALDATA ON INTERVALDATA.meterid = METERS.meterid
JOIN      centralservices.ENDPOINTS    ON ENDPOINTS.meterid    = METERS.meterid
JOIN      centralservices.PACKETTYPES  ON INTERVALDATA.packettypeid = PACKETTYPES.packettypeid
WHERE INTERVALDATA.intervalstartdate >= TRUNC(SYSDATE) - 1
  AND INTERVALDATA.intervalstartdate <  TRUNC(SYSDATE)
  AND INTERVALDATA.datadefinitionid  = 1        -- kWh
  AND INTERVALDATA.packettypeid IN (8, 9)       -- Published, Gap Analysis
GROUP BY METERS.meterno, PACKETTYPES.name;
```

_Note: the original L+G example joined ENDPOINTS on `endpointid = meterid`; corrected here to `ENDPOINTS.meterid = METERS.meterid`._
</details>

<details>
<summary>Commands &amp; response — what was sent and how it responded</summary>

Returns commands issued, who issued them, when sent/completed, and the response status.

```sql
SELECT COMMANDSSENT.meterno,
       COMMANDTYPES.name        AS command,
       COMMANDSSENT.sent,
       COMMANDSSENT.completed,
       STATUSCODES.name         AS response_status,
       USERS.loginuser,
       COMMANDSTATUSCODES.displayname AS sent_status,
       COMMANDTYPES.priority
FROM centralservices.COMMANDLOG
JOIN      centralservices.COMMANDRESPONSE    ON COMMANDLOG.commandlogid = COMMANDRESPONSE.commandlogid
LEFT JOIN centralservices.STATUSCODES        ON STATUSCODES.statuscodeid = COMMANDRESPONSE.statuscodeid
JOIN      centralservices.USERS              ON COMMANDLOG.issuedby = USERS.userid
JOIN      centralservices.COMMANDTYPES       ON COMMANDTYPES.commandtypeid = COMMANDLOG.commandtypeid
LEFT JOIN centralservices.COMMANDSSENT       ON COMMANDSSENT.commandlogid = COMMANDLOG.commandlogid
LEFT JOIN centralservices.COMMANDSTATUSCODES ON COMMANDSTATUSCODES.commandstatuscodeid = COMMANDSSENT.commandstatuscodeid;
```
</details>

<details>
<summary>Events &amp; errors — event summary (last 2 days)</summary>

Summarizes events by type over the last two days, with first/last occurrence and distinct meters affected.

```sql
SELECT EVENTLOG.eventtypeid AS type,
       EVENTTYPES.name      AS event,
       MAX(METERS.meterno)  AS example,
       COUNT(DISTINCT METERS.meterno) AS distinct_meters,
       COUNT(*)             AS total_events,
       MIN(TRUNC(EVENTLOG.eventdate)) AS first_occurred,
       MAX(TRUNC(EVENTLOG.eventdate)) AS last_occurred
FROM centralservices.EVENTLOG
JOIN centralservices.ENDPOINTS  ON EVENTLOG.endpointid = ENDPOINTS.endpointid
JOIN centralservices.EVENTTYPES ON EVENTLOG.eventtypeid = EVENTTYPES.eventtypeid
JOIN centralservices.METERS     ON ENDPOINTS.meterid    = METERS.meterid
WHERE EVENTLOG.eventdate >= TRUNC(SYSDATE) - 2
GROUP BY EVENTLOG.eventtypeid, EVENTTYPES.name
ORDER BY COUNT(*) DESC;
```
</details>

<details>
<summary>Meter configuration — program, firmware, model, interval length</summary>

Returns the program, firmware, model, and interval length for electric meters.

```sql
SELECT METERS.meterno,
       ENDPOINTMODELS.name AS model,
       METERS.firmwareversion,
       METERCONFIGURATION.intervallength,
       METERS.meterpgmcd
FROM centralservices.ENDPOINTS
JOIN      centralservices.METERS         ON ENDPOINTS.meterid = METERS.meterid
LEFT JOIN centralservices.ENDPOINTMODELS ON ENDPOINTS.hwmodelid = ENDPOINTMODELS.endpointmodelid
LEFT JOIN centralservices.ENDPOINTMETERCONFIGURATION ON ENDPOINTS.endpointid = ENDPOINTMETERCONFIGURATION.endpointid
LEFT JOIN centralservices.METERCONFIGURATION ON ENDPOINTMETERCONFIGURATION.meterconfigurationid = METERCONFIGURATION.meterconfigurationid
WHERE METERS.metertypeid = 1;   -- electric
```
</details>

> **Performance tip:** `COMMANDLOG`, `EVENTLOG`, `IDREADINGLOGS`, and `INTERVALDATA` are very large
> and fast-changing — always filter by a date range (e.g. `TRUNC(SYSDATE) - n`) and avoid unbounded scans.

---

## Contributing a query

Add your query to this page (edit `docs/07-code-catalog.md`) using the same pattern:

```text
<details>
<summary>Short title — what it returns</summary>

One or two sentences on what it does and any parameters.

​```sql
SELECT ...
​```
</details>
```

Include: a clear title, what it returns, any parameters/filters to adjust, and call out tables
that are large or sensitive. See [How to Contribute]({{ '/info/contributing.html' | relative_url }}).

---

### Source references
- **Landis+Gyr — Command Center Database** presentation (example queries &amp; schema).
- [Data Dictionary](https://csu-advanced-utilities-tech.github.io/command-center-data-catalog/index.html) — table &amp; column definitions.
