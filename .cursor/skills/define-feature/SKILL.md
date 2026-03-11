---
name: define-feature
description: Interactive guide for defining new product features. Walks the user through each section of the context file with questions, creates the file, and registers it in the tracker. Use when the user says "new feature", "define a feature", "start a feature", or wants to create a context file.
---

# Define a New Feature — Interactive Guide

## When to use this skill

- User says "new feature", "define a feature", "start a feature"
- User asks to create a context file
- User wants help thinking through a feature definition

## How this works

This is a **conversational workflow**. Walk the user through the feature definition step by step. At each step, ask questions, wait for answers, then write that section into the context file. Don't dump the whole template — build it up progressively.

The goal: by the end, the user has a filled context file, a tracker entry, and any platform knowledge contributions identified.

---

## Phase 1: Understand the basics

Before creating any files, gather the essentials. Ask these questions (use the AskQuestion tool when available, otherwise ask conversationally):

**Question 1 — Product:**
"Which product does this feature belong to?"
Options: `energy`, `bms`, `fdd`, `datahub`

**Question 2 — Feature name:**
"What should we call this feature? (short name for the folder, e.g. 'budget', 'll97-compliance', 'weather-normalization')"

**Question 3 — One sentence:**
"Describe the feature in one sentence. Use this format: 'This feature lets [who] do [what] so that [why].'"

**Question 4 — Owner:**
"Who owns this feature? (name or role — can be left blank for now)"

Once you have answers, do two things:
1. Create the folder and context file: `context/[product]/[feature-name]/context.md`
2. Add a row to `context/README.md` under the product's dashboard table

Fill in the metadata table, the "In one sentence" section, and set status to `Defining`. Use today's date for Started.

Tell the user: "Context file created. Let's fill it in section by section. I'll ask you questions and write the answers into the file as we go."

---

## Phase 2: Problem & users

**Question 5 — Problem:**
"What problem does this feature solve? Think about:
- Who feels the pain?
- How often do they feel it?
- What breaks or goes wrong without this feature?"

Write their answer into the Problem section. Be concrete — push back on vague answers like "improves user experience."

**Question 6 — Users:**
"Which personas are affected by this feature?"

Read `core/product/personas.md` and present the list:
- Chief Engineer
- Property Manager
- Energy Manager
- Facility Director / Asset Manager
- Tenant
- FDE (Onboarding Engineer)

Let the user pick. Then paste the relevant persona summaries inline into the Users section.

---

## Phase 3: Domain context

Before asking the user, do your own research:
1. Read `core/domain/glossary.md` — find terms relevant to this feature
2. Read `[product]/domain/concepts/` — find concept files that apply
3. Read [products.md](products.md) — check the product-specific questions

Then ask:

**Question 7 — Domain terms:**
"I found these relevant terms from the glossary and [product] concepts: [list them]. Are there additional domain terms specific to this feature that we should define?"

Fill in the domain context table with terms and their definitions in the context of this feature.

**Question 8 — Constraints:**
"What rules must this feature respect because of how the platform works? For example, 'Metrics must be entity-bound' or 'Findings must always be attached to an entity.'"

Also add any constraints you identified from reading the domain concepts and product-specific guidance.

---

## Phase 4: Scope

**Question 9 — What we are building:**
"What are the 2–5 core capabilities of this feature? Keep it plain language — what does the user get?"

**Question 10 — What we are NOT building:**
"What is explicitly out of scope for this version? This is just as important as what's in scope — it prevents scope creep later."

Push the user on this. Every feature needs explicit non-goals.

---

## Phase 5: How it works

**Question 11 — Happy path:**
"Walk me through the happy path — step by step, what does the user do and what does the system do? Start from when the user first touches this feature."

Write as a numbered list.

**Question 12 — Edge cases:**
"What happens when things go wrong or are incomplete? Think about:
- Missing data
- Partial state
- Errors or failures
- Extreme values
- Permissions"

Write as a table: Situation | Behaviour. It's fine if some Behaviour cells are left as open questions.

---

## Phase 6: Design & technical approach

**Question 13 — Design principles:**
"What are the key UX principles for this feature? What should the experience feel like?"

**Question 14 — Key screens:**
"What are the main screens or states the user will see? Just names and brief descriptions — not full specs."

**Question 15 — Architecture:**
Present the standard architecture touchpoints table and ask:
"Which platform components does this feature touch?"
- Building Graph
- Timeseries Engine
- Rules Engine
- Library
- API Layer
- Frontend

For each one the user selects, ask briefly how it's involved.

---

## Phase 7: Dependencies & questions

**Question 16 — Dependencies:**
"What must exist before this feature can work? Think about:
- Data that needs to be available
- Other features that must ship first
- External integrations"

Check the product dependency chain: `core → datahub → bms → fdd / energy`. Flag any upstream dependencies the user may have missed.

**Question 17 — Open questions:**
"What's still unresolved? What decisions haven't been made yet? For each question, who should answer it?"

Every question must have an owner. Push the user to assign one.

---

## Phase 8: Wrap up

After all sections are filled, do three things:

### 1. Knowledge contributions
Check and ask:
"Before we wrap up, let me check if this feature surfaced any platform-wide knowledge:
- Any new terms that should be added to the glossary?
- Any domain knowledge deep enough for its own concept file?
- Any architecture components not yet documented?
- Any new user needs not captured in personas?"

If yes, offer to create or update those shared files.

### 2. Additional documents
Ask:
"Does this feature need any of these? (Most features don't — the context file is usually enough.)
- A separate PRD (formal requirements with acceptance criteria)
- A design spec (detailed screen specs with states and interactions)
- A user flow doc (complex multi-step journey)
- An ADR (irreversible architectural decision)"

If yes, create the file in the feature folder from the relevant template.

### 3. Summary
Tell the user:
- Where the context file lives
- Current status and what's filled vs. what needs more work
- Link to the feature tracker
- What the next step is (usually: "Fill in Figma links when designs are ready, then move to Designing status")

Add a decision log entry: `[today's date] Feature kickoff. Initial scope defined.`

---

## Resuming a feature

If the user mentions a feature that already has a context file, don't start from scratch. Instead:
1. Read the existing context file
2. Read its progress in `context/README.md`
3. Find the first unchecked item in the progress checklist
4. Pick up from there — ask questions for the incomplete sections

---

## Key files to read during the flow

| When | Read |
|------|------|
| Always at start | `core/domain/glossary.md`, `core/product/personas.md` |
| After product is chosen | `[product]/domain/concepts/` (all files), [products.md](products.md) |
| When filling architecture | `core/engineering/architecture.md` |
| When checking design patterns | `core/design/design-system.md` |
| When registering in tracker | `context/README.md` |
| When looking at examples | `context/energy/ll97-compliance/context.md` (the worked example) |

## Reference files

- Product-specific concerns and checklists: [products.md](products.md)
- Document type guidance: [documents.md](documents.md)
