---
phase: "Phase 2 - Regulated Operations"
epic: "Regulatory and Scheduled Reporting"
portals: [Risk Compliance, Finance Reporting]
status: Ready for review
requirements: [RPT-003, RPT-004, RPT-005, RPT-007, RPT-008, REP-001, REP-002, REP-003]
stories: [US-047, US-065]
backend_dependencies: [Report catalog/schema, schedule, run, validation, approval, regulatory pack, secure distribution and evidence APIs]
last_updated: 2026-10-17
---

# Epic: Regulatory and Scheduled Reporting

## Objective

Provide controlled preparation, validation, scheduling, review, approval, and secure distribution of operational, financial, risk, and country-pack regulatory reports.

## Experience

- Report catalog by institution, country pack, period, obligation, owner, status, and permission.
- Parameter schemas, schedule/calendar, run status, validation exceptions, prior-version comparison, review/approval, submission preparation, attestation, and evidence.
- Secure server-generated PDF/Excel/CSV delivery with expiry, watermark/classification where contracted, and access audit reference.

## Controls

Frontend does not calculate regulatory figures or certify compliance. Reports name source/read model, period, business date, currency, version, generation time, and freshness. PII columns are minimized and access-controlled. Scheduling and distribution destinations are backend-validated.

## Slices and evidence

1. Catalog, obligation calendar, and report metadata.
2. Parameter/run/status and validation exceptions.
3. Schedule and approved distribution configuration.
4. Review/approve/attest workflow.
5. Secure delivery and evidence history.

Test wrong country pack, missing permission, cross-tenant request, invalid period, stale version, failed generation, validation exception, expired export, self-approval, PII masking, timezone/currency labels, and accessible report tables.

## Prohibited assumptions

Do not invent regulator formats, submission deadlines, attestation wording, calculation logic, retention, or legal approval rules.
