---
phase: "Phase 2 - Regulated Operations"
epic: "Privileged Access Review"
portals: [System Administration]
status: Ready for review
requirements: [IAM-005, IAM-009, IAM-010, SEC-009, SEC-010, SEC-013]
stories: [US-010]
backend_dependencies: [Access review campaign, effective entitlement, decision, temporary grant and revocation APIs]
last_updated: 2026-10-17
---

# Epic: Privileged Access Review

## Objective

Enable security reviewers to inspect effective privileged access, conflicts, temporary grants, expiry, usage context, and campaign progress, then attest, revoke, escalate, or request evidence through controlled decisions.

## Experience and controls

- Campaign list/detail, reviewer queue, user/resource grant detail, role-to-capability explanation, conflict indicators, evidence, decision reason, and progress.
- Distinguish direct, inherited, delegated, temporary, expired, revoked, pending removal, and stale entitlement states.
- Require step-up and prevent self-review or conflicted review according to backend policy.
- Mask identity attributes not needed for the review and never expose tokens or credentials.

## Slices and evidence

1. Read-only campaigns, queues, and effective-access explanation.
2. Filters, bulk selection with explicit scope summary, and accessible comparison.
3. Attest/revoke/escalate decisions with reason and concurrency.
4. Completion evidence and entitlement refresh.

Test self-review denial, cross-institution access, expired delegation, stale campaign, concurrent reviewer, partial bulk failure, step-up, session expiry, and keyboard-complete review. Bulk actions must report per-item authoritative outcomes.

## Prohibited assumptions

Do not infer effective access from role labels or client-side joins, and do not invent review frequency, evidence policy, or revocation timing.
