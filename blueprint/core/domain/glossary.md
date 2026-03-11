# Glossary

> Single source of truth for all platform terms. Every team reads from here.
> To add a term: open a PR, any team can propose, all teams review.
> Format: use `_templates/glossary-entry.md` as a guide.

---

## Building Graph
**Definition:** A graph-structured digital model of a building where nodes are entities (equipment, spaces, systems) and edges are the relationships between them.
**Used in:** core — everything reads from and writes to this graph.
**Do not confuse with:** a database table or a flat list of assets.
**See also:** core/domain/concepts/graph.md

---

## Entity
**Definition:** A node in the Building Graph representing a real-world thing — a building, floor, space, system, equipment, device, or point.
**Used in:** core, fdd, energy, bms.
**See also:** core/domain/concepts/entities.md

---

## Point
**Definition:** A raw sensor reading, setpoint, command, alarm, or status value from a physical device — the lowest-level signal in the platform.
**Used in:** core, bms.
**Do not confuse with:** Virtual Point, which is calculated, not measured.
**See also:** core/domain/concepts/signals.md

---

## Virtual Point (VP)
**Definition:** A calculated signal derived from one or more raw points that makes equipment more complete — for example, efficiency calculated from power and load.
**Used in:** core, fdd, energy.
**Do not confuse with:** Metric, which is entity-bound and batch-computed; VP is device-bound and real-time.
**See also:** core/domain/concepts/signals.md

---

## Metric
**Definition:** A batch-computed, entity-bound signal that can aggregate data from any source — points, VPs, entity properties, bills, or weather.
**Used in:** core, energy.
**Do not confuse with:** Virtual Point, which is device-bound and real-time.
**See also:** core/domain/concepts/signals.md

---

## KPI
**Definition:** A Metric combined with a target from a library and a judgment — passing, failing, improving, or degrading.
**Used in:** core, energy, fdd.
**Do not confuse with:** Metric, which has no target or judgment.
**See also:** core/domain/concepts/signals.md

---

## Finding
**Definition:** The output of a rule firing — a detected problem attached to a graph entity, with full evidence of what triggered it.
**Used in:** fdd.
**Do not confuse with:** Fault (a type of finding specific to equipment failure), or Alert (a threshold crossing).
**See also:** fdd/domain/concepts/findings.md

---

## Rule
**Definition:** Evaluation logic that watches signals against library thresholds and produces findings when conditions are met.
**Used in:** fdd, energy, core.
**See also:** fdd/domain/concepts/rules.md

---

## Namespace
**Definition:** A classification tag on graph nodes that identifies which domain they belong to — hvac, metering, lighting, occupancy, etc.
**Used in:** core, bms.
**Do not confuse with:** a hierarchy level; namespace is a tag alongside the hierarchy, not above it.
**See also:** core/domain/concepts/graph.md

---

## Twin Completeness
**Definition:** A measure of how much of a building's expected equipment and points are actually connected and modeled in the graph — expressed as a percentage.
**Used in:** core, bms.
**See also:** core/domain/concepts/entities.md

---

## Building Profile
**Definition:** A template that defines what systems and equipment are expected for a given building type and climate zone — used to compute twin completeness and guide onboarding.
**Used in:** core, bms.
**See also:** core/domain/concepts/building-profiles.md
