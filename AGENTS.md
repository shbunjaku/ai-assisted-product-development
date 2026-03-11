# AGENTS.md — AI Assistant Guide

> Read this first. This tells you how the repository is structured and where to find what you need.

---

## What this platform is

A building intelligence platform for commercial real estate. It connects buildings — their sensors, equipment, and systems — into a graph-based digital model, then reasons over that data to detect faults, track energy performance, and surface actionable insights to the people who operate buildings.

Users are not developers. They are facilities engineers, property managers, energy managers, and building science specialists.

---

## Repository structure

```
blueprint/
├── core/              ← Definitions. Stable. All teams read from here.
│   ├── domain/        ← Glossary and concepts (what things mean)
│   ├── product/       ← Personas and roadmap (who we build for)
│   ├── design/        ← Design system (components, tokens, patterns)
│   ├── engineering/   ← Platform architecture
│   └── ai-context.md ← Compressed platform summary — read this for fast context
│
├── context/           ← Feature context. Grouped by product. Start here for any feature work.
│   ├── README.md      ← Feature tracker — dashboard of all features and progress
│   └── [product]/
│       └── [feature]/
│           └── context.md ← Main context file (+ prd.md, design-spec.md, adr-*.md as needed)
│
├── _templates/        ← Copy these. Never edit in place.
│   ├── context.md     ← Main template for new features
│   ├── prd.md
│   ├── adr.md
│   ├── flow.md
│   └── design-spec.md
│
└── [product]/         ← Optional depth. Detailed specs and domain concepts per product.
    ├── domain/concepts/
    ├── product/prd/
    ├── design/flows|specs/
    └── engineering/adr/
```

The repository has **two primary layers**:

1. **`core/`** — definitions that never change. What things mean, who the users are, how the platform works.
2. **`context/`** — features grouped by product (`context/energy/`, `context/bms/`, etc.). Each feature has its own folder with a `context.md` and any supporting documents.

Product folders (`bms/`, `fdd/`, `energy/`, `datahub/`) hold deeper domain knowledge and detailed artefacts. They are supporting reference, not the primary entry point.

---

## How to navigate based on your task

| You are asked to... | Go to |
|--------------------|-------|
| Understand the platform | `core/ai-context.md` |
| Work on a specific feature | `context/[product]/[feature]/context.md` |
| See all features and their progress | `context/README.md` |
| Understand a domain term | `core/domain/glossary.md` |
| Understand a domain concept deeply | `[product]/domain/concepts/[concept].md` |
| Understand who the users are | `core/product/personas.md` |
| Understand the architecture | `core/engineering/architecture.md` |
| Understand what's being built | `core/product/roadmap.md` |
| Start a new feature | `_templates/context.md` — create `context/[product]/[feature]/context.md` |
| Make an architectural decision | `_templates/adr.md` |

---

## Domain vocabulary — minimum required

Read `core/domain/glossary.md` for the full list. These are the terms you must know before working on any feature:

| Term | What it means |
|------|--------------|
| **Building Graph** | Graph-structured digital model of a building. Nodes = entities. Edges = relationships. The digital twin. |
| **Entity** | Any node in the graph: building, floor, space, system, equipment, device, or point. |
| **Point** | Raw sensor reading, setpoint, command, or status from a physical device. |
| **Virtual Point (VP)** | Calculated signal from one or more raw points. Device-bound. Real-time. |
| **Metric** | Batch-computed, entity-bound signal. Can aggregate from any source. |
| **KPI** | Metric + target + judgment (passing / failing / improving / degrading). |
| **Finding** | Detected problem output from a rule. Attached to an entity. Has evidence, severity, and recommended action. |
| **Rule** | Logic that evaluates signals against thresholds and produces findings. |
| **Twin Completeness** | % of expected equipment and points that are verified in the graph. |
| **Namespace** | Tag on graph nodes identifying their domain (hvac, metering, lighting, occupancy). |

Critical distinctions:
- VP = device-bound, real-time. Metric = entity-bound, batch. Not the same.
- Finding = the output. Rule = the logic. Fault = a type of finding (equipment failure specifically).
- Metric has no target. KPI = Metric + target + judgment.

---

## Products

| Product | What it does | Depends on |
|---------|-------------|-----------|
| **DataHub** | Data ingestion: integrations, pipeline, quality, catalog | core |
| **BMS** | Building Graph construction: point mapping, equipment classification, twin completeness | core, datahub |
| **FDD** | Fault detection: rules, findings, issues, configuration | core, bms |
| **Energy** | Energy management: metering, EUI, carbon, compliance, optimization | core, bms |

Dependency order: `core → datahub → bms → fdd / energy`

---

## Context files — the primary AI entry point

When working on any feature, look for its context folder in `context/[product]/[feature]/`. Features are grouped by product. Each feature folder contains a `context.md` (always present) plus any supporting docs (PRD, design spec, ADR, flow) as needed.

The feature tracker at `context/README.md` shows all features and their progress.

If a context folder doesn't exist for the feature you're working on, create one from `_templates/context.md`.

---

## Conventions — always follow these

| Rule | What it means |
|------|--------------|
| **Match the template** | Every document type has a template. Use it. |
| **Reference, don't redefine** | If a term is in the glossary, link to it. Don't define it twice. |
| **Inline personas in context files** | Don't just link to personas.md. Paste the relevant summary inline so the file is self-contained. |
| **Status is always set** | Every file has a status field. Set it: Draft / Review / Approved / Shipped (for docs), or Defining / Designing / Building / Shipped (for context). |
| **Open questions have owners** | Every unresolved question must have a named owner and a due date. |
| **Decision log is append-only** | Add dated entries. Never delete. |
| **`core/` is for everyone** | If it applies to all products → `core/`. If one product → `[product]/`. If one feature → `context/`. |

---

## What NOT to do

- Do not invent platform behaviour. If you're unsure, say so and point to the relevant concept file.
- Do not add feature-specific content to `core/`.
- Do not create documents outside the established templates.
- Do not skip the header metadata table in any document.
- Do not define terms inline without also checking whether they belong in `core/domain/glossary.md`.
