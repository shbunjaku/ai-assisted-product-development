# Meters & Metering Hierarchy — Context

> @-mention this file in Cursor when working on meter management, hierarchy, virtual meters, or bill reconciliation.

---

| Field        | Value |
|--------------|-------|
| Feature      | Meters & Metering Hierarchy |
| Product      | energy |
| Status       | Defining |
| Owner        | |
| Started      | |
| Shipped      | |
| Ticket       | |
| Figma        | |

---

## In one sentence

This feature lets building teams define and manage their metering hierarchy — from utility feeds down to sub-meters and virtual meters — so that consumption can be correctly attributed and reconciled at every level.

---

## Problem

<!--
e.g. Meter hierarchies live in spreadsheets. Without a modeled hierarchy, EUI double-counts, tenant billing has no data, and nobody knows what's unmeasured.
Who feels it, how often, what breaks without this?
-->

---

## Users

<!--
Paste relevant persona summaries inline from core/product/personas.md.
-->

---

## Domain context

| Term | What it means in this feature |
|------|------------------------------|
| **Meter** | Entity in the Building Graph that records energy consumption. Physical or virtual. |
| **Metering hierarchy** | Parent-child tree of meters. Utility meter at top, sub-meters below. See `energy/domain/concepts/metering-hierarchy.md`. |
| **Virtual meter** | Calculated meter with no physical device. Formula references other meters. |
| **Bill reconciliation** | Comparing utility meter reading to sum of sub-meters. Gap = unmeasured energy. |
| | |

**Constraints from the domain:**
<!-- e.g. Hierarchy must be a tree (no cycles). Virtual meters can't have circular references. Decommissioned meters are archived, not deleted. -->
-

---

## What we are building

<!-- 2–5 bullets. e.g. meter CRUD, hierarchy builder, virtual meter formulas, reconciliation view, completeness indicator -->
-

## What we are not building (this version)

<!-- e.g. Automatic meter discovery, tenant billing, demand analysis -->
-

---

## How it works

### Happy path

1.
2.
3.

### Edge cases

| Situation | Behaviour |
|-----------|-----------|
| Building has no sub-meters | |
| Meter is replaced (new hardware, same circuit) | |
| Virtual meter references an offline meter | |
| | |

---

## Design approach

**Principles:**
<!-- e.g. Visual hierarchy — scannable tree. Gaps are visible, not hidden. -->
-

**Key screens / states:**

| Screen / state | What the user sees | Figma |
|---------------|-------------------|-------|
| Hierarchy tree | | |
| Add / edit meter | | |
| Virtual meter editor | | |
| Reconciliation panel | | |

**Open design questions:**
| Question | Owner | Due |
|----------|-------|-----|
| | | |

---

## Technical approach

**Architecture touchpoints:**

| Component | How it's involved |
|-----------|------------------|
| Building Graph | |
| Timeseries Engine | |
| Rules Engine | |
| Library | |
| API Layer | |
| Frontend | |

**Key decisions:**
-

**ADRs:**
-

---

## Dependencies

| Dependency | Status | Owner |
|------------|--------|-------|
| Building entity in graph | | BMS |
| Meter points mapped from BMS | | BMS onboarding |
| Utility bill ingestion | | See `context/energy/utility-data/` |
| Interval meter data | | DataHub |

---

## Open questions

| Question | Owner | Due | Answer |
|----------|-------|-----|--------|
| | | | |

---

## Decision log

- **2026-03-10** Feature scoped.
