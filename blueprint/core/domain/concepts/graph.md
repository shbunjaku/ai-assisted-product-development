# The Building Graph

**Scope:** core — this is the foundation of the entire platform.

## What it is

The Building Graph is the platform's digital twin — a graph-structured model of every building. Nodes are entities. Edges are relationships. It is the single source of truth that every product, dashboard, and AI agent reads from.

## Why a graph, not a database

Buildings are relationship-dense. A single fault doesn't live in isolation — it propagates through physical connections, affects spaces, impacts tenants, and costs money.

A graph enables what tables can't:
- **Traversal-based diagnostics** — "If this chiller fails, which AHUs lose cooling, which floors get hot, which tenants are affected?"
- **Blast radius calculation** — "How many sqft are affected? How many tenants? What's the financial exposure?"
- **Cross-domain correlation** — Equipment faults + energy spikes + comfort complaints + work orders, all connected through one graph.

## Relationship types

| Category | Examples |
|----------|---------|
| **Physical** | `feeds`, `serves`, `contains`, `adjacentTo` |
| **Logical** | `memberOf`, `groupedBy`, `controlledBy`, `monitoredBy` |
| **Ownership** | `ownedBy`, `managedBy`, `assignedTo` |
| **Causal** | `causedBy`, `triggers`, `dependsOn` |
| **Metering** | `measures`, `submeters`, `billsTo` |
| **Spatial** | `locatedIn`, `onFloor`, `inZone` |

## Namespaces

Namespace is a tag on entities — not a hierarchy level. It answers: "What domain does this entity belong to?"

| Namespace | What it covers |
|-----------|---------------|
| `hvac` | Chillers, AHUs, VAVs, boilers, pumps, fans |
| `metering` | Electrical, gas, steam, water meters |
| `lighting` | Fixtures, circuits, controls |
| `occupancy` | Presence sensors, access-derived counts |
| `security` | Access control, CCTV, intrusion |
| `ieq` | CO₂, PM2.5, temperature, humidity, acoustic |

A single entity can have signals across multiple namespaces. A space is relevant to `hvac` + `lighting` + `occupancy` simultaneously.

## Graph hierarchy

```
Site → Building → Floor → Space → System → Equipment → Device → Point
```

Namespace sits alongside this hierarchy as a lens, not within it.

## Related concepts
- core/domain/concepts/entities.md — what the nodes are
- core/domain/concepts/signals.md — what signals attach to nodes
- bms/domain/concepts/onboarding.md — how the graph gets built
