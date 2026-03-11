# LL97 Compliance Tracking — Context

> @-mention this file in Cursor when working on anything related to NYC Local Law 97 compliance — carbon limits, fine calculations, and compliance reporting.

---

| Field        | Value |
|--------------|-------|
| Feature      | LL97 Compliance Tracking |
| Product      | energy |
| Status       | Defining |
| Owner        | |
| Started      | |
| Shipped      | |
| Ticket       | |
| Figma        | |

---

## In one sentence

This feature gives Energy Managers and Property Managers a real-time view of their NYC buildings' LL97 compliance status — current carbon emissions vs. their annual limit — so they can act before the compliance deadline rather than discover a fine after it.

---

## Problem

NYC Local Law 97 sets mandatory annual carbon emissions limits for buildings over 25,000 sq ft. Buildings that exceed their limit face fines of $268 per metric ton CO₂e over the limit — which for a large non-compliant building can easily reach $500k–$2M+ per year.

The compliance cycle runs annually. Penalties are calculated after the year ends. By the time a building owner discovers they're non-compliant, it's too late to act.

Property and Energy managers currently have no way to see their in-year compliance trajectory without manually pulling meter data, applying emission factors, and running Excel models. The data is available on the platform — the platform just doesn't surface it in compliance terms.

**Who feels it:** Energy Manager (owns the compliance task). Property Manager (faces the financial consequence). Asset Manager (models financial risk across portfolio).

**When:** Annual compliance cycle. Compliance year = calendar year. Fines assessed after June 30 of the following year.

---

## Users

**Energy Manager**
Responsible for energy performance, sustainability targets, and regulatory compliance across a portfolio. Tracks EUI trends. Monitors utility bills. Prepares compliance reports. What they care about most: accuracy and auditability — carbon data that can be defended to regulators and ownership. Uses the platform for portfolio-level views and regulatory prep.

**Property Manager** *(secondary — sees financial impact)*
Manages operational and financial performance of one or more buildings. Doesn't speak technical — needs carbon data translated into financial exposure. Checks building compliance status in the context of "what does this cost me?" What they care about most: business impact — dollars at risk.

**Asset Manager / Facility Director** *(secondary — portfolio risk)*
Owns the capital plan. Reviews LL97 compliance across a portfolio to understand which buildings need retrofits and what the CapEx case is. What they care about most: portfolio-level risk and ROI on compliance investments.

---

## Domain context

| Term | What it means in this feature |
|------|------------------------------|
| **LL97** | NYC Local Law 97. Sets annual carbon emissions limits for NYC buildings >25,000 sq ft. Penalties apply for exceedance starting compliance year 2024. |
| **Carbon intensity** | CO₂e emissions per sq ft per year (kg CO₂e/sq ft/yr). The unit LL97 uses for limits. |
| **Emission factor** | Multiplier converting energy consumption to CO₂e. For electricity: varies by grid (NYC uses Consolidated Edison grid factor). For gas: 53.06 kg CO₂/MMBtu (EPA). |
| **Scope 1** | Direct on-site combustion emissions — natural gas boilers, emergency generators. |
| **Scope 2** | Indirect electricity emissions — purchased electricity from the grid. |
| **CO₂e limit** | LL97-specified annual carbon limit for the building, calculated as: limit (kg CO₂e/sq ft/yr) × building sq ft. Tightens in phases (2024–2029, 2030–2034, 2035+). |
| **Compliance gap** | Current annual emissions vs. the limit. Positive gap = building is over limit. Negative = headroom. |
| **Projected fine** | If compliance gap > 0 at year end: gap (metric tons CO₂e) × $268/mt. |
| **REC** | Renewable Energy Certificate. Purchasing RECs reduces Scope 2 reported emissions. Tracked separately from meter data. |
| **Metric** | Batch-computed, entity-bound signal. Emissions and EUI are Metrics attached to the building entity. |
| **KPI** | Metric + target + judgment. LL97 compliance = a KPI: actual emissions vs. limit = passing/failing/improving/degrading. |

**Constraints from the domain:**
- LL97 only applies to NYC buildings. The feature must be scoped to buildings where LL97 is flagged as applicable.
- Emission factors must be updated annually when EPA and Con Edison publish new values — using stale factors produces incorrect compliance calculations.
- Compliance year = calendar year. The platform must track cumulative year-to-date emissions and project the annual total.
- REC purchases reduce Scope 2 reporting. RECs must be tracked separately from meter data — they are an input to compliance calculation, not a meter reading.
- The limit tightens in 2030 and 2035. The platform must show the current limit and future limits so owners can plan retrofits.

---

## What we are building

- A per-building LL97 compliance dashboard: year-to-date carbon emissions vs. annual limit, with projected year-end total
- Fine calculator: if on current trajectory, estimated annual fine
- Emissions breakdown: Scope 1 (gas) and Scope 2 (electricity) shown separately, with the emission factors applied
- REC tracking: input for REC purchases, showing how they reduce Scope 2 reported emissions
- Phase timeline: current limit, 2030 limit, 2035 limit — so owners can see when their building becomes non-compliant under future rules
- Portfolio summary: all NYC buildings ranked by compliance gap / fine exposure

## What we are not building (this version)

- Compliance reporting submission (Energy Star Portfolio Manager integration — separate feature)
- Optimization recommendations for closing the compliance gap (separate feature)
- Other regulatory frameworks (BEPS, Title 24, ENERGY STAR — separate features sharing the same data model)
- Embodied carbon (Scope 3 — not required by LL97)

---

## How it works

### Happy path

1. Energy Manager opens the LL97 compliance view for a portfolio of NYC buildings
2. Platform shows each building's: YTD carbon emissions, annual limit, gap (surplus or deficit), and projected year-end fine (if any)
3. Manager clicks into a building with a projected fine
4. Building detail shows: Scope 1 breakdown (gas consumption × emission factor), Scope 2 breakdown (electricity × grid emission factor), REC purchases applied, net position
5. Manager sees the phase timeline: "You're compliant in 2024–2029. Under 2030 limits, you're projected to exceed by X metric tons ($Y fine). Under 2035 limits, by Z metric tons ($W fine)."
6. Manager exports the compliance summary for reporting to ownership

### Edge cases

| Situation | Behaviour |
|-----------|-----------|
| Meter data gap (utility bill not yet uploaded) | Compliance calculation is shown as partial with a warning: "Missing meter data for [period] — figures are estimated." |
| Emission factors not yet updated for current year | Calculation uses prior year factors with a visible warning: "2025 emission factors not yet published — using 2024 values." |
| Building is LL97-exempt (under 25,000 sq ft) | Building is excluded from the LL97 view with a note explaining exemption. |
| REC purchase entered manually | Scope 2 emissions are reduced by REC quantity × emission factor. Shown as a distinct line item in the breakdown. |
| Building is over limit despite RECs | Fine is calculated on the net position after RECs, per LL97 rules. |

---

## Design approach

**Principles:**
- Financial first. The primary number is the fine exposure — not the raw emissions figure. Translate every number into dollars.
- Time-aware. Show YTD actuals + projected year-end on one view. Don't make the user calculate the projection.
- Phase visibility. Owners make CapEx decisions 2–3 years out. The 2030 and 2035 limits must be visible now.
- Auditability. Every number must be traceable: which meters, which emission factors, which REC entries. Energy Managers must be able to defend the figure.

**Key screens / states:**

| Screen / state | What the user sees | Figma |
|---------------|-------------------|-------|
| Portfolio compliance summary | Table: building name, current year compliance status (KPI badge), YTD gap, projected fine. Sortable by fine exposure. | |
| Building compliance detail | Header: status badge, YTD emissions vs. limit bar, projected fine. Sections: Scope 1 breakdown, Scope 2 breakdown, RECs, net position. Phase timeline chart. | |
| Phase timeline | Line chart: actual emissions trend + limit lines for 2024–2029, 2030–2034, 2035+. Shows when building crosses into non-compliance. | |
| Emission factor panel | Shows which factors are applied, their source, and the year they were published. FMI link to EPA/Con Edison. | |
| REC entry | Input form: purchase date, quantity (MWh), certificate ID, reduction applied to Scope 2. | |
| Missing data warning | Inline alert when meter data has gaps. Shows which period and estimated impact on accuracy. | |

**Open design questions:**

| Question | Owner | Due |
|----------|-------|-----|
| Should projected year-end be a linear projection or weather-normalized? | Product + Domain | |
| How do we handle buildings that straddle two LL97 compliance phases mid-year? | Domain | |
| Is the portfolio view by fine exposure only, or should it also rank by "gap as % of limit"? | Product | |

---

## Technical approach

**Architecture touchpoints:**

| Component | How it's involved |
|-----------|------------------|
| Building Graph | Buildings and meters are entities. Carbon is a Metric attached to the Building entity. |
| Timeseries Engine | Source of electricity and gas consumption data (interval meter readings) |
| Rules Engine | Not directly involved in calculation — but KPI evaluation (passing/failing) uses the Rules Engine |
| Library | Stores LL97 limits by building type, phase, and emission factors by source |
| API Layer | Serves compliance dashboard data: YTD emissions, limit, fine projection, breakdown |
| Frontend | Compliance dashboard, phase timeline chart, REC input |

**Key decisions:**
- Emissions are computed as a Metric (batch, entity-bound) on the Building entity — not a real-time signal
- Emission factors live in the Library alongside fault signatures — they are versioned and updated annually
- REC purchases are stored as manual entries (not meter readings) — they reduce Scope 2 reported emissions in the compliance calculation
- Projections use a 12-month rolling average adjusted for YTD actuals — not a naive linear projection

**ADRs:**
- TBD: How to handle annual emission factor updates without retroactively changing historical compliance calculations

---

## Dependencies

| Dependency | Status | Owner |
|------------|--------|-------|
| Meter data in timeseries store (electricity + gas) | Required | DataHub |
| Building entity with sq ft and LL97 flag | Required | BMS |
| Emission factors in Library | Not yet in Library | Platform / Domain |
| LL97 limits by building type in Library | Not yet in Library | Platform / Domain |

---

## Open questions

| Question | Owner | Due | Answer |
|----------|-------|-----|--------|
| Who is responsible for updating emission factors annually? | Platform / Domain | | |
| Do we need to support LL97 exemptions beyond sq ft (e.g. affordable housing exemptions)? | Product + Domain | | |
| Is the fine projection a best-effort estimate or a certified compliance calculation? (Legal implications) | Product + Legal | | |
| How do we handle buildings acquired mid-year — partial year compliance? | Domain | | |

---

## Decision log

- **2026-03-06** Feature scoped. LL97 only for this version. BEPS, Title 24, and ENERGY STAR share the same Metrics infrastructure but are separate features. Optimization recommendations are explicitly out of scope.
