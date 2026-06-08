---
layout: default
title: 7. Code Catalog
subtitle: A reference for status, command, event, and error codes — a separate upcoming effort.
---

<span class="badge placeholder">Placeholder — separate effort</span>

> The Code Catalog is **planned as its own initiative** and is not yet built. This page is a
> placeholder so the section has a home in the navigation.

## What it will cover

A human-readable reference for the coded values used throughout the Command Center, so a
number in a log maps to a clear meaning. Likely sources (from the
[Data Dictionary](https://csu-advanced-utilities-tech.github.io/command-center-data-catalog/index.html)):

- `STATUSCODES`, `ENDPOINTSTATUSCODEHISTORY`
- `COMMANDTYPES`, `COMMANDSTATUSCODES`
- `EVENTTYPES`, `ERRORTYPES`
- `PACKETTYPES`, `PLANTYPES`, `GROUPTYPES`, `INTERVALTYPES`

## Why it's separate

The Data Dictionary documents *tables and columns*; the Code Catalog documents the
*enumerated values* inside key code/type columns. It needs its own extract and review pass,
so it's tracked as a distinct workstream rather than bundled with the dictionary.

_TODO: define scope, source of the code values, and owner once this effort kicks off._
