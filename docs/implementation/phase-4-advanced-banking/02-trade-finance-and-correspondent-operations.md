---
phase: "Phase 4 - Advanced Banking"
epic: "Trade Finance and Correspondent Operations"
portals: [Staff Operations, Risk Compliance, Finance Reporting]
status: Ready for review
requirements: [IAM-006, IAM-007, RPT-002, RPT-003, SEC-013]
stories: [US-078]
backend_dependencies: [Trade instrument, party, document, limit/collateral, sanctions, approval, message, fee and settlement APIs]
last_updated: 2026-10-17
---

# Epic: Trade Finance and Correspondent Operations

## Objective

Support controlled issuance and servicing of letters of credit and guarantees, document/evidence handling, sanctions review, approvals, correspondence/message status, fees, expiry, amendments, and settlement trace.

## Experience and controls

- Instrument search/detail, parties, amount/currency, dates, terms, document checklist, discrepancy, limit/collateral status, fees, approvals, messages, amendments, expiry, and settlement.
- Role-separated operations, compliance, finance, approver, and audit views.
- Secure document upload/download with scanning, classification, version, legal-hold/retention indicators, and access evidence.
- Backend owns trade rules, message validation, sanctions outcome, charges, accounting, and final settlement.

## Slices and evidence

1. Instrument/party search and detail timeline.
2. Application/draft and document checklist.
3. Discrepancy/sanctions/limit review.
4. Multi-level approval, issue/amend/expire/cancel states.
5. Message and settlement trace plus evidence export.

Test cross-tenant/correspondent access, missing/restricted document, self-approval, stale terms, currency/date precision, sanctions pending, message rejection, settlement unknown, secure download, keyboard workflow, and accessible document status.

## Prohibited assumptions

Do not invent UCP/SWIFT/legal rules, message formats, charges, collateral treatment, sanctions disposition, or accounting behavior.
