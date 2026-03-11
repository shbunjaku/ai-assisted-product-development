# Metering Hierarchy

| Field        | Value |
|--------------|-------|
| Author       | |
| Last updated | |
| Scope        | energy |

## What it is

The metering hierarchy is the structured tree of meters in a building, from the utility feed at the top to sub-meters that measure individual systems, tenants, or equipment. It defines how energy flows through the building and how consumption is allocated, reconciled, and attributed.

Understanding the metering hierarchy is a prerequisite for any energy analysis. Without it, you cannot know whether data is complete, whether costs are correctly allocated, or whether sub-meter readings are consistent with the utility bill.

## Why it matters

Three critical use cases depend on the metering hierarchy:

1. **EUI computation** — total building energy comes from the utility meter(s) at the top of the hierarchy
2. **Tenant cost allocation** — tenant energy costs require sub-meters that measure tenant spaces specifically
3. **Bill reconciliation** — sub-meter sum should equal (or approximately equal) the utility meter; large gaps indicate metering gaps or losses

## How it works

### Hierarchy structure

```
Utility meter (main)
├── Whole-building electricity meter
│   ├── HVAC sub-meter (chillers, AHUs, cooling towers)
│   │   ├── Chiller sub-meter
│   │   └── AHU sub-meter
│   ├── Lighting sub-meter
│   ├── Tenant A sub-meter
│   └── Tenant B sub-meter
├── Gas meter (main)
│   ├── Boiler sub-meter
│   └── Kitchen/lab gas sub-meter
└── Steam / district energy meter
```

In the Building Graph, each meter is an entity (`Meter` type) with edges defining its position in the hierarchy:
- `submeters` → child meters that roll up into this one
- `measures` → the entity (space, system, equipment) this meter tracks
- `billsTo` → the tenant or cost centre this meter's consumption is allocated to

### Meter types

| Meter type | Energy type | Common data source |
|------------|------------|-------------------|
| **Utility meter** | Electric, gas, steam, water | Utility bill + AMI interval data |
| **Building sub-meter** | Electric | BMS-connected panel meter |
| **System sub-meter** | Electric (HVAC, lighting) | Dedicated submeter on electrical panel |
| **Tenant sub-meter** | Electric | Landlord-installed submeter per tenant |
| **Equipment meter** | Electric | CT-clamp or dedicated meter on equipment |
| **Virtual meter** | Any | Calculated from other meters or points — no physical device |

### Bill reconciliation

Bill reconciliation compares the utility meter (top of hierarchy) against the sum of sub-meters below it:

```
Utility meter reading = Sum of sub-meters + Unmetered losses
```

If the gap between utility meter and sub-meter sum is > 5–10%, there is likely:
- A missing sub-meter (a circuit not being measured)
- A metering error (faulty sensor, wrong multiplier)
- Distribution losses (normal, but should be quantified)

The platform surfaces this gap as a data quality finding.

### Interval data vs. bill data

| Type | Resolution | Use |
|------|-----------|-----|
| **Bill data** | Monthly | EUI computation, tenant billing, regulatory reporting |
| **Interval data** | 15-min or hourly | Demand analysis, peak detection, real-time efficiency |

When both are available, interval data is preferred. Bill data is used when interval data isn't available for a period (utility outage, meter offline).

## Key terms

| Term | Definition |
|------|-----------|
| **AMI (Advanced Metering Infrastructure)** | Utility smart meters that provide interval (15-min or hourly) data automatically. |
| **Sub-meter** | Any meter below the utility meter. Measures a portion of the building's energy. |
| **Virtual meter** | A calculated meter derived from other meters or points. Not a physical device. |
| **Meter gap** | The difference between a parent meter reading and the sum of its sub-meters. Indicates unmeasured energy. |
| **Cost allocation** | Dividing total energy cost among tenants, cost centres, or systems based on sub-meter readings or allocation formulas. |
| **Reconciliation** | Comparing utility bill to internal meter data to catch billing errors or metering gaps. |

## What it is not

- Not the same as the Building Graph entity hierarchy. The metering hierarchy is a sub-graph of meter entities and their energy flow relationships. It does not map to Site → Building → Floor → Space directly.
- Not static. Tenants move in and out. Equipment is added. The metering hierarchy must be maintained as the building changes.

## Related concepts

- `energy/domain/concepts/eui.md` — EUI is computed from the top of the hierarchy
- `core/domain/concepts/entities.md` — Meter is an entity type in the Building Graph
- `core/domain/concepts/graph.md` — meter relationships (`submeters`, `billsTo`, `measures`)
