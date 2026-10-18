---
phase: "Phase 1 - Banking Foundation"
epic: "Payments and Transaction Enquiry"
portals: [Staff Operations]
status: Ready for review
requirements: [LED-004, LED-005, LED-006, LED-007, PAY-001, PAY-003, PAY-005, PAY-006, PAY-007, PAY-009, PAY-012, PAY-013, NFR-OBS-001]
stories: [US-020, US-025, US-026, US-050, US-071]
backend_dependencies: [Name enquiry, payment quote/validation, payment command, status enquiry, transaction search/detail and investigation APIs]
last_updated: 2026-10-17
---

# Epic: Payments and Transaction Enquiry

## Objective and scope

Enable permitted staff to initiate approved internal/interbank payment journeys, review authoritative fees and beneficiary results, prevent accidental duplicates, track exact status, and investigate transactions end to end.

## Command experience

1. Select scoped source and enter exact beneficiary/payment data.
2. Obtain backend name enquiry/validation and quote.
3. Present amount, currency, fees, destination, warnings, approval and total exactly as returned.
4. Confirm once with a stable idempotency key.
5. Show submitted reference and authoritative state.
6. On timeout, show outcome unknown and query status without resubmitting.

## Enquiry experience

Server-side search/filter, transaction timeline, posting/payment/provider/workflow references, state history, fees, reversals/disputes, correlation, and permitted investigation actions. Search or provider data never overrides ledger authority.

## Implementation slices and evidence

1. Transaction search/detail and status vocabulary.
2. Name enquiry and exact quote/review.
3. Internal payment command and duplicate protection.
4. Interbank command, pending/uncertain/status enquiry.
5. Failed-payment investigation handoff and trace view.

Test double-click, replayed idempotency key, session loss, quote expiry, insufficient permission, cross-tenant account, changed balance/limit, provider timeout, uncertain-to-final transitions, stale detail, and accessible confirmation/status announcements.

## Prohibited assumptions

Do not calculate fees, trust account ownership from the form, retry blindly, infer finality from redirect/callback, or collapse failed, rejected, uncertain, reversed, and disputed states.
