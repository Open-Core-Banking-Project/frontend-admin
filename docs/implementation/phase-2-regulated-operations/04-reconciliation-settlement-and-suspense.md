---
phase: "Phase 2 - Regulated Operations"
epic: "Reconciliation, Settlement, and Suspense"
portals: [Finance Reporting]
status: Ready for review
requirements: [REC-001, REC-002, REC-003, REC-004, REC-005, REC-006, REC-007, REC-008, REC-009, REC-010, LED-003]
stories: [US-051, US-052, US-053, US-054]
backend_dependencies: [File/API ingestion, run, match, break, settlement, suspense, adjustment, certification and evidence APIs]
last_updated: 2026-10-17
---

# Epic: Reconciliation, Settlement, and Suspense

## Objective

Provide finance operators with ingestion status, reconciliation runs, match results, breaks, settlement positions, suspense visibility, controlled resolution, and certification without altering authoritative records in the browser.

## Experience

- Source/file/API ingestion status and validation evidence.
- Run dashboard with source, business date, currency, counts, totals, match rule version, freshness, and restart/replay state.
- Break workbench for unmatched, missing, duplicate, and amount-mismatched items with ownership, ageing, notes, evidence, escalation, proposed resolution, and linked postings.
- Settlement position and suspense views; certification/sign-off with scope summary.

## Integrity rules

All totals and matches come from backend results. Manual match, adjustment, write-off, or suspense clearance requires capability, reason, approval, authoritative posting reference, and audit evidence. Replays must not be presented as new financial outcomes.

## Slices and evidence

1. Ingestion/run list and validation detail.
2. Match summary and break workbench.
3. Assignment, notes, evidence, and manual-match proposal.
4. Adjustment/suspense workflow status.
5. Settlement certification and secure evidence export.

Test duplicate file, partial validation, rerun/replay, conflicting assignment, unauthorized manual match, self-approval, amount/currency mismatch, unresolved break, certification blocked, timeout, exact totals, large tables, and accessible comparison.

## Prohibited assumptions

Do not calculate settlement, tolerance, match, suspense entry, or write-off outcome client-side. Do not hide unresolved breaks to make totals appear balanced.
