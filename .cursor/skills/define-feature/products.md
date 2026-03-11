# Product-Specific Feature Guidance

> Read this when defining a feature for a specific product.
> Each section provides the structure for capturing personas, domain concepts, architectural concerns, and testing considerations.
> Energy is filled as a worked example. Other products follow the same structure — teams populate them as they define features.

---

## Shared concerns (all products)

These apply to every feature regardless of product:

**When defining any feature, ask:**
- Which personas are affected? Check `core/product/personas.md`.
- What domain terms does this feature use? Check `core/domain/glossary.md`.
- Does this feature depend on something upstream in the dependency chain (`core → datahub → bms → fdd / energy`)?
- Does this feature change something that downstream products depend on?
- Does this introduce new terms or entity types that should be added to the glossary?

**Architectural concerns common to all products:**
- Changes to shared components (Building Graph, Timeseries Engine, API Layer) affect every product. Coordinate early.
- API contract changes must be backward-compatible unless a migration plan exists.
- New entity types or relationships in the graph require glossary coordination.

---

## Energy *(worked example)*

**What it does:** Reasons over the Building Graph for energy performance — metering, EUI, carbon, compliance, optimization.

**Primary personas:** *(populate from `core/product/personas.md`)*
- <!-- e.g. Energy Manager, Property Manager -->

**Domain concepts to check:** `energy/domain/concepts/` — eui, metering-hierarchy, benchmarks, carbon

**When defining an Energy feature, ask:**
- Does this involve regulatory compliance? (LL97, BEPS, Title 24, ENERGY STAR) — accuracy and auditability are non-negotiable.
- Does it change the metering hierarchy? (building → system → equipment meter relationships)
- Does it affect EUI calculation? What normalization factors are involved (weather, occupancy, area)?
- Does it produce data that could be submitted to regulators? If yes, calculation methodology must be documented and auditable.
- Is this single-building or portfolio-level? Portfolio features have different data aggregation concerns.
- Does it depend on utility bill data? Bill ingestion has different latency and reliability than real-time meter data.

**Architectural concerns:**
- Energy calculations must be reproducible — same inputs must always produce same outputs.
- Regulatory calculations follow specific published methodologies (e.g., LL97 carbon coefficients). These must match the regulation exactly.
- Metering hierarchy changes affect cost allocation, EUI, and carbon calculations.
- Weather normalization requires reliable external data — handle API failures gracefully.
- Utility bill data arrives monthly, not real-time — features must handle mixed-latency data sources.
- Carbon coefficients and regulatory thresholds change with policy updates — these must be configurable, not hardcoded.

**Testing focus:**
- Calculation accuracy: verify against hand-calculated expected values for known building data
- Regulatory compliance: compare output against published compliance examples if available
- Metering hierarchy: verify correct aggregation when meters are added, removed, or reorganized
- Mixed data sources: real-time meter data + monthly utility bills + weather data — all arriving at different times
- Edge cases: missing utility bill for a month, weather API downtime, building with no sub-meters, mid-year ownership change
- Auditability: every calculated value must be traceable to its source data and methodology

---

## DataHub

**What it does:** Foundation layer. Gets data into the platform — integrations, pipelines, quality monitoring, catalog.

**Primary personas:** *(populate from `core/product/personas.md`)*
-

**Domain concepts to check:** `datahub/domain/concepts/` — integrations, pipeline, data-quality

**When defining a DataHub feature, ask:**
- <!-- What integration types are affected? -->
- <!-- Does this change the ingestion pipeline? Throughput impact? -->
- <!-- Does this affect data quality scoring? Downstream impact? -->
- <!-- Vendor-specific or generic connector? -->
-

**Architectural concerns:**
- <!-- e.g. pipeline changes affect every building, connector failure handling, catalog schema changes -->
-

**Testing focus:**
- <!-- e.g. connector reliability under failure, pipeline throughput, data quality consistency -->
-

---

## BMS

**What it does:** Structures raw data into the Building Graph — point mapping, equipment classification, twin completeness.

**Primary personas:** *(populate from `core/product/personas.md`)*
-

**Domain concepts to check:** `bms/domain/concepts/` — protocols, point-mapping, twin-completeness, onboarding-lifecycle, normalization

**When defining a BMS feature, ask:**
- <!-- Which onboarding phase does this touch? -->
- <!-- Does this change the graph schema? Migration path? -->
- <!-- Does it affect twin completeness? Downstream impact on FDD/Energy? -->
- <!-- Which protocols are affected? Backward-compatible? -->
-

**Architectural concerns:**
- <!-- e.g. graph schema migration, protocol compatibility, normalization model changes -->
-

**Testing focus:**
- <!-- e.g. mapping accuracy, graph migration, protocol compatibility, onboarding workflow -->
-

---

## FDD

**What it does:** Reasons over the Building Graph to detect problems — rules, findings, issues, severity.

**Primary personas:** *(populate from `core/product/personas.md`)*
-

**Domain concepts to check:** `fdd/domain/concepts/` — rules, findings, severity

**When defining an FDD feature, ask:**
- <!-- Does this affect finding creation, prioritization, or resolution? -->
- <!-- Does it change severity logic? -->
- <!-- Could this create more noise (nuisance findings)? -->
- <!-- Does it affect blast radius computation? -->
-

**Architectural concerns:**
- <!-- e.g. finding immutability, issue grouping latency, evidence preservation -->
-

**Testing focus:**
- <!-- e.g. false positive rate, finding lifecycle, severity ranking, noise levels -->
-
