# User Personas

> All personas live here. Products reference this file — they don't define their own personas.
> To add a persona: open a PR with research justification.

---

## Chief Engineer
**Role:** Senior facilities engineer responsible for day-to-day building operations and equipment health.
**Goal:** Keep equipment running, catch problems before they cause failures, minimize emergency repairs.
**Pain points:**
- Too many alarms with no context — doesn't know which ones actually matter
- Fault diagnosis is manual and time-consuming
- No visibility into whether preventive maintenance is actually preventing failures

**How they use the platform:**
Opens the platform when something is wrong or when starting a shift. Wants to see what needs attention today, why it matters, and what to do about it. Spends most time in fault/finding views and equipment detail pages.

**What they care about most:** Actionability — every alert must tell them what to do, not just what happened.

---

## Property Manager
**Role:** Manages the operational and financial performance of one or more buildings on behalf of the owner.
**Goal:** Minimize costs, maximize tenant satisfaction, avoid surprises, produce reports for ownership.
**Pain points:**
- Doesn't speak technical — needs building performance translated into business terms
- Reactive to tenant complaints instead of proactive
- Hard to show ownership that they're doing a good job

**How they use the platform:**
Primarily a consumer of summaries and reports. Checks building health scores, energy costs, and open issues. Uses the platform to prepare for owner meetings and respond to tenant escalations.

**What they care about most:** Business impact — dollars saved, tenants satisfied, risks avoided.

---

## Energy Manager
**Role:** Responsible for energy performance, sustainability targets, and regulatory compliance across a portfolio.
**Goal:** Hit energy and carbon reduction targets, ensure benchmarking compliance, identify optimization opportunities.
**Pain points:**
- Energy data is siloed across different systems and utilities
- Hard to prove ROI on energy projects
- Regulatory deadlines (LL97, Title 24, BEPS) are complex and high-stakes

**How they use the platform:**
Portfolio-level views. Compares buildings against benchmarks. Tracks EUI trends. Monitors utility bills. Prepares compliance reports.

**What they care about most:** Accuracy and auditability — energy data that can be defended to regulators and ownership.

---

## Facility Director / Asset Manager
**Role:** Owns the capital plan for a portfolio — deciding what to replace, when, and at what cost.
**Goal:** Maximize asset value, optimize CapEx timing, reduce risk of critical failures.
**Pain points:**
- CapEx decisions are made on gut feel and vendor recommendations, not data
- Hard to prioritize which equipment to replace vs. repair
- No visibility into aging risk across the portfolio

**How they use the platform:**
Infrequent but high-stakes. Reviews equipment health scores, aging risk, and maintenance cost trends. Uses findings to build the CapEx budget justification.

**What they care about most:** Portfolio-level risk — which buildings and systems are most exposed.

---

## Tenant
**Role:** Occupant of a leased space — individual or facilities contact for a company.
**Goal:** Comfortable, functional workspace with fast response to issues.
**Pain points:**
- Comfort complaints feel like they disappear into a black hole
- No visibility into whether anything is being done
- HVAC is either too hot, too cold, or inconsistent

**How they use the platform:**
Minimal — may submit comfort requests or view their space's comfort status. Not expected to understand equipment or energy.

**What they care about most:** Speed of response and feeling heard.

---

## FDE (Facilities Data Engineer / Onboarding Engineer)
**Role:** Technical specialist who connects buildings to the platform — maps points, classifies equipment, builds the digital twin.
**Goal:** Get a building fully connected and producing intelligence as fast as possible.
**Pain points:**
- Point naming is inconsistent across BMS vendors
- Hard to know when the twin is "done enough" to go live
- Mapping thousands of points manually is slow and error-prone

**How they use the platform:**
Deep in BMS onboarding tools — device discovery, point mapping, equipment classification, twin completeness checking.

**What they care about most:** Efficiency — tools that reduce manual work and surface gaps clearly.
