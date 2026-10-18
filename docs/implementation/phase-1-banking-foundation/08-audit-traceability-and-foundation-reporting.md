---
phase: "Phase 1 - Banking Foundation"
epic: "Audit, Traceability, and Foundation Reporting"
portals: [Finance Reporting, System Administration, Staff Operations]
status: Ready for review
requirements: [LED-006, LED-013, RPT-001, RPT-003, RPT-004, RPT-005, NFR-OBS-001, SEC-013]
stories: [US-023, US-065, US-070, US-071, US-080]
backend_dependencies: [Audit search, transaction trace, report catalog/run, secure export and operational health APIs]
last_updated: 2026-10-17
---

# Epic: Audit, Traceability, and Foundation Reporting

## Objective and scope

Provide permissioned audit search, end-to-end transaction trace, foundational operational/financial reports, report-run status, and secure export delivery while clearly distinguishing read models from authoritative records.

## Experiences

- Audit search/detail with actor, capability, scope, reason, time, correlation, before/after where permitted, and immutable source reference.
- Transaction trace across command, workflow, posting, provider and notification references.
- Report catalog, parameter form, validation, queued/running/ready/failed/expired states, preview summary, and secure download.
- Health/operations summaries with freshness and dependency status, not raw infrastructure secrets.

## Controls

Audit evidence is read-only to ordinary administrators. Sensitive fields are masked based on backend response and reveal is separately permissioned/audited. Reports declare source, scope, currency, timezone, business date, generation time, and freshness. Export generation remains server-side.

## Implementation slices and evidence

1. Audit and trace search/detail.
2. Report catalog and parameter schemas.
3. Asynchronous run/status/download pattern.
4. Foundation dashboards and accessible tables/chart alternatives.
5. Secure export expiry and support references.

Test cross-tenant denial, masked fields, immutable presentation, large pagination, no-results, stale report, run failure, expired link, unauthorized export, timezone/currency labels, and keyboard/screen-reader table behavior.

## Prohibited assumptions

Do not derive audit evidence from browser telemetry, calculate financial statements client-side, generate unbounded exports in the browser, or present a read model as the ledger.
