# Energy — Energy Management

> Everything about the Energy product lives here.
> Concepts, PRDs, flows, specs, and engineering decisions — all in one place.

---

## What this product does

Energy gives operators, property managers, and energy managers visibility into energy consumption, efficiency, cost, and carbon across equipment, systems, spaces, and buildings. It reconciles meter data against utility bills, benchmarks performance against standards, and surfaces optimization opportunities.

---

## Folder structure

```
energy/
├── domain/
│   ├── concepts/        ← Energy-specific domain knowledge (EUI, meters, benchmarks, carbon)
│   └── README.md
├── product/
│   ├── prd/             ← one file per feature
│   └── README.md
├── design/
│   ├── flows/           ← user flows for Energy features
│   ├── specs/           ← screen-level design specs
│   └── README.md
└── engineering/
    ├── adr/             ← Energy-specific architectural decisions
    ├── api/             ← Energy API documentation
    └── README.md
```

---

## Key domain concepts
→ `energy/domain/concepts/`

Understand what EUI is, how metering hierarchy works, and how utility bills reconcile against meter data before writing any PRD or spec.

## Key personas
→ `core/product/personas.md`

Primary: **Energy Manager** (tracks benchmarks, compliance, optimization), **Property Manager** (cost summaries).
Secondary: **Asset Manager** (ROI on energy projects), **Chief Engineer** (equipment-level efficiency).

## Core dependency
→ `core/domain/concepts/signals.md` — Energy uses Metrics and KPIs heavily (EUI, carbon intensity, efficiency scores).
→ `core/domain/concepts/entities.md` — Metrics attach to buildings, systems, equipment, and spaces.
