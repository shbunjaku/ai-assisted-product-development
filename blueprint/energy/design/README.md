# Energy — Design

> Owned by Design.

---

## Before designing

1. Read the PRD in `energy/product/prd/`
2. Read the domain concept in `energy/domain/concepts/`
3. Check `core/design/design-system.md` — especially the KPIWidget and TimeseriesChart components

---

## Flows

Mirror the module structure from `energy/product/prd/`. Copy `_templates/flow.md`.

```
energy/design/flows/
├── metering/
├── consumption/
├── cost/
├── carbon/
└── optimization/
```

| Flow | Module | Status | PRD | Last updated |
|------|--------|--------|-----|-------------|
| | | | | |

**Suggested flows to create:**
- `consumption/energy-overview-flow.md` — Energy Manager reviewing portfolio performance
- `cost/bill-upload-flow.md` — uploading and reconciling a utility bill
- `consumption/benchmark-comparison-flow.md` — comparing a building to peers

---

## Specs

Mirror the module structure. Copy `_templates/design-spec.md`.

```
energy/design/specs/
├── metering/
├── consumption/
├── cost/
├── carbon/
└── optimization/
```

| Screen | Module | Status | Flow | Figma | Last updated |
|--------|--------|--------|------|-------|-------------|
| | | | | | |

**Suggested specs to create:**
- `consumption/energy-dashboard.md` — portfolio and building energy KPIs
- `metering/meter-hierarchy.md` — visual meter tree with health status
- `cost/bill-detail.md` — utility bill breakdown and reconciliation view
- `consumption/eui-benchmark.md` — EUI scorecard with peer comparison
- `carbon/carbon-tracker.md` — Scope 1/2/3 with compliance status
