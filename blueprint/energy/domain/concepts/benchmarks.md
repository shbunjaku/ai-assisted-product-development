# Energy Benchmarking

| Field        | Value |
|--------------|-------|
| Author       | |
| Last updated | |
| Scope        | energy |

## What it is

Energy benchmarking is the process of comparing a building's energy performance (typically EUI) against a reference standard — either a code baseline, a peer group median, or the building's own historical performance. It answers the question: "Is this building performing well, relative to what we'd expect?"

Benchmarking turns a raw number (EUI = 95) into a judgment (EUI = 95, target is 70, this building is 36% above baseline — failing).

## Why it matters

Without benchmarking, energy data is descriptive but not actionable. "This building uses 2 million kBtu/year" gives no basis for action. "This building's EUI is 95 vs. its ASHRAE baseline of 70 — it should be performing 26% better" creates urgency and a quantifiable goal.

Benchmarking also drives regulatory compliance. Laws like NYC LL97, DC BEPS, and California Title 24 set mandatory performance thresholds expressed as EUI or carbon intensity targets. Buildings that miss them face fines.

## How it works

### Reference standards

| Standard | What it is | Used for |
|----------|-----------|---------|
| **ASHRAE 90.1** | Code-minimum energy performance by building type and climate zone | Regulatory baseline; compliance for new construction |
| **ENERGY STAR** | EPA peer-group percentile ranking (1–100 score) | Voluntary certification; mandatory disclosure in some cities |
| **CBECS** | Commercial Buildings Energy Consumption Survey — US average by building type | Peer comparison; broad industry context |
| **Portfolio baseline** | Owner's own portfolio average by building type | Internal benchmarking; relative performance ranking |
| **Historical baseline** | Building's own performance in a defined baseline year | Year-over-year performance tracking |

### How the platform benchmarks

1. Building type and climate zone are set in the Building Profile
2. The platform selects the appropriate reference EUI from the library (ASHRAE, CBECS, ENERGY STAR median)
3. EUI is computed from meter data (see `energy/domain/concepts/eui.md`)
4. EUI is compared to reference → percentage above/below is computed
5. A KPI is created: EUI = 95, target = 70, status = FAILING, gap = 36%

### Benchmark KPI judgment

| Status | Condition |
|--------|----------|
| **Passing** | EUI ≤ target |
| **Failing** | EUI > target |
| **Improving** | EUI is failing but trending downward over the last 12 months |
| **Degrading** | EUI was passing but is trending upward over the last 6 months |

### Regulatory benchmarking

Some jurisdictions require annual benchmarking reports submitted to a government portal (NYC: Energy Star Portfolio Manager; DC: District Department of Energy and Environment). The platform generates the data needed for these submissions.

Key regulations:

| Regulation | Jurisdiction | Type | Metric |
|-----------|-------------|------|--------|
| **LL97** | New York City | Carbon emissions cap | kg CO₂e/sq ft (penalties for exceedance) |
| **BEPS** | Washington DC | Energy performance standard | Site EUI limit by building type |
| **Title 24** | California | Building code | EUI for new construction and major renovations |
| **ENERGY STAR disclosure** | Multiple cities | Mandatory disclosure | ENERGY STAR score |

## Key terms

| Term | Definition |
|------|-----------|
| **Baseline year** | The reference year against which current performance is measured. |
| **Peer group** | Buildings of the same type and climate zone used for ENERGY STAR percentile ranking. |
| **EUI target** | The performance level a building should achieve, derived from the applicable benchmark standard. |
| **ENERGY STAR score** | 1–100 percentile score vs. peer group. ≥75 qualifies for certification. |
| **Compliance gap** | The gap between current EUI and the regulatory target. Drives fine calculation for LL97. |

## What it is not

- Not a ranking of absolute energy use. A hospital with EUI 250 may be ENERGY STAR certified; an office with EUI 100 may be failing. Context (building type, climate, occupancy) is everything.
- Not a substitute for knowing why performance is what it is. Benchmarking identifies the gap; FDD and Energy optimization identify the causes.

## Related concepts

- `energy/domain/concepts/eui.md` — the metric being benchmarked
- `energy/domain/concepts/carbon.md` — carbon benchmarking for LL97 and similar regulations
- `core/domain/concepts/signals.md` — KPIs represent benchmark comparisons
