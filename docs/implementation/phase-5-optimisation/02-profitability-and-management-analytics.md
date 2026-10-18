---
phase: "Phase 5 - Optimisation and Intelligence"
epic: "Profitability and Management Analytics"
portals: [Finance Reporting]
status: Ready for review
requirements: [RPT-003, RPT-004, RPT-005, RPT-006]
stories: [US-065, US-066, US-080]
backend_dependencies: [Governed metric catalog, profitability/management read models, lineage, quality, schedule and secure export APIs]
last_updated: 2026-10-17
---

# Epic: Profitability and Management Analytics

## Objective

Provide governed product, customer-segment, branch, channel, and management analytics with metric definitions, lineage, quality, scope, comparability, and secure reporting.

## Experience and controls

- Dashboard/report catalog with metric definition, owner, calculation version, source, currency basis, period, as-of time, quality, and permitted dimensions.
- Drill-down uses authorized aggregates and bounded detail; it does not expose unauthorized customer data.
- Comparisons explicitly handle currency, business date, restatement/version, and incomplete data.
- Reports and exports remain non-authoritative for balances and are backend-generated.

## Slices and evidence

1. Metric catalog and definition/lineage drawer.
2. Management dashboards with accessible alternatives.
3. Profitability dimensions and governed drill-down.
4. Quality/staleness/restatement handling.
5. Scheduled reports and secure exports.

Test metric-version mismatch, stale/incomplete data, mixed currency, restatement, suppressed small cohorts where policy requires, cross-scope denial, export restriction, large data, timezone, and keyboard/chart accessibility.

## Prohibited assumptions

Do not calculate profitability in the browser, combine incompatible metrics silently, or present analytic values as ledger/account balances.
