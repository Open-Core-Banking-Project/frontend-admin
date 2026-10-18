---
phase: "Phase 2 - Regulated Operations"
epic: "Risk, Compliance, Fraud, and AML Investigation"
portals: [Risk Compliance]
status: Ready for review
requirements: [RSK-001, RSK-002, RSK-003, RSK-004, RSK-005, RSK-006, RSK-007, RSK-008, WFL-006, WFL-008]
stories: [US-043, US-044, US-045, US-046]
backend_dependencies: [Screening, alert, risk explanation, case, evidence, decision, rule/model version and monitoring APIs]
last_updated: 2026-10-17
---

# Epic: Risk, Compliance, Fraud, and AML Investigation

## Objective

Provide prioritized alert and screening workbenches, explainable risk context, controlled investigation cases, evidence, decisions, escalation, and role separation without allowing analytical outputs to mutate balances or become unexplained authority.

## Experience and state

- Alert queues by institution, risk, rule/model version, age, status, owner, and SLA.
- Alert detail with reason codes, evidence links, customer/transaction context, timeline, related alerts, and model/rule version.
- Sanctions/PEP/watchlist review, match comparison, disposition, escalation, and rescreen state.
- Investigation case notes/evidence, assignment, decision, approval, reporting handoff, and immutable history.

## Controls

Separate investigator, approver, auditor, and model/rule administrator capabilities. Show model output as decision support with explanation and version. Frontend never changes an account balance or invents allow/challenge/hold/reject policy. Sensitive case evidence remains restricted and redacted from telemetry.

## Slices and evidence

1. Alert/screening queues and accessible risk presentation.
2. Detail, explanation, related activity, and assignment.
3. Investigation notes/evidence and concurrency.
4. Disposition, escalation, approval, and reporting handoff.
5. Rule/model version and performance read-only views.

Test false-positive and true-match paths, insufficient evidence, cross-team denial, self-approval, stale alert, concurrent assignment, restricted evidence, model unavailable, reason-code display, keyboard queue operation, and chart alternatives.

## Prohibited assumptions

Do not invent thresholds, legal reporting criteria, match decisions, model explanations, sanctions policy, or transaction blocks.
