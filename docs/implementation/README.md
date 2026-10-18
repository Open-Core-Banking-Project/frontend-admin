# Frontend Admin Implementation Instructions

## Purpose

This directory converts the frontend architecture, SRS, user stories, and approved backend contracts into executable instructions for engineers and coding agents.

The structure mirrors backend delivery phases so frontend features are not mistaken for available backend capabilities. It does not mirror backend project internals: frontend epics are organized around staff journeys, portal ownership, interaction states, and integration evidence.

## Required reading

Before implementing an epic, read:

1. Root `AGENTS.md`.
2. `README.md`.
3. `docs/architecture/FRONTEND_ADMIN_ARCHITECTURE.md`.
4. `docs/design/UI_DESIGN_DIRECTION.md`.
5. This index, the phase overview, and the epic document.
6. Applicable approved designs, ADRs, API schemas, generated clients, and existing tests.
7. Relevant SRS requirements and user stories in the workspace root PDFs.

The sibling `../backend` repository is read-only unless the user explicitly assigns backend work. Frontend work must not depend on uncommitted backend implementation details.

## Directory structure

```text
docs/implementation/
├── README.md
├── EPIC_TEMPLATE.md
├── phase-0-engineering-foundation/
│   ├── 00-phase-overview.md
│   └── 01..05 epic instructions
├── phase-1-banking-foundation/
│   ├── 00-phase-overview.md
│   └── 01..08 epic instructions
├── phase-2-regulated-operations/
│   ├── 00-phase-overview.md
│   └── 01..07 epic instructions
├── phase-3-growth-channels/
│   ├── 00-phase-overview.md
│   └── 01..04 epic instructions
├── phase-4-advanced-banking/
│   ├── 00-phase-overview.md
│   └── 01..02 epic instructions
└── phase-5-optimisation/
    ├── 00-phase-overview.md
    └── 01..03 epic instructions
```

## Document states

- `Draft`: incomplete or awaiting key product, security, design, or contract decisions.
- `Ready for review`: implementation contract is complete enough for product, design, security, accessibility, and engineering review.
- `Approved`: authorized for implementation.
- `In progress`: active implementation exists.
- `Implemented`: code and required automated evidence are complete.
- `Verified`: acceptance, security, accessibility, operational, and traceability evidence is approved.
- `Superseded`: replaced by another document or decision.

Only an approved epic is a stable implementation contract. Drafts and review-ready documents may support reversible scaffolding or prototypes, but not production claims or irreversible security decisions.

## Source precedence

1. Approved user request or work item.
2. Applicable `AGENTS.md`.
3. Approved ADRs, designs, and versioned API contracts.
4. `docs/architecture/FRONTEND_ADMIN_ARCHITECTURE.md`.
5. SRS requirements.
6. User stories and acceptance criteria.
7. Blueprint and repository README.

Conflicts must be recorded and resolved, not silently interpreted.

## Epic contract

Every epic identifies:

- Portal and owning feature areas.
- Requirements, stories, dependencies, and backend contract readiness.
- Actors, permissions, scopes, step-up, and approvals.
- Routes, screens, components, states, and responsive/accessibility behavior.
- Canonical page-grid selection, portal identity, design-token use, component reuse, and anti-generic UI compliance.
- Query, command, cache, idempotency, timeout, and concurrency behavior.
- Sensitive-data, security, privacy, and telemetry restrictions.
- Ordered vertical slices and automated evidence.
- Acceptance criteria, definition of done, open decisions, and prohibited assumptions.

Use `EPIC_TEMPLATE.md` for new epics.

## Traceability

```text
Requirement ID
  -> user story
  -> phase and frontend epic
  -> design/ADR
  -> backend API contract
  -> route/component
  -> automated test
  -> accessibility/security/acceptance evidence
```

Pull requests must list the epic, requirements/stories, API schema version, affected portals/packages, tests, verification commands, and known gaps.

## Agent workflow

1. Confirm the epic is approved or the user explicitly authorized work from a non-approved document.
2. Inspect the current tree; proposed files and scripts may not exist.
3. Verify the relevant backend contract is approved and available. Read backend files only when needed.
4. Identify identity, permission, tenant, financial, approval, sensitive-data, accessibility, and unknown-outcome risks.
5. Implement the smallest complete vertical slice without exposing an unsafe partial feature.
6. Test denial, stale state, conflict, timeout, duplicate submission, and recovery as applicable.
7. Inspect the diff and report exact evidence. Never invent a successful check.

## Phase sequence

Phase 0 creates the delivery and interaction foundation. Phases 1–5 align to the platform capability roadmap. Work may overlap only when dependencies and contracts are stable and feature exposure remains controlled.

An epic may build against synthetic contract fixtures before its backend dependency is live. Such work remains non-integrated until the approved schema, environment, contract tests, and end-to-end evidence pass.

## Global completion gates

Every implemented epic must satisfy the root Definition of Done plus:

- No authoritative rule is implemented only in the browser.
- Permission and cross-tenant denials are tested.
- All material UI states and safe recovery actions exist.
- Keyboard and accessibility evidence covers critical interactions.
- Sensitive data is absent from source, telemetry, fixtures, screenshots, and unsafe storage.
- Backend contract versions and unresolved dependencies are stated accurately.
- No sibling repository was changed unless explicitly assigned.
