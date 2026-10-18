---
phase: "Phase 3 - Growth Channels"
epic: "Card and Merchant Operations"
portals: [Staff Operations, Finance Reporting]
status: Ready for review
requirements: [SEC-011, SEC-013, REC-001, REC-003, REC-007]
stories: [US-062, US-063]
backend_dependencies: [Card lifecycle/control, merchant onboarding, terminal, settlement, dispute and reconciliation APIs]
last_updated: 2026-10-17
---

# Epic: Card and Merchant Operations

## Objective

Provide authorized back-office card lifecycle/control and merchant onboarding, terminal, settlement, dispute, and exception workflows with strict payment-card data minimization.

## Experience and controls

- Masked card search/detail, lifecycle status, permitted controls, replacement/block request, limits, transactions, disputes, and audit references.
- Merchant profile, beneficial owners/evidence, stores/terminals, pricing reference, approval, activation/suspension, settlement position, and exceptions.
- Full PAN, CVV, PIN, cryptographic material, and secret keys are never rendered, stored, logged, or placed in fixtures.
- Provider/network responses are canonicalized by backend; the frontend does not determine final card or merchant status.

## Slices and evidence

1. Masked card search/detail and lifecycle state.
2. Controlled block/replacement/limit requests.
3. Merchant onboarding, evidence, review, and approval.
4. Terminal and settlement views.
5. Dispute/reconciliation handoff.

Test enumeration resistance, masking, unauthorized reveal/control, cross-tenant merchant, self-approval, provider timeout, stale card status, lost/stolen urgency, settlement mismatch, secure documents, and keyboard-complete workflows.

## Prohibited assumptions

Do not implement PCI-sensitive data collection beyond an explicitly approved contract, invent network/provider semantics, or expose card controls based only on a hidden button.
