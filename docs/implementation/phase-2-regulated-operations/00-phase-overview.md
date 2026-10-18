---
phase: "Phase 2 - Regulated Operations"
status: Ready for review
portals: [All]
requirements: [IAM-009, IAM-010, CUS-001, ACC-008, LED-010, LED-011, LED-012, WFL-005, WFL-006, REC-001, REC-002, REC-003, REC-004, REC-005, REC-006, REC-007, REC-008, REC-009, BRN-001, BRN-002, BRN-003, BRN-004, BRN-005, BRN-006, RSK-001, RSK-002, RSK-003, RSK-004, RSK-005, RSK-006, RSK-007, RSK-008, RPT-008]
stories: [US-010, US-012, US-024, US-038, US-039, US-040, US-041, US-042, US-043, US-044, US-045, US-046, US-047, US-051, US-052, US-053, US-054, US-055, US-056, US-057, US-058, US-065, US-073]
dependencies: [Phase 1 verified, Approved regulated-operation APIs and policy decisions]
last_updated: 2026-10-17
---

# Phase 2 - Regulated Operations

## Objective

Extend the verified foundation with privileged-access review, corporate onboarding, lending operations, AML/fraud work, reconciliation and settlement, branch/teller cash controls, agent/degraded operations, and regulatory reporting.

## Epics

| Order | Epic | Primary portal |
| --- | --- | --- |
| 1 | Privileged Access Review | System Administration |
| 2 | Corporate Onboarding and Lending Operations | Staff Operations |
| 3 | Risk, Compliance, Fraud, and AML Investigation | Risk/Compliance |
| 4 | Reconciliation, Settlement, and Suspense | Finance/Reporting |
| 5 | Branch, Teller, Vault, and Cash Operations | Staff Operations |
| 6 | Agency, Offline Capture, and Degraded Operations | Staff Operations/System Administration |
| 7 | Regulatory and Scheduled Reporting | Risk/Compliance and Finance/Reporting |

## Cross-phase gates

- High-risk actions display dual-control, approval, reason, evidence, and exact state.
- No risk score, reconciliation result, cash balance, loan calculation, regulatory return, or offline transaction is authored by the browser.
- Dense workbenches remain keyboard-complete and provide accessible alternatives for visual summaries.
- Unknown, unmatched, unbalanced, suspicious, overdue, degraded, and restricted states remain visible until backend-authorized resolution.

## Exit criteria

- Each critical workbench has permission/tenant/branch denial, conflict, timeout, and recovery evidence.
- Manual matches, adjustments, cash exceptions, risk decisions, and privileged access decisions preserve authoritative audit references.
- Regulatory exports and evidence use secure, expiring delivery.
- Degraded/offline presentation cannot create duplicate or falsely final financial outcomes.

## Agent instructions

Regulatory, accounting, risk, cash, lending, and offline rules must come from approved contracts and policies. Record gaps; do not infer them or modify the backend.
