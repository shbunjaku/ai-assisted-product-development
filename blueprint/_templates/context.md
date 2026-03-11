# [Feature Name] — Context

> One file. All the context any team member or AI assistant needs to work on this feature.
> Fill it at kickoff. Keep it updated as the feature evolves. @-mention it in Cursor when asking for help.
> Only spin out separate PRD / design spec / ADR files if the feature is large enough to require them.

---

| Field        | Value |
|--------------|-------|
| Feature      | |
| Product      | datahub / bms / fdd / energy |
| Status       | Defining / Designing / Building / Shipped |
| Owner        | |
| Started      | YYYY-MM-DD |
| Shipped      | YYYY-MM-DD |
| Ticket       | [link] |
| Figma        | [link] |

---

## In one sentence

<!--
"This feature lets [persona] do [action] so that [outcome]."
-->

---

## Problem

<!--
What pain or gap does this solve?
Who feels it, how often, what breaks without this?
Be concrete — avoid generic statements.
-->

---

## Users

<!--
Which personas are directly affected?
Paste a brief summary of each persona here — don't just link.
This makes the file self-contained for AI and fast reviews.
Full personas: core/product/personas.md
-->

**[Persona name]**
Role and goal in one sentence. What they care about most.

---

## Domain context

<!--
The domain knowledge required to work on this feature.
Write brief inline definitions — don't just link.
This is the most important section for AI: it loads the right vocabulary without hunting across files.
Full definitions: core/domain/glossary.md, [product]/domain/concepts/
-->

| Term | What it means in this feature |
|------|------------------------------|
| | |

**Constraints from the domain:**
<!--
Rules the feature must respect because of how the platform works.
E.g. "A Finding must always be attached to an entity — it cannot be free-floating."
-->
-

---

## What we are building

<!--
2–5 bullets. The core capability in plain language.
Enough for any team member to understand scope without reading further.
-->
-

## What we are not building (this version)

<!--
Explicit non-goals. As important as goals — prevents scope creep.
-->
-

---

## How it works

<!--
The behaviour of the feature: what the user sees, what the system does.
Keep this outcome-focused, not implementation-focused.
Flows and edge cases go in sub-sections below if needed.
-->

### Happy path

1.
2.
3.

### Edge cases

<!--
What happens when things are incomplete, missing, or unexpected?
-->

| Situation | Behaviour |
|-----------|-----------|
| | |

---

## Design approach

<!--
Key UX decisions and principles for this feature.
Link to Figma for screens. Only call out decisions that need to be understood, not described.
For most features this replaces a separate flow.md and design-spec.md.
If the design is complex enough to need dedicated files, link to them here.
-->

**Principles:**
-

**Key screens / states:**

| Screen / state | What the user sees | Figma |
|---------------|-------------------|-------|
| | | |

**Open design questions:**
| Question | Owner | Due |
|----------|-------|-----|
| | | |

---

## Technical approach

<!--
How this is built. Key decisions, not implementation detail.
For most features this replaces a separate ADR.
If a decision is complex, irreversible, or affects other teams → create a dedicated ADR and link here.
-->

**Architecture touchpoints:**

| Component | How it's involved |
|-----------|------------------|
| Building Graph | |
| Timeseries Engine | |
| Rules Engine | |
| Library | |
| API Layer | |
| Frontend | |

**Key decisions:**
<!--
What did we decide, and why? What was ruled out?
-->
-

**ADRs:**
<!--
Link to any formal ADRs created for this feature.
-->
-

---

## Dependencies

| Dependency | Status | Owner |
|------------|--------|-------|
| | | |

---

## Open questions

| Question | Owner | Due | Answer |
|----------|-------|-----|--------|
| | | | |

---

## Knowledge contributions

<!--
Every feature surfaces knowledge that benefits the whole platform.
Before moving past Definition, check if anything should be promoted to shared files.
This is how the platform gets smarter with each feature.
-->

- [ ] **Glossary** — Any new terms defined above that should be in `core/domain/glossary.md`?
- [ ] **Domain concepts** — Any deep domain knowledge worth its own file in `[product]/domain/concepts/`?
- [ ] **Architecture** — Does this feature touch a component or data flow not yet in `core/engineering/architecture.md`?
- [ ] **Personas** — Did this feature reveal a user type or need not captured in `core/product/personas.md`?
- [ ] **Design patterns** — Does this feature introduce a reusable UI pattern for `core/design/design-system.md`?

---

## Decision log

<!--
Append-only. Add a dated entry whenever a significant decision is made.
Never delete entries — this is the audit trail.
-->

- **[YYYY-MM-DD]** Feature kickoff. Initial scope defined.
