# Platform AI Context

> This file is optimised for fast AI loading. It is a compressed, structured summary of the entire platform.
> It is not a substitute for the full documentation — it is the entry point.
> When updated, it must reflect what is actually true in the other files.

---

## Platform identity

A building intelligence platform for commercial real estate. It ingests raw data from building management systems (BMS), structures it into a graph-based digital model of each building, and reasons over that model to detect equipment faults, track energy performance, and surface actionable intelligence to the people who operate buildings.

The core product insight: buildings generate enormous amounts of sensor data that is almost never used intelligently. This platform makes that data meaningful.

---

## Who uses it

Defined fully in `core/product/personas.md`. Summary:

| Persona | Primary concern |
|---------|----------------|
| **Chief Engineer** | Equipment health, fault diagnosis, actionable alerts |
| **Property Manager** | Operational performance in business terms — cost, risk, tenant satisfaction |
| **Energy Manager** | Energy/carbon targets, benchmarking, regulatory compliance |
| **Facility Director / Asset Manager** | CapEx decisions, equipment lifecycle, portfolio risk |
| **Tenant** | Comfort, fast issue response |
| **FDE (Onboarding Engineer)** | Connecting buildings, mapping points, building the digital twin |

---

## Platform architecture

Defined fully in `core/engineering/architecture.md`. Summary:

```
BMS / Integration → Point Ingestion → Virtual Point Computation → Rule Evaluation → Findings
                                                                 ↓
                                                    Metric Computation → KPI Evaluation → API → Frontend / AI
```

Two computation models run in parallel:
- **Timeseries Engine** — high-throughput streaming. Raw points, Virtual Points, real-time rule evaluation.
- **Entity / Graph Engine** — batch processing. Metrics, KPIs, Health Scores, graph traversal.

Core components:

| Component | Role |
|-----------|------|
| Building Graph | Stores all entities and their relationships (the digital twin) |
| Timeseries Engine | Processes streaming sensor data in real time |
| Rules Engine | Evaluates rules and fires findings when conditions are met |
| Library | Stores formulas, benchmarks, fault signatures, and KPI targets |
| API Layer | Serves data to frontend and AI agents |
| AI Agent Layer | KAI — reasoning over graph data to answer user questions |

---

## Domain model — key terms

Defined fully in `core/domain/glossary.md`. Every term below has a precise definition there.

| Term | One-line summary |
|------|-----------------|
| **Building Graph** | Directed graph: nodes = entities, edges = relationships. The digital twin. |
| **Entity** | Any node in the graph: building, floor, space, system, equipment, device, or point. |
| **Point** | Raw signal from a physical device. Sensor reading, setpoint, command, alarm, or status. |
| **Virtual Point (VP)** | Calculated signal from one or more raw points. Device-bound. Real-time. |
| **Metric** | Batch-computed, entity-bound signal. Can aggregate from any source (points, VPs, bills, weather). |
| **KPI** | Metric + target from Library + judgment (passing / failing / improving / degrading). |
| **Finding** | Output of a rule firing. Detected problem attached to an entity, with full evidence. |
| **Rule** | Logic that evaluates signals against thresholds and produces findings. |
| **Namespace** | Classification tag on graph nodes. Identifies domain: hvac, metering, lighting, occupancy, etc. |
| **Twin Completeness** | % of expected equipment and points that are connected and modelled. |
| **Building Profile** | Template defining expected systems/equipment for a building type + climate zone. |

Critical distinctions:
- VP is device-bound, real-time. Metric is entity-bound, batch. Do not conflate them.
- Finding is the output. Rule is the logic that produces it. Fault is a type of Finding (equipment failure).
- Metric has no target. KPI = Metric + target + judgment.

---

## Products

### core
Not a product users see. The shared foundation: graph model, signal model, personas, design system, architecture. Every other product depends on it.

### DataHub — Data Platform & Integrations
Foundation layer. Handles everything about getting data in:
- Integration connectors (BMS vendors, utilities, weather, manual uploads)
- Point ingestion pipelines
- Data quality monitoring
- Data catalog and access control

**Modules:** integrations, pipeline, quality, catalog, access

### BMS — BMS Integration & Onboarding
Structures raw data into the Building Graph:
- Device discovery and point mapping
- Equipment classification
- Twin completeness tracking
- Building health for onboarding state

**Modules:** connectivity, mapping, completeness, health

### FDD — Fault Detection & Diagnostics
Reasons over the graph to detect problems:
- Rule evaluation against fault signature library
- Finding generation and lifecycle (open, acknowledged, resolved)
- Issue management and prioritisation
- Rule configuration per equipment type

**Modules:** detection, findings, issues, configuration

### Energy — Energy Management
Reasons over the graph for energy and sustainability:
- Metering and consumption tracking
- Cost analysis
- Carbon accounting
- Regulatory compliance (LL97, BEPS, Title 24, ENERGY STAR)
- Optimisation recommendations

**Modules:** metering, consumption, cost, carbon, optimization

---

## Product dependency chain

```
core → datahub → bms → fdd
                     → energy
```

DataHub provides the raw data. BMS turns it into a structured graph. FDD and Energy reason over that graph. No product bypasses this chain.

---

## How the knowledge base works

The repository is a living knowledge system. It has two layers:

**Shared knowledge (stable, everyone reads):**
- `core/` — glossary, personas, architecture, design system
- `[product]/domain/concepts/` — deep domain knowledge per product

**Feature knowledge (evolving, per-feature):**
- `context/[product]/[feature]/context.md` — everything about a specific feature, grouped by product
- Additional docs (PRD, design spec, ADR, flow) live in the same folder

**The feedback loop:** Every feature definition should make the shared knowledge richer. When defining a feature, new terms go to the glossary. New domain patterns become concept files. New architecture touchpoints update `architecture.md`. This is how the platform gets smarter with each feature — knowledge doesn't stay locked in one context file.

**Rule of thumb:** if three features would benefit from knowing something, it belongs in a shared file.

---

## How features are documented

Each feature lives in `context/[product]/[feature]/`. The folder contains:

| Document | Template | When to create |
|----------|----------|---------------|
| Context file | `_templates/context.md` | Always — every feature gets one |
| PRD | `_templates/prd.md` | If requirements need formal tracking |
| Design spec | `_templates/design-spec.md` | If complex screen specs |
| User flow | `_templates/flow.md` | If complex multi-step flow |
| ADR | `_templates/adr.md` | If irreversible or cross-team decision |

The context file is the entry point. Supporting docs are only created when the feature is large enough to need them.

Feature progress is tracked in `context/README.md` — the feature tracker dashboard.

---

## Where to start for common tasks

| Task | Entry point |
|------|------------|
| Understand the platform | This file → `core/domain/glossary.md` |
| See all features and their progress | `context/README.md` |
| Start working on a feature | `context/[product]/[feature]/context.md` |
| Start a new feature | `_templates/context.md` → create `context/[product]/[feature]/` |
| Understand a user | `core/product/personas.md` |
| Understand a domain term | `core/domain/glossary.md` |
| Understand a concept deeply | `[product]/domain/concepts/[concept].md` |
| Make an engineering decision | `core/engineering/architecture.md` → `_templates/adr.md` |
| Understand current priorities | `core/product/roadmap.md` |
