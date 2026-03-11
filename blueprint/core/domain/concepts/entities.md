# Entities

**Scope:** core — every product works with entities.

## What it is

An entity is a node in the Building Graph. Every real-world thing in a building — a floor, a chiller, a sensor, a tenant — is an entity. Entities have properties, relationships to other entities, and signals attached to them.

## Entity types

| Entity | What it represents | Key relationships |
|--------|--------------------|-------------------|
| **Building / Site** | The top-level container | Contains: floors, spaces, systems, equipment |
| **Floor** | A level within a building | Contains: spaces; served by: systems |
| **Space** | A physical area — room, zone, common area | Served by: equipment; occupied by: tenant |
| **System** | A logical grouping of equipment that works together | Members: equipment; serves: spaces |
| **Equipment** | A physical device that does work — chiller, AHU, pump | Member of: system; serves: spaces; has: points |
| **Device / Gateway** | The connectivity layer that hosts points | Hosts: points; serves: equipment |
| **Point** | A raw signal value from a device | Belongs to: device; measures: equipment |
| **Tenant** | A company or person occupying spaces | Occupies: spaces; has: lease |
| **Meter** | A meter measuring energy, water, or gas | Measures: equipment or space; bills to: tenant |

## What every entity has

- **Identity** — name, type, ID
- **Properties** — static attributes (install date, capacity, sqft)
- **Relationships** — edges to other entities
- **Signals** — Points, VPs, Metrics, and KPIs attached to it
- **Events** — findings, faults, alerts attached to it

## Twin Completeness

The platform knows what to expect for each entity type. For a chiller, it expects certain points. For an office building, it expects certain systems. The gap between expected and actual is **twin completeness** — expressed as a percentage, per entity and per building.

This is the first thing to check when a building is onboarded: how complete is the twin?

## Related concepts
- core/domain/concepts/graph.md — how entities connect
- core/domain/concepts/signals.md — what signals attach to entities
- core/domain/building-profiles.md — what entities are expected per building type
