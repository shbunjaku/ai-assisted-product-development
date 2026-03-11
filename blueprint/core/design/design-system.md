# Design System

> One design system for all products. Product-specific patterns live in each product's `design/` folder.
> Link to Figma, tokens, and component library here.

---

## Links
- Figma library: 
- Token file: 
- Storybook / component docs: 

---

## Foundations

### Color tokens
<!--
List semantic color tokens, not raw hex values.
Products use tokens, never raw colors.
-->

| Token | Usage |
|-------|-------|
| `color.status.critical` | Critical severity findings, errors |
| `color.status.warning` | Medium severity, caution states |
| `color.status.ok` | Healthy state, passing KPIs |
| `color.status.inactive` | Offline, disconnected, unknown |
| `color.data.primary` | Primary data series in charts |
| `color.data.secondary` | Secondary data series |
| `color.surface.base` | Page background |
| `color.surface.raised` | Cards, panels |

### Typography
| Style | Usage |
|-------|-------|
| `heading.xl` | Page titles |
| `heading.lg` | Section headings |
| `heading.md` | Card headings, entity names |
| `body.md` | Default body text |
| `body.sm` | Secondary info, metadata |
| `label.sm` | Field labels, tags |
| `mono.md` | Point values, IDs, technical data |

### Spacing scale
<!--
Document spacing scale so all products use consistent spacing.
-->

### Elevation / shadow levels
<!--
Cards, modals, dropdowns — what elevation do they use?
-->

---

## Core components
<!--
List components that all products use.
Link to Figma and Storybook for each.
-->

| Component | Usage | Figma | Storybook |
|-----------|-------|-------|-----------|
| EntityCard | Summarize any graph entity | | |
| StatusBadge | Show severity, health, or connection state | | |
| SignalValue | Display a Point, VP, Metric, or KPI value with unit | | |
| KPIWidget | Show KPI value + target + status | | |
| FindingCard | Show a finding with severity and evidence | | |
| TimeseriesChart | Plot point or VP data over time | | |
| EmptyState | No data, no results, not connected | | |
| LoadingState | Data is being fetched | | |
| ErrorState | Something went wrong | | |

---

## Patterns

### Severity system
All products use the same four severity levels, always in this order:

| Severity | Color token | When to use |
|----------|-------------|-------------|
| Critical | `color.status.critical` | Immediate action required, equipment at risk |
| High | `color.status.warning-high` | Significant impact, act today |
| Medium | `color.status.warning` | Moderate impact, act this week |
| Low | `color.status.info` | Informational, monitor |

### Empty, loading, and error states
Every screen that loads data must handle all three states. See `_templates/design-spec.md` for the required state checklist.

### Entity page structure
All entity detail pages follow the same layout:
1. Identity header (name, type, status badge, key metadata)
2. Active findings / alerts (if any)
3. Key signals (VPs, Metrics, KPIs)
4. Relationships (what this entity connects to)
5. History / timeline

---

## What lives in product `design/` folders

Product-specific patterns — how FDD presents a fault triage view, how Energy shows a meter hierarchy — live in the product's own `design/` folder, not here. If a pattern starts appearing in two or more products, it should be promoted to this file.
