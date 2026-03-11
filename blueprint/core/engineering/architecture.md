# System Architecture

> Platform-wide architecture. Product-specific decisions go in each product's `engineering/adr/` folder.

---

## Overview
<!--
3-5 sentences. What is this system, what does it do, and what are its defining characteristics?
-->

---

## High-level diagram
<!--
Embed an architecture diagram here.
-->

---

## Core components

| Component | What it does | Technology |
|-----------|-------------|-----------|
| Building Graph | Stores entities and relationships | |
| Timeseries Engine | Processes streaming sensor data | |
| Rules Engine | Evaluates rules and fires findings | |
| Library | Stores formulas, benchmarks, fault signatures | |
| API Layer | Serves data to frontend and AI agents | |
| AI Agent Layer | KAI — reasoning over graph data | |

---

## Two computation models

### Timeseries Engine
Processes high-throughput streaming data. Used for:
- Raw point ingestion
- Real-time Virtual Point computation
- Streaming rule evaluation

### Entity / Graph Engine
Processes entity properties and relationships. Used for:
- Batch Metric computation
- KPI evaluation
- Health scores
- Graph traversal (blast radius, relationship queries)

---

## Data flow

```
BMS / Integration
      │
      ▼
  Point ingestion (timeseries)
      │
      ▼
  Virtual Point computation (real-time)
      │
      ▼
  Rule evaluation → Findings
      │
      ▼
  Metric computation (batch)
      │
      ▼
  KPI evaluation
      │
      ▼
  API → Frontend / AI Agent
```

---

## Key architectural decisions
See `engineering/adr/` for the full decision log.

| ADR | Decision |
|-----|---------|
| | |
