# Energy — Product

> Owned by Product.
> Features are organized into modules. One PRD per feature, inside its module folder.

---

## Before writing a PRD

1. Read the relevant concept in `energy/domain/concepts/`
2. Check `core/product/personas.md`
3. Decide which module the feature belongs to (see below)
4. Copy `_templates/prd.md` → `energy/product/prd/[module]/[feature-name].md`

---

## Modules

```
energy/product/prd/
├── metering/           ← meter hierarchy, assignment, health, sub-metering
├── consumption/        ← energy use, EUI, benchmarking, trends
├── cost/               ← utility bills, rate structures, cost allocation, budgets
├── carbon/             ← Scope 1/2/3, carbon intensity, regulatory compliance
└── optimization/       ← savings opportunities, project ROI, demand response
```

**When to add a new module:** When a new logical area of the product emerges. Add a folder and document it here.

---

## PRD index

### metering/
| Feature | Status | Owner | Last updated |
|---------|--------|-------|-------------|
| | | | |

### consumption/
| Feature | Status | Owner | Last updated |
|---------|--------|-------|-------------|
| | | | |

### cost/
| Feature | Status | Owner | Last updated |
|---------|--------|-------|-------------|
| | | | |

### carbon/
| Feature | Status | Owner | Last updated |
|---------|--------|-------|-------------|
| | | | |

### optimization/
| Feature | Status | Owner | Last updated |
|---------|--------|-------|-------------|
| | | | |

---

## Suggested features to define

| Module | Feature | Why it matters |
|--------|---------|---------------|
| `metering/` | Meter hierarchy | Visual tree of meters showing what each measures |
| `metering/` | Meter health monitoring | Data freshness, gaps, and reconciliation gaps |
| `consumption/` | EUI benchmarking | Building EUI vs. ASHRAE/EnergyStar by type and climate |
| `consumption/` | Energy trends | Consumption over time with weather normalization |
| `cost/` | Utility bill reconciliation | Bill vs. meter data to catch billing errors |
| `cost/` | Tenant cost allocation | Energy cost broken down per tenant by allocation method |
| `carbon/` | Carbon tracking | Scope 1/2/3 emissions with LL97 compliance status |
| `optimization/` | Savings opportunities | Ranked list of improvements with estimated ROI |
