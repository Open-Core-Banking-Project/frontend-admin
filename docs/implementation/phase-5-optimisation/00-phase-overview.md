---
phase: "Phase 5 - Optimisation and Intelligence"
status: Ready for review
portals: [All]
requirements: [RPT-003, RPT-004, RPT-005, RPT-006, RPT-007, RSK-005, RSK-006, RSK-007]
stories: [US-066, US-080]
dependencies: [Phase 4 verified, Approved governed analytical/model contracts]
last_updated: 2026-10-17
---

# Phase 5 - Optimisation and Intelligence

## Objective

Add governed data lineage, profitability/management analytics, and human-controlled AI-assisted or predictive operational insights without turning analytical or model output into authoritative banking action.

## Epics

| Order | Epic | Primary portal |
| --- | --- | --- |
| 1 | Enterprise Data Governance and Lineage | System Administration/Risk |
| 2 | Profitability and Management Analytics | Finance/Reporting |
| 3 | AI-Assisted Service and Predictive Operations | All, capability-specific |

## Gates

- Every metric/model output names source, lineage/version, as-of time, confidence/quality where supplied, and authorized scope.
- Human operators remain responsible for regulated or financial decisions unless an approved policy explicitly states otherwise.
- Generated suggestions cannot call privileged APIs directly, create postings, approve work, or reveal data outside the user's scope.
- Feedback, overrides, model versions, drift, and decisions are auditable through backend evidence.

## Agent instructions

Do not add a generic chatbot or expose unrestricted prompts to banking data. Each use case needs an approved threat model, data-classification review, evaluation set, human-control design, and kill switch.
