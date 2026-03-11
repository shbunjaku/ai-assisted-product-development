# Product Development Repository

This is the knowledge base for a building intelligence platform for commercial real estate. It contains everything needed to define, design, and build the product — domain knowledge, personas, architecture, design system, and feature context files that drive each feature from idea to shipping.

The platform connects buildings — their sensors, equipment, and systems — into a graph-based digital model, then reasons over that data to detect faults, track energy performance, and surface actionable insights to facilities teams.

---

## Repository structure

Everything lives inside `blueprint/`.

```
blueprint/
├── core/                   ← Shared definitions. Stable. All teams read from here.
│   ├── domain/             ← Glossary, domain concepts
│   ├── product/            ← Personas, roadmap
│   ├── design/             ← Design system (tokens, components, patterns)
│   ├── engineering/        ← Platform architecture
│   └── ai-context.md       ← Compressed platform summary for fast context loading
│
├── context/                ← Feature context. Start here for any feature work.
│   ├── README.md           ← Feature tracker dashboard
│   └── [product]/
│       └── [feature]/
│           └── context.md  ← Primary context file (+ prd.md, design-spec.md, adr-*.md as needed)
│
├── _templates/             ← Copy these when creating new documents
│
└── [product]/              ← Deep domain knowledge and detailed specs per product
    ├── domain/concepts/
    ├── product/prd/
    ├── design/flows|specs/
    └── engineering/adr/
```

**Two layers:**

1. **`core/`** — what things mean, who the users are, how the platform works. Rarely changes.
2. **`context/`** — features grouped by product. Each feature has its own folder with a `context.md` and any supporting docs. This is where active work happens.

Product folders (`bms/`, `fdd/`, `energy/`, `datahub/`) hold deeper reference material — domain concepts, PRDs, design flows, and architecture decisions.

---

## Products

| Product | What it does |
|---------|-------------|
| **DataHub** | Data ingestion — integrations, pipeline, data quality, catalog |
| **BMS** | Building Graph construction — point mapping, equipment classification, twin completeness |
| **FDD** | Fault detection — rules, findings, issues, configuration |
| **Energy** | Energy management — metering, EUI, carbon, compliance, optimization |

Dependency chain: `core → DataHub → BMS → FDD / Energy`

---

## Quick navigation

| You want to... | Go to |
|----------------|-------|
| Understand the platform fast | `blueprint/core/ai-context.md` |
| See all features and progress | `blueprint/context/README.md` |
| Work on a feature | `blueprint/context/[product]/[feature]/context.md` |
| Start a new feature | Copy `blueprint/_templates/context.md` into `blueprint/context/[product]/[feature]/` |
| Look up a domain term | `blueprint/core/domain/glossary.md` |
| Understand who the users are | `blueprint/core/product/personas.md` |
| Understand the architecture | `blueprint/core/engineering/architecture.md` |
| See current priorities | `blueprint/core/product/roadmap.md` |

---

## Conventions

- **Use the templates.** Every document type has a template in `_templates/`. Copy it, don't start from scratch.
- **Reference, don't redefine.** If a term is in the glossary, link to it. Don't define it again in a feature file.
- **Every file has a status.** Draft / Review / Approved / Shipped for documents. Defining / Designing / Building / Shipped for features.
- **Open questions need owners.** Every unresolved question gets a named owner and a due date.
- **Decision log is append-only.** Add dated entries. Never delete or overwrite.
- **`core/` is shared.** If it applies to all products, it goes in `core/`. If one product, it goes in `[product]/`. If one feature, it goes in `context/`.

---

## AI assistants

If you are an AI assistant working in this repository, read `AGENTS.md` at the root. It contains navigation rules, domain vocabulary, and conventions you must follow. For fast platform context, start with `blueprint/core/ai-context.md`.
