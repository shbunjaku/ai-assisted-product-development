# Energy Budget — Context

> @-mention this file in Cursor when working on energy budgeting.

---

| Field        | Value |
|--------------|-------|
| Feature      | Energy Budget |
| Product      | energy |
| Status       | Defining |
| Owner        | |
| Started      | |
| Shipped      | |
| Ticket       | |
| Figma        | |

---

## In one sentence

This feature lets building operators set annual energy consumption and cost budgets, then track actuals vs. budget — so they can catch overruns before the money is spent.

---

## Problem

<!--
e.g. Energy costs are 20–30% of building OpEx but teams only discover budget overruns after the year ends.
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
| **Energy budget** | Planned consumption (kBtu) and/or cost ($) target for a building, set annually, allocated by month |
| **Budget variance** | Actual minus budgeted for a period. Positive = over budget. |
| | |

**Constraints from the domain:**
<!-- e.g. Budget must cover all energy types. Monthly allocation is seasonal, not annual ÷ 12. -->
-

---

## What we are building

<!-- 2–5 bullets -->
-

## What we are not building (this version)

<!-- e.g. Tenant-level budgets, rate optimization, automated budget generation -->
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
| Utility bill not yet received for a month | |
| Utility rate changes mid-year | |
| | |

---

## Design approach

**Principles:**
-

**Key screens / states:**

| Screen / state | What the user sees | Figma |
|---------------|-------------------|-------|
| Budget setup | | |
| Monthly tracking | | |
| Portfolio summary | | |

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
| Meter data (electricity + gas) | | DataHub |
| Utility bill ingestion | | See `context/energy/utility-data/` |
| Weather data for variance context | | See `context/energy/weather-normalization/` |

---

## Open questions

| Question | Owner | Due | Answer |
|----------|-------|-----|--------|
| | | | |

---

## Decision log

- **2026-03-10** Feature scoped.
