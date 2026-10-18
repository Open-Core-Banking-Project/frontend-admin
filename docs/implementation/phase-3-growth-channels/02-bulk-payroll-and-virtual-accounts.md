---
phase: "Phase 3 - Growth Channels"
epic: "Bulk/Payroll Payments and Virtual Accounts"
portals: [Staff Operations, Finance Reporting]
status: Ready for review
requirements: [PAY-005, PAY-006, PAY-007, PAY-010, PAY-011, PAY-012]
stories: [US-030, US-031]
backend_dependencies: [Secure file upload, bulk validation/repair, batch approval/execution/status, virtual account, collection matching and report APIs]
last_updated: 2026-10-17
---

# Epic: Bulk/Payroll Payments and Virtual Accounts

## Objective

Provide back-office oversight and authorized operation of bulk/payroll batches, validation/repair, approval, execution status, virtual accounts, collection references, and matching exceptions.

## Experience

- Secure batch upload with schema, checksum/reference, scanning, parsing, validation, duplicate, repair, approval, scheduled/executing/partial/final states.
- Per-item errors and outcomes plus exact aggregate amount/currency/count from backend.
- Virtual-account create/assign/suspend/close workflows and collection-match investigation.
- Downloadable error/result files through secure expiring links.

## Integrity controls

File content is not trusted authority. Browser previews are bounded and redacted. Execution uses approved idempotency and mandate/approval checks. Partial outcome remains visible per item; timeout triggers status enquiry, not re-upload or resubmit.

## Slices and evidence

1. Batch upload/status and validation summary.
2. Accessible per-item error repair and resubmission versioning.
3. Approval/execution/partial result and unknown-outcome recovery.
4. Virtual-account lifecycle.
5. Collection matching and exception handoff.

Test malicious/oversize file, duplicate batch, formula injection in downloads/previews, mixed currency, partial validation/execution, stale version, self-approval, timeout, cross-corporate access, and large-table accessibility.

## Prohibited assumptions

Do not parse an unbounded payment file in the browser, calculate authoritative totals, assign virtual accounts locally, or interpret partial execution as all-or-nothing.
