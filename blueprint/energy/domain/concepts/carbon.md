# Carbon Accounting

| Field        | Value |
|--------------|-------|
| Author       | |
| Last updated | |
| Scope        | energy |

## What it is

Carbon accounting is the process of calculating the greenhouse gas (GHG) emissions associated with a building's energy use. It converts energy consumption (kWh, therms, etc.) into equivalent CO₂ emissions (kg CO₂e) using emission factors, then tracks those emissions against regulatory limits or voluntary targets.

## Why it matters

Carbon is increasingly the regulatory and commercial unit of accountability for buildings. NYC LL97, DC BEPS, and the SEC climate disclosure rules all require buildings to report and limit emissions — not just energy. Asset managers face carbon-related financial penalties. Tenants demand carbon data for their own ESG reporting. Investors price carbon risk into acquisitions.

Buildings that don't track carbon can't manage it.

## How it works

### Emission scopes (GHG Protocol)

| Scope | Definition | Building examples |
|-------|-----------|------------------|
| **Scope 1** | Direct emissions from on-site combustion | Natural gas boilers, backup generators, refrigerant leaks |
| **Scope 2** | Indirect emissions from purchased electricity | Grid electricity (varies by grid's carbon intensity) |
| **Scope 3** | All other indirect emissions | Tenant operations, supply chain, embodied carbon in construction |

Buildings primarily report Scope 1 and Scope 2. Scope 3 is complex and usually addressed only for large portfolios or voluntary commitments.

### Emission factors

Energy is converted to CO₂e using emission factors:

| Energy type | Emission factor | Source |
|-------------|----------------|--------|
| **Natural gas** | 53.06 kg CO₂ / MMBtu | US EPA |
| **Electricity** | Varies by grid region | EPA eGRID (updated annually) |
| **Fuel oil #2** | 73.96 kg CO₂ / MMBtu | US EPA |
| **Steam (purchased)** | Depends on utility's generation mix | Local utility |

**Electricity emission factors vary significantly by region.** The Pacific Northwest (mostly hydro) has a very low electricity emission factor. Texas (gas-heavy grid) has a higher factor. This is critical for NYC LL97 compliance: a building using the same amount of electricity as one in a cleaner-grid city will have much higher emissions.

### NYC LL97 — key example

LL97 sets annual carbon emissions limits for NYC buildings over 25,000 sq ft:

```
Annual carbon limit (kg CO₂e) = Building sq ft × Limit (kg CO₂e/sq ft/yr)
```

Limits tighten in phases:
- **Phase 1:** 2024–2029 — significant compliance headroom for most buildings
- **Phase 2:** 2030–2034 — tighter limits; many buildings will need retrofits
- **Phase 3:** 2035+ — aggressive limits approaching net zero

Penalties for exceeding the limit: **$268 per metric ton CO₂e over the limit per year**.

The platform computes:
- Current annual carbon emissions from energy data
- Carbon limit for the building (based on type and sq ft)
- Compliance gap (surplus or deficit)
- Estimated fine if no action is taken
- Actions needed to achieve compliance

### Market-rate electricity (RECs)

Buildings can purchase Renewable Energy Certificates (RECs) to reduce their Scope 2 electricity emissions toward zero. RECs are not physical energy — they are certificates that someone else generated clean energy and the building can claim credit for it.

The platform tracks REC purchases and applies them to reduce Scope 2 reported emissions for compliance purposes.

## Key terms

| Term | Definition |
|------|-----------|
| **CO₂e** | CO₂ equivalent. All GHGs (CO₂, CH₄, N₂O, etc.) expressed as the amount of CO₂ that would have the same warming effect. |
| **Emission factor** | The amount of CO₂e emitted per unit of energy consumed. Varies by fuel type and, for electricity, by grid region. |
| **eGRID** | EPA's Emissions & Generation Resource Integrated Database. Source for regional electricity emission factors. |
| **REC (Renewable Energy Certificate)** | A tradeable certificate representing 1 MWh of renewable electricity. Used to offset Scope 2 emissions. |
| **LL97** | NYC Local Law 97. Sets carbon emissions limits for large buildings starting 2024, with financial penalties. |
| **Carbon intensity** | Carbon emissions per unit of floor area (kg CO₂e/sq ft/yr). The metric used by LL97 and similar laws. |
| **Net zero** | Zero net carbon emissions — usually achieved through efficiency improvements + RECs + offsets. |

## What it is not

- Not the same as energy efficiency. A building can reduce its carbon footprint by switching to renewable electricity without changing its EUI. Conversely, a very efficient building in a carbon-heavy grid may have higher emissions than a less efficient building with clean electricity.
- Not just LL97. Carbon accounting is relevant for BEPS, ENERGY STAR, GRESB, SEC disclosures, and voluntary net-zero commitments.

## Related concepts

- `energy/domain/concepts/eui.md` — energy is the input to carbon calculations
- `energy/domain/concepts/benchmarks.md` — LL97 and BEPS are regulatory benchmarks for carbon
- `energy/domain/concepts/metering-hierarchy.md` — meter data is the source for Scope 1 and 2 calculations
