# Energy Use Intensity (EUI)

| Field        | Value |
|--------------|-------|
| Author       | |
| Last updated | |
| Scope        | energy |

## What it is

Energy Use Intensity (EUI) is the primary metric for measuring a building's energy performance. It expresses a building's total annual energy consumption per unit of floor area:

```
EUI = Total annual energy (kBtu) / Gross floor area (sq ft)
```

A lower EUI means a more energy-efficient building. EUI makes energy performance comparable across buildings of different sizes.

## Why it matters

EUI is the universal language of building energy performance. It is used by:
- **Energy managers** to benchmark a building against its peers and track performance over time
- **Regulators** to set mandatory performance standards (LL97 in NYC, BEPS in DC, Title 24 in California)
- **Asset managers** to compare portfolio performance and prioritize capital investment
- **ENERGY STAR** to certify high-performing buildings

Without EUI, "this building uses 2 million kBtu per year" is meaningless. With EUI, "this building's EUI is 95, vs. an ASHRAE baseline of 70 for its type" is immediately actionable.

## How it works

### Data sources

EUI is computed from all energy consumed by the building:
- **Electricity** — from utility bills or interval meter data
- **Natural gas** — from utility bills or gas meters
- **Steam / district heating/cooling** — from utility bills with appropriate conversion factors
- **Other fuels** — fuel oil, propane (converted to kBtu)

All sources are converted to kBtu using standard conversion factors (1 kWh = 3.412 kBtu, 1 therm = 100 kBtu, etc.).

### Site EUI vs. Source EUI

| Type | What it measures |
|------|-----------------|
| **Site EUI** | Energy consumed at the building. What appears on utility bills. |
| **Source EUI** | Energy consumed to generate and deliver energy to the building, including grid losses. Used for ENERGY STAR ratings. |

The platform computes Site EUI from meter data. Source EUI requires source-site ratios from EPA (updated annually).

### Weather normalization

Raw EUI fluctuates with weather. A cold winter drives up heating energy; a hot summer drives up cooling energy. Weather-normalized EUI removes this variability so that performance changes reflect building improvements, not weather.

Normalization uses **Heating Degree Days (HDD)** and **Cooling Degree Days (CDD)** from local weather data.

### Benchmarking

EUI is compared against reference values:
- **ASHRAE 90.1 baseline** — code-minimum performance by building type and climate zone
- **ENERGY STAR median** — the median EUI for a building's peer group (requires ENERGY STAR Portfolio Manager)
- **Portfolio baseline** — the average EUI across the owner's own portfolio (internal benchmark)
- **Historical baseline** — the building's own EUI in a prior baseline year

## Key terms

| Term | Definition |
|------|-----------|
| **kBtu/sq ft/yr** | Standard unit for EUI in the US. Thousand British Thermal Units per square foot per year. |
| **kWh/m²/yr** | Standard unit for EUI in metric countries. |
| **Weather normalization** | Adjusting EUI to remove the effect of weather variability, enabling year-over-year and peer comparisons. |
| **HDD / CDD** | Heating Degree Days / Cooling Degree Days. Weather metrics used for normalization. |
| **Source EUI** | EUI adjusted for grid transmission losses. Used by ENERGY STAR. |
| **Site EUI** | EUI measured at the building boundary (from utility bills and meters). |
| **ENERGY STAR score** | 1–100 score for a building based on source EUI percentile vs. peers. Score ≥ 75 qualifies for ENERGY STAR certification. |

## What it is not

- Not a complete picture of energy performance alone. EUI doesn't tell you *why* energy is high. It tells you the outcome; FDD tells you the causes.
- Not the same as total energy consumption. A 1,000 sq ft office using 50 kBtu/sq ft uses less total energy than a 100,000 sq ft warehouse at the same EUI.
- Not standardized for all building types. A hospital has a naturally high EUI due to 24/7 operations; it shouldn't be compared against an office building.

## Examples

| Building type | Typical EUI range (kBtu/sq ft/yr) | ENERGY STAR 75th percentile |
|--------------|----------------------------------|----------------------------|
| Office | 50–120 | ~50 |
| Retail | 60–150 | ~60 |
| Hospital | 200–400 | ~250 |
| Warehouse | 20–60 | ~25 |
| K-12 School | 50–120 | ~55 |

## Related concepts

- `energy/domain/concepts/metering-hierarchy.md` — how energy data is collected for EUI computation
- `energy/domain/concepts/benchmarks.md` — how EUI is compared to standards
- `core/domain/concepts/signals.md` — Metrics and KPIs that represent EUI
