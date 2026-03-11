# The Signal Spectrum

**Scope:** core — every product builds on top of this.

## What it is

Every piece of data in the platform travels through four levels of increasing intelligence. Understanding this spectrum is the foundation for all product, design, and engineering work.

```
Point ──────────► Virtual Point ──────────► Metric ──────────► KPI
raw sensor         calculated from            aggregated,        metric +
value              other signals              any entity,        target +
                                              batch              judgment

"44.2°F"           "0.72 kW/ton"             "EUI = 95"        "EUI = 95,
                                                                 target 85,
                                                                 FAILING"

No opinion          Light opinion             Medium opinion     Strong opinion
```

## The four levels

| Level | What it is | Scope | Computed how | Opinion |
|-------|-----------|-------|-------------|---------|
| **Point** | Raw sensor reading from a physical device | Device-bound | Not computed — ingested | None |
| **Virtual Point** | Calculated signal from other points | Device-bound | Real-time formula | Light |
| **Metric** | Aggregated signal from any data source | Any entity | Batch computation | Medium |
| **KPI** | Metric + target + judgment | Any entity | Compare to library benchmark | Strong |

## Why this matters for product and design

- **Points** — users configure, map, and verify these during BMS onboarding. They don't see point values in operational views; they see VPs and Metrics.
- **Virtual Points** — appear on equipment detail pages as "calculated signals." They fill gaps when sensors don't exist.
- **Metrics** — power dashboards, portfolio views, and trend analysis. Any entity can have Metrics.
- **KPIs** — the platform's opinion. They answer "is this good or bad?" and drive alerts, findings, and recommendations.

## Key distinction: VP vs Metric

Both are computed signals. The difference is scope:
- **VP** uses only points from the same or nearby device → enables real-time streaming
- **Metric** can pull from anything → requires batch computation

Design implication: VPs feel like live readings. Metrics feel like reports or scorecards.

## Related concepts
- core/domain/concepts/entities.md — what entities carry signals
- core/domain/concepts/graph.md — how signals connect through the graph
- fdd/domain/concepts/rules.md — how rules consume signals to produce findings
