---
phase: "Phase 1 - Banking Foundation"
epic: "Institution, Branch, Product, and Policy Administration"
portals: [System Administration]
status: Ready for review
requirements: [CFG-001, CFG-003, CFG-004, CFG-005, CFG-007, ACC-001, ACC-002, ACC-010, DAT-007]
stories: [US-001, US-002, US-003]
backend_dependencies: [Institution, branch, calendar, product, pricing, limit, policy, simulation, approval and publication APIs]
last_updated: 2026-10-17
---

# Epic: Institution, Branch, Product, and Policy Administration

## Objective and scope

Allow authorized administrators to view and manage institution profile, branches, regions, currencies, holidays, business calendars, products, pricing, fees, taxes, limits, and policies through versioned draft-simulate-approve-publish flows.

Excluded: backend calculation engines, direct chart-of-account mutation, production secret entry, and any client-side claim that a draft is active.

## Experiences and state

- Scoped catalog/list, detail, compare-version, create/edit draft, simulate, submit, review, publish, schedule, rollback request, and audit-reference surfaces.
- Distinguish draft, validation failed, simulated, pending approval, approved, scheduled, active, superseded, rejected, rollback pending, and failed.
- Use server-side tables; retain exact currency/date semantics and show effective time zone.

## Controls

Capabilities are resource-specific and institution-scoped. Makers cannot approve their own restricted changes. Sensitive publication may require step-up. Forms show prior/proposed values and backend-calculated simulation results; the browser does not calculate authoritative fees, rates, eligibility, or limits.

## Implementation slices

1. Read-only institution/branch/calendar catalogs.
2. Accessible versioned draft forms with backend validation.
3. Product/pricing/limit/policy catalogs and diff view.
4. Simulation and review evidence.
5. Submit/approve/reject/schedule/publish/rollback states.

## Test and acceptance evidence

- Permission, branch/institution scope, self-approval, conflict, stale version, invalid effective date, and backend validation tests.
- Keyboard-complete dense forms, diff, simulation, and approval flow.
- No floating-point authoritative calculation or client-invented defaults.
- Active configuration changes only after confirmed backend outcome and cache refresh.

## Prohibited assumptions

Do not invent product schemas, approval matrices, rounding, tax, calendar, or rollback semantics. Keep the feature unavailable when the required contract is absent.
