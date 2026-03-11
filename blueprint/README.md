# Blueprint

> The shared knowledge foundation for Product, Design, Engineering, and Domain teams.
> `core/` holds definitions that never change. `context/` holds everything a team needs to work on a feature.

---

## Two layers. That's it.

```
blueprint/
│
├── core/                    ← DEFINITIONS. Stable, shared, owned by everyone.
│   ├── domain/              ←   Glossary + concepts (what things are)
│   ├── product/             ←   Personas + roadmap (who we build for, what we're building)
│   ├── design/              ←   Design system (how things look and behave)
│   ├── engineering/         ←   Architecture (how the platform works)
│   └── ai-context.md        ←   Compressed platform summary for AI
│
├── context/                 ← FEATURE CONTEXT. Grouped by product. The primary working layer.
│   ├── README.md            ←   Feature tracker — dashboard of all features and their progress
│   ├── energy/              ←   Energy features
│   │   ├── ll97-compliance/
│   │   │   └── context.md   ←   Main context file (+ prd.md, design-spec.md, adr-*.md as needed)
│   │   ├── budget/
│   │   ├── meters/
│   │   └── ...
│   ├── bms/                 ←   BMS features
│   ├── fdd/                 ←   FDD features
│   └── datahub/             ←   DataHub features
│
├── _templates/              ← Templates. Copy, never edit here.
│   ├── context.md           ←   The main template — use this for new features
│   ├── prd.md               ←   For large features that need a dedicated PRD
│   ├── adr.md               ←   For architectural decisions with lasting impact
│   ├── flow.md              ←   For complex user flows that need their own file
│   ├── design-spec.md       ←   For detailed screen specs
│   └── concept.md           ←   For adding domain knowledge to core/
│
└── [product]/               ← DEPTH. Optional. For detailed specs and decisions.
    ├── domain/concepts/     ←   Product-specific domain knowledge
    ├── product/prd/         ←   Dedicated PRDs for large features
    ├── design/flows|specs/  ←   Detailed design artefacts
    └── engineering/adr/     ←   Formal architectural decisions
```

---

## How to start a feature

**1. Check `core/` first.**
Does the glossary have the terms you need? Do the relevant concept files exist? If not, add them before writing anything else — undefined terms create silent misalignment.

**2. Create a feature folder in `context/[product]/`.**
Create `context/[product]/[feature-name]/` and copy `_templates/context.md` into it as `context.md`.
This is your team's working document and the AI's entry point for this feature.

**3. Register it in the feature tracker.**
Add a row to `context/README.md` and copy the progress template. This is how the team tracks where every feature stands and what's left to do in each phase.

**4. Add more documents only when needed.**
Most features live entirely in one `context.md`. When the feature is large enough, add a PRD, design spec, flow, or ADR to the same folder. Everything stays together.

That's it.

---

## What goes where

| Content | Where it lives |
|---------|---------------|
| "What does X mean?" | `core/domain/glossary.md` or `[product]/domain/concepts/` |
| "Who are our users?" | `core/product/personas.md` |
| "What are we building and why?" | `context/[product]/[feature]/context.md` |
| "What does the design look like?" | `context/[product]/[feature]/context.md` (design approach section) — or a `design-spec.md` in the same folder |
| "What technical decisions were made?" | `context/[product]/[feature]/context.md` (technical approach section) — or an `adr-*.md` in the same folder |
| "What's the platform architecture?" | `core/engineering/architecture.md` |
| "What's being built this cycle?" | `core/product/roadmap.md` |

---

## The rule for `core/`

If knowledge applies to **all products** → `core/`.
If knowledge applies to **one product** → `[product]/domain/concepts/`.
If knowledge applies to **one feature** → `context/[product]/[feature]/context.md`.

Never put feature-specific content in `core/`. Never put cross-product definitions only in a product folder.

---

## Context files: what they contain

A context file is self-contained. When a team member or AI assistant reads it, they should understand the full picture without navigating elsewhere. It includes:

- **In one sentence** — the feature goal
- **Problem** — who is affected, how, what breaks without this
- **Users** — persona summaries inline (not just links)
- **Domain context** — key terms defined inline + constraints from the domain
- **What we're building / not building** — scope and non-goals
- **How it works** — happy path + edge cases
- **Design approach** — key UX decisions and key screens
- **Technical approach** — architecture touchpoints and key decisions
- **Dependencies** — what must exist first
- **Open questions** — with owners and due dates
- **Decision log** — append-only history of decisions made

---

## Where to start reading

| I am... | Start here |
|---------|-----------|
| New to the team | `core/domain/glossary.md` → `core/product/personas.md` |
| Picking up a feature | `context/[product]/[feature]/context.md` |
| Starting a new feature | `_templates/context.md` → create `context/[product]/[feature]/` |
| Adding domain knowledge | `core/domain/glossary.md` → `_templates/concept.md` |
| Making an architectural decision | `core/engineering/architecture.md` → `_templates/adr.md` |
| AI assistant | `../AGENTS.md` → `core/ai-context.md` |

---

## Product knowledge (domain concepts)

| Product | Concepts |
|---------|---------|
| core | `core/domain/concepts/` — graph, entities, signals |
| bms | `bms/domain/concepts/` — protocols, point-mapping, twin-completeness, onboarding-lifecycle, normalization |
| fdd | `fdd/domain/concepts/` — rules, findings, severity |
| energy | `energy/domain/concepts/` — eui, metering-hierarchy, benchmarks, carbon |
| datahub | `datahub/domain/concepts/` — integrations, pipeline, data-quality |

---

## Product dependency order

```
core → datahub → bms → fdd
                     → energy
```

DataHub provides the data. BMS structures it into the graph. FDD and Energy reason over it.
