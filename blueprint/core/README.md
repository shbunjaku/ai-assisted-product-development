# Core

> Shared foundation. Every product depends on what is defined here.
> If it only applies to one product, it does not belong here.

---

## What lives here

| Folder | Owned by | What goes in it |
|--------|----------|-----------------|
| `domain/` | Domain / Building Science | Shared glossary, concepts every team needs to understand |
| `product/` | Product | All user personas, cross-product roadmap |
| `design/` | Design | Design system — components, tokens, patterns shared by all products |
| `engineering/` | Engineering | Platform architecture, cross-product ADRs, shared APIs |

---

## domain/

- `glossary.md` — single source of truth for all platform terms. Every team reads this. Any team can propose additions via PR.
- `concepts/` — one file per foundational concept (signals, graph, entities, building profiles). Use `_templates/concept.md`.

## product/

- `personas.md` — all user personas. Products reference these, they don't define their own.
- `roadmap.md` — cross-product priorities. Updated each planning cycle.

## design/

- `design-system.md` — components, tokens, and patterns used across all products. If a pattern only appears in one product, it stays in that product's `design/` folder. When it appears in two or more, it gets promoted here.

## engineering/

- `architecture.md` — system-wide architecture overview.
- `adr/` — architectural decisions that affect the whole platform. Use `_templates/adr.md`.
- `api/` — core API documentation shared across products.
