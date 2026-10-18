---
phase: "Phase 1 - Banking Foundation"
epic: "Accounts, Deposits, Restrictions, and Statements"
portals: [Staff Operations]
status: Ready for review
requirements: [ACC-001, ACC-002, ACC-003, ACC-004, ACC-005, ACC-006, ACC-009, LED-007, LED-013, RPT-001, RPT-002]
stories: [US-016, US-017, US-019, US-023]
backend_dependencies: [Product eligibility, account opening/lifecycle, balance view, restriction, statement, receipt and document APIs]
last_updated: 2026-10-17
---

# Epic: Accounts, Deposits, Restrictions, and Statements

## Objective and scope

Allow staff to open an eligible account, view distinct ledger/available/hold/lien/block values, request controlled lifecycle changes, and retrieve authoritative statements and receipts.

## Experiences and states

- Product eligibility and account-opening review with backend-calculated terms.
- Account summary, transaction history, restrictions, holds/liens/blocks, service actions, and audit references.
- Freeze, restrict, reactivate, dormant-reactivation, and close request flows with reason, impact, approval, and status.
- Statement/receipt request, generation, ready, expired, failed, and secure download states.

## Integrity rules

The browser never generates an account number, determines eligibility, calculates interest, combines balance types, or treats search/report data as authoritative. Lifecycle commands use approved idempotency and conflict control. A timeout produces unknown outcome and status enquiry.

## Implementation slices and evidence

1. Account list/detail with masked identifiers and distinct balances.
2. Opening form, eligibility, review, and confirmed result.
3. Restriction/lifecycle request and maker-checker status.
4. Paginated transaction history.
5. Statement/receipt generation and secure delivery.

Test permission and tenant denial, ineligible product, stale customer/account, duplicate submit, self-approval, timeout recovery, balance-label accuracy, large history, secure-link expiry, and accessible money/table presentation.

## Prohibited assumptions

Do not infer currency, status, eligibility, interest, restriction reason, or final closure from local state. Fixed-deposit maturity is Phase 2 unless separately approved.
