---
phase: "Phase 2 - Regulated Operations"
epic: "Branch, Teller, Vault, and Cash Operations"
portals: [Staff Operations]
status: Ready for review
requirements: [BRN-001, BRN-002, BRN-003, IAM-006, LED-004, LED-005, LED-007, WFL-007]
stories: [US-055, US-056]
backend_dependencies: [Branch/till/vault, teller session, cash command, limit, dual-control, balancing and exception APIs]
last_updated: 2026-10-17
---

# Epic: Branch, Teller, Vault, and Cash Operations

## Objective

Enable branch staff to open/close teller sessions, view authoritative till/vault positions, initiate approved cash deposits/withdrawals/transfers, perform dual control, and resolve overage/shortage and end-of-day exceptions.

## Experience and controls

- Branch/till/vault context with explicit currency, denomination support where contracted, business date, operator, and freshness.
- Teller open/close, cash command review, receipt, pending/unknown/final status, and supervisor approval.
- Cash transfer, count/recount, balancing, overage/shortage, reason, evidence, and escalation.
- High-value or vault operations expose dual-control state and never allow self-approval.

## Integrity rules

Browser totals assist presentation only; authoritative cash position, denomination result, limits, fees, posting, and imbalance come from backend. Commands use stable idempotency. Timeout is unknown until status enquiry.

## Slices and evidence

1. Branch/teller context and session state.
2. Cash deposit/withdrawal with exact review and receipt.
3. Till/vault transfer and dual control.
4. Close/balance and exception workflow.
5. Supervisor workbench and end-to-end branch day.

Test wrong branch, closed session, insufficient permission, changed limit, duplicate submit, timeout, dual-control/self-approval, currency mismatch, imbalance, concurrent teller action, session expiry, keyboard number entry, and accessible confirmation.

## Prohibited assumptions

Do not calculate authoritative till balance, post cash, invent denomination/limit policy, or mark a drawer balanced from local arithmetic.
