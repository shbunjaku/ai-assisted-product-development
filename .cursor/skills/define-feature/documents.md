# Document Types — When and How

> When to create each document type, how to structure it, and what to watch out for.
> The context file is always the primary artefact. These are supplementary documents for larger features.

---

## Context File (the default)

**Template:** `_templates/context.md`
**Location:** `context/[product]/[feature-name]/context.md`
**When:** Always. Every feature gets one. The folder holds this file plus any additional documents the feature needs.

**Purpose:** Single source of truth for a feature — everything a team member or AI assistant needs to understand and work on it.

**How to structure it well:**

- **"In one sentence"** — force a single sentence. If you can't say it in one sentence, the scope isn't clear yet. Format: "This feature lets [persona] do [action] so that [outcome]."
- **Problem** — be concrete. Name who feels the pain. Say how often. Say what breaks without this feature. Avoid generic statements like "improves the user experience."
- **Users** — paste the full persona summary inline from `core/product/personas.md`. Don't just link. The file must be self-contained.
- **Domain context** — this is the most important section for AI. Define every term the feature uses, in the context of this feature. Check the glossary first; don't contradict it. Add domain constraints as bullet points.
- **What we are not building** — this section prevents scope creep. Be specific: "Not building X" is better than "Out of scope: various things."
- **Edge cases** — use the table format (Situation | Behaviour). Think about: missing data, partial state, concurrent users, permissions, extreme values, errors.
- **Open questions** — every question needs an owner and due date. Questions without owners never get answered.

**Good example:** `context/energy/ll97-compliance/context.md`

---

## PRD (Product Requirements Document)

**Template:** `_templates/prd.md`
**Location:** `[product]/product/prd/[module]/[feature].md`
**When:** The feature is large enough that requirements need formal tracking with acceptance criteria and MoSCoW prioritization.

**How it differs from the context file:**
- The context file answers "what are we building and why?" for the whole team.
- The PRD answers "what are the specific requirements, and how do we know when each is done?" — it's more granular.

**How to structure it well:**

- **User stories** — write as "As a [persona], I want [action] so that [outcome]." Each story must be independently valuable and testable. Don't write compound stories.
- **Requirements (MoSCoW)** — Must have / Should have / Won't have. Be honest about Won't have — it's the same as the context file's non-goals but at the requirement level.
- **Acceptance criteria** — write as testable conditions: "Given X, when Y, then Z." Every Must Have requirement needs at least one acceptance criterion.
- **Goals** — prefer measurable outcomes: "user can X without doing Y", "reduces Z by N%". If you can't measure it, reconsider whether it's a real goal.

**Common mistakes:**
- Writing a PRD without a context file. The context file comes first.
- User stories that are really implementation tasks ("As a developer, I want to add a column to the database"). Stories describe user value, not engineering work.
- Acceptance criteria that are too vague to test ("the page loads quickly").

**Link it:** Add the PRD link to the context file's metadata table.

---

## ADR (Architecture Decision Record)

**Template:** `_templates/adr.md`
**Location:** `[product]/engineering/adr/[NNN-decision-name].md`
**When:** A decision is irreversible, affects multiple teams, or has lasting architectural impact. Not for routine implementation choices.

**How to structure it well:**

- **Context** — describe the situation that forced a decision. What constraints, requirements, or trade-offs existed? Don't just say "we needed to decide X" — explain why the decision was non-trivial.
- **Decision** — state it directly in one or two sentences. "We will use X because Y."
- **Consequences** — be honest. Every decision has trade-offs. List what becomes easier, what becomes harder, and what to watch for.
- **Alternatives considered** — show that other options were evaluated. For each rejected option, explain why in one sentence.

**When NOT to write an ADR:**
- The decision is easily reversible.
- Only one team is affected and they all agree.
- The decision is standard practice.
- The context file's "Key decisions" section is sufficient.

**Numbering:** Sequential, never reused. ADR-001, ADR-002, etc. Record it in the product's `engineering/README.md` ADR table.

**Link it:** Add the ADR link to the context file's "ADRs" section under Technical approach.

---

## Design Spec

**Template:** `_templates/design-spec.md`
**Location:** `[product]/design/specs/[module]/[screen-name].md`
**When:** A screen or component is complex enough to need detailed state documentation, interaction specs, and accessibility notes beyond what fits in the context file's design approach section.

**How to structure it well:**

- **Data** — list every data field the screen displays. Where does each come from? This is the contract between design and engineering.
- **States** — document all four states: Empty, Loading, Error, Populated. Designers tend to only design the populated state. Engineers need the others.
- **Interactions** — use the table format (Interaction | Trigger | Result). Be specific about what happens, not just what the user clicks.
- **Edge cases** — what happens with missing data, long strings, zero values, extreme values, no permissions?
- **Accessibility** — keyboard navigation order, screen reader labels, color contrast. Not optional.

**Common mistakes:**
- Only documenting the happy state. Empty, Loading, and Error must be designed upfront.
- Describing visual appearance instead of behaviour. The Figma shows what it looks like; the spec describes what it does.
- Forgetting permissions — what does the screen look like for a user who can view but not edit?

**Link it:** Add the spec link to the context file's design approach section.

---

## User Flow

**Template:** `_templates/flow.md`
**Location:** `[product]/design/flows/[module]/[flow-name].md`
**When:** A multi-step user journey is complex enough to need its own documentation — branching paths, error recovery, multiple systems involved.

**How to structure it well:**

- **Overview** — name the persona, entry point, and success end state. One sentence each.
- **Steps** — for each step, document four things: what the user sees, what the user does, what the system does, and edge cases at that step.
- **Error paths** — use the table format (Step | Error | What happens). For each error, clarify who recovers: user, system, or support?
- **Flow diagram** — include one. Can be ASCII, Mermaid, or a Figma link. The visual is faster to scan than the step-by-step text.

**When NOT to write a flow doc:**
- The flow is a simple linear sequence (3-4 steps, no branching). The context file's "How it works → Happy path" section is enough.
- The flow is identical to an existing flow in another product. Reference it instead.

**Link it:** Add the flow link to the context file's "How it works" section.

---

## How documents relate

```
context/[product]/[feature]/
├── context.md          ← Always exists. Single entry point.
├── prd.md              ← If requirements need formal tracking
├── design-spec.md      ← If complex screen specs
├── flow.md             ← If complex multi-step flow
└── adr-001-*.md        ← If irreversible decision
```

Everything lives in one folder per feature, grouped under its product. The context file is the hub. A reader should never need to open a supporting document without first passing through `context.md`.
