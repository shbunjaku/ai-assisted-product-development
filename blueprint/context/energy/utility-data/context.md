# Utility Data & Integrations — Context

> @-mention this file in Cursor when working on utility bill ingestion, utility API integrations, or manual data uploads.

---

| Field        | Value |
|--------------|-------|
| Feature      | Utility Data & Integrations |
| Product      | energy |
| Status       | Defining |
| Owner        | |
| Started      | |
| Shipped      | |
| Ticket       | |
| Figma        | |

---

## In one sentence

This feature gets utility data (bills, interval reads, rate schedules) into the platform — automatically where possible, manually where not — so that every energy calculation has accurate, timely source data.

---

## Problem

<!--
e.g. Utility data arrives in different formats, on different schedules, from different sources. Without reliable ingestion, every downstream energy feature (EUI, budget, compliance) is working with stale or incomplete data.
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
| **Utility bill** | Monthly statement from a utility provider. Contains consumption (kWh, therms), demand (kW), cost ($), and billing period. |
| **Interval data** | High-resolution meter reads (15-min or hourly) from AMI smart meters or utility Green Button data. |
| **Green Button** | Industry standard format (XML) for sharing utility interval data. Supported by many US utilities. |
| **Rate schedule / tariff** | The utility's pricing structure: $/kWh, demand charges, time-of-use tiers, taxes. Needed to validate billed costs. |
| **AMI** | Advanced Metering Infrastructure — utility smart meters that provide automated interval reads. |
| | |

**Constraints from the domain:**
<!-- e.g. Bill data arrives 30–60 days after the billing period. Interval data may have gaps. Multiple utilities per building (electric + gas). -->
-

---

## What we are building

<!-- 2–5 bullets. e.g. manual bill upload, utility API connectors, Green Button import, bill parsing, data validation -->
-

## What we are not building (this version)

<!-- e.g. Rate optimization, automated utility account setup, demand response integration -->
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
| Bill has estimated reads (utility didn't do an actual read) | |
| Billing period doesn't align with calendar month | |
| Utility API is temporarily unavailable | |
| Building has multiple utility accounts for the same energy type | |
| | |

---

## Design approach

**Principles:**
<!-- e.g. Show data freshness — when was the last bill received for each meter? Surface gaps, don't hide them. -->
-

**Key screens / states:**

| Screen / state | What the user sees | Figma |
|---------------|-------------------|-------|
| Bill upload / entry | | |
| Utility connections | | |
| Data freshness dashboard | | |
| Bill validation / errors | | |

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
| Meter entities in Building Graph | | See `context/energy/meters/` |
| DataHub ingestion pipeline | | DataHub |
| Utility provider API access | | External / Customer |

---

## Open questions

| Question | Owner | Due | Answer |
|----------|-------|-----|--------|
| Which utility APIs to support first? | | | |
| Manual upload format — CSV, PDF parsing, or structured form? | | | |
| | | | |

---

## Decision log

- **2026-03-10** Feature scoped.
