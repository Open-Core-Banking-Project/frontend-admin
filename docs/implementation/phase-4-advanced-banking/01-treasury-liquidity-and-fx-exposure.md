---
phase: "Phase 4 - Advanced Banking"
epic: "Treasury, Liquidity, and FX Exposure"
portals: [Finance Reporting]
status: Ready for review
requirements: [RPT-003, RPT-004, RPT-005, DAT-004, DAT-005]
stories: [US-077]
backend_dependencies: [Liquidity position/forecast, maturity gap, FX position/rate, limit, deal approval, settlement and report APIs]
last_updated: 2026-10-17
---

# Epic: Treasury, Liquidity, and FX Exposure

## Objective

Provide treasury officers with authoritative positions, forecasts, maturity gaps, FX exposures, limits, alerts, deal workflow status, settlement references, and secure reports.

## Experience and controls

- Dashboard by institution, currency, value/business date, horizon, legal entity, source, and as-of time.
- Position/exposure tables, accessible chart alternatives, limit consumption, breach/near-breach state, drill-down, forecast version, and data-quality warning.
- Deal draft/review/approval/settlement status only where approved APIs exist.
- Explicit rate type, rate timestamp, base/quote currency, precision, and source.

## Slices and evidence

1. Position/liquidity summary and freshness.
2. Maturity-gap and cash-flow forecast views.
3. FX exposure, rates, limits, and alert drill-down.
4. Deal approval/settlement trace.
5. Secure reports and scenario comparison if backend-provided.

Test stale/missing data, mixed currencies, rate precision, breach state, cross-entity denial, self-approval, conflicting deal, partial source failure, timezone/date boundaries, and accessible charts/tables.

## Prohibited assumptions

Do not calculate valuation, conversion, forecast, limit, gain/loss, funds-transfer pricing, or settlement outcome in the browser.
