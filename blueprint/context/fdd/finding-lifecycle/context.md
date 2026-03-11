# Finding Lifecycle — Context

> @-mention this file in Cursor when working on how findings are created, surfaced, actioned, and resolved.

---

| Field        | Value |
|--------------|-------|
| Feature      | Finding Lifecycle |
| Product      | fdd |
| Status       | Defining |
| Owner        | |
| Started      | |
| Shipped      | |
| Ticket       | |
| Figma        | |

---

## In one sentence

This feature gives the Chief Engineer a structured, prioritised view of active findings — what's wrong, where, why it matters, and what to do — so they can act quickly without having to diagnose from raw sensor data.

---

## Problem

Chief Engineers are overwhelmed by alarms. A typical building BMS generates hundreds of alarms per day. Most are noise (nuisance alarms), a few are critical. There is no triage. Engineers miss real problems because they're buried in false positives, or they ignore all alarms because they've stopped trusting them.

The platform has the detection logic (rules engine). The problem is the downstream experience: how a finding is presented, how it's prioritised, how the engineer acknowledges and resolves it. Without a coherent lifecycle, findings are just another alarm system — different data source, same trust problem.

**Who feels it:** Chief Engineer (primary — acts on findings daily). Property Manager (reads summary-level finding data). FDE (configures rules during onboarding).

**How often:** Chief Engineer opens this view daily, sometimes multiple times per shift.

---

## Users

**Chief Engineer**
Senior facilities engineer responsible for day-to-day building operations and equipment health. Opens the platform when something is wrong or starting a shift. Wants to see what needs attention today, why it matters, and what to do about it. Spends most time in fault/finding views. What they care about most: actionability — every finding must tell them what to do, not just what happened. Hates alarms with no context.

**Property Manager** *(secondary — reads summaries)*
Manages operational and financial performance of buildings. Doesn't speak technical — needs findings translated into business terms (cost impact, tenant risk, urgency). Checks building health scores and open issue counts. What they care about most: business impact — dollars at risk, tenants affected.

---

## Domain context

| Term | What it means in this feature |
|------|------------------------------|
| **Finding** | A detected problem — the output of a rule firing. Attached to a graph entity. Has severity, evidence, recommended action, and a lifecycle (open → acknowledged → resolved). |
| **Rule** | The logic that watches signals against thresholds and fires a finding when conditions are met. The rule defines severity and recommended action. |
| **Severity** | How urgently a finding needs attention. Four levels: Critical, High, Medium, Low. Determines visual priority and notification routing. |
| **Evidence** | The timestamped signal values that triggered the rule. Required for engineer trust — shows exactly what the data did and when. |
| **Entity** | The graph node the finding is attached to (e.g. AHU-03, Floor 3). Findings are never free-floating — always attached to a specific thing. |
| **Blast radius** | Other entities downstream of the faulting entity that are affected. Computed by traversing the Building Graph. |
| **Issue** | A group of related findings representing one underlying problem. An engineer acts on the Issue, not on individual findings. |
| **Recommended action** | Specific instruction from the rule: what the engineer should do. Not generic — equipment-specific. |

**Constraints from the domain:**
- A finding is always attached to a graph entity — it cannot be free-floating.
- A finding does not close when acknowledged — only when the underlying condition clears (the rule stops firing).
- Severity is set by the rule, not by the user. Users can suppress or exclude findings, but not change severity on individual instances.
- The same condition persisting should not create duplicate findings — the existing finding is updated, not replaced.
- Evidence must be preserved even after a finding resolves — auditability is required.

---

## What we are building

- A finding list view: all active findings across a building, sorted and filterable by severity, entity type, system, and time open
- Finding detail: full evidence panel (signal chart), entity context, recommended action, blast radius, and cost impact where calculable
- Lifecycle actions: acknowledge, resolve (with resolution note), suppress/exclude
- Issue grouping: related findings surfaced as a single actionable issue with a root cause summary
- Notification delivery: push / email routing by severity and user role

## What we are not building (this version)

- Manual rule creation (configuration module — separate feature)
- Portfolio-level finding aggregation across buildings (phase 2)
- Work order integration triggered by findings (DataHub / CMMS integration — separate feature)
- Finding comments or team collaboration within the platform

---

## How it works

### Happy path

1. Rules engine detects a fault condition on AHU-03 (supply air temperature 7°F above setpoint for 20 min during occupied hours)
2. Finding is created: severity High, entity AHU-03, evidence chart, recommended action "Inspect supply fan VFD, check filters"
3. Finding appears in Chief Engineer's finding list — ranked by severity
4. Engineer opens finding detail: sees evidence chart, blast radius (3 VAV zones affected, 12 tenants), estimated energy waste
5. Engineer acknowledges the finding (confirms they've seen it and are acting)
6. Engineer investigates, fixes the fan VFD issue
7. Condition clears — supply air temperature returns to within setpoint
8. Finding automatically resolves — timestamped
9. Resolution is recorded: condition cleared, duration 4h 22min, energy waste estimated X kWh

### Edge cases

| Situation | Behaviour |
|-----------|-----------|
| Finding condition returns after resolution | New finding is created — not the same finding reopened. Prior finding remains in history. |
| Engineer marks as "won't fix" | Finding is excluded for this entity. Rule continues to run. If condition worsens, a new Critical finding overrides the exclusion. |
| Finding fires on an entity with low data quality | Finding is created with a "low data confidence" flag visible in the detail view. Engineer is warned that evidence may be unreliable. |
| Two rules fire simultaneously on the same entity | Both findings are created separately. Issue grouping logic determines if they represent the same root cause. |
| Entity is offline | Findings dependent on that entity's points are suspended (not created). Offline status surfaces as a separate data quality finding. |

---

## Design approach

**Principles:**
- Severity drives everything. Critical findings are impossible to miss. Low findings are visible but don't compete for attention.
- Actionability first. Every finding detail page leads with the recommended action — not the evidence. Evidence is secondary (supporting, not leading).
- Context is built-in. Engineer should understand the impact (blast radius, cost) without navigating away.
- Noise is the enemy. Any pattern that creates nuisance findings (many openings/closings per day on same entity) must be surfaced as a rule quality issue, not accepted as normal.

**Key screens / states:**

| Screen / state | What the user sees | Figma |
|---------------|-------------------|-------|
| Finding list | Grouped by severity. Critical at top. Each row: entity name, finding title, time open, severity badge. Filterable by system, floor, time. | |
| Issue view | Group of related findings under one issue header. Root cause summary. "Act on issue" CTA. | |
| Finding detail | Header: entity, severity, time open. Section 1: Recommended action. Section 2: Evidence chart (signal over time with condition window highlighted). Section 3: Blast radius map. Section 4: Cost/energy impact. Section 5: Lifecycle history. | |
| Empty state | No active findings = explicit "Building healthy" message with last rule evaluation timestamp | |
| Excluded findings | Separate tab or filter — not hidden, but deprioritised | |

**Open design questions:**

| Question | Owner | Due |
|----------|-------|-----|
| Should blast radius be a graph visualisation or a flat list? | Design | |
| How do we prevent "acknowledged" state from becoming a graveyard of ignored findings? | Product | |
| What does the Property Manager view look like — same page filtered, or a separate summary surface? | Product | |

---

## Technical approach

**Architecture touchpoints:**

| Component | How it's involved |
|-----------|------------------|
| Building Graph | Blast radius calculation — traverse entity relationships from the faulting entity |
| Timeseries Engine | Evidence data — the signal values shown in the evidence chart |
| Rules Engine | Creates, updates, and resolves findings as conditions change |
| Library | Provides recommended actions and severity for each rule |
| API Layer | Serves finding list, finding detail, lifecycle actions |
| Frontend | Finding list, issue grouping, detail view |

**Key decisions:**
- Findings are immutable records — lifecycle state changes (acknowledge, resolve) are separate events, not overwrites
- Issue grouping runs as a periodic job, not real-time — acceptable latency is 5 minutes
- Blast radius is computed at finding creation time and cached — not recomputed on every view
- Evidence chart data is fetched from the timeseries engine on demand (not pre-computed)

**ADRs:**
- None created yet

---

## Dependencies

| Dependency | Status | Owner |
|------------|--------|-------|
| Rules engine — finding creation | Exists | Platform |
| Building Graph — blast radius traversal API | Exists | Platform |
| Notification service | Not started | Engineering |
| Issue grouping logic | Not started | Engineering |

---

## Open questions

| Question | Owner | Due | Answer |
|----------|-------|-----|--------|
| What is the right issue grouping algorithm — time proximity? same entity? same rule? | Engineering + Domain | | |
| How long should resolved findings be visible in the active list before moving to history? | Product | | |
| What is the escalation path if a Critical finding is not acknowledged within X hours? | Product | | |

---

## Decision log

- **2026-03-06** Feature scoped. Focus on single-building finding lifecycle. Portfolio aggregation and CMMS integration are explicitly out of scope for this version.
