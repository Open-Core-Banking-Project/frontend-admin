---
phase: "Phase 1 - Banking Foundation"
status: Ready for review
portals: [Staff Operations, System Administration, Finance Reporting]
requirements: [CFG-001, CFG-003, CFG-005, CFG-006, CFG-007, IAM-004, IAM-006, IAM-007, CUS-001, CUS-005, CUS-007, CUS-009, ACC-001, ACC-002, ACC-003, LED-004, LED-005, LED-007, LED-013, PAY-001, PAY-003, PAY-006, PAY-007, WFL-001, WFL-002, WFL-004, WFL-005, RPT-001, RPT-002, NFR-USA-001, NFR-ACC-001]
stories: [US-001, US-002, US-003, US-004, US-005, US-006, US-007, US-011, US-013, US-014, US-015, US-016, US-017, US-020, US-023, US-025, US-026, US-034, US-035, US-036, US-048, US-049, US-050, US-064, US-070, US-071, US-074, US-076]
dependencies: [Phase 0 verified, Approved Phase 1 API contracts and permissions]
last_updated: 2026-10-17
---

# Phase 1 - Banking Foundation

## Objective

Deliver the first coherent internal banking experience: configure an institution safely, administer access and approvals, onboard and serve customers, operate accounts and basic payments, manage work queues and documents, and trace outcomes without making the frontend authoritative.

## Epics

| Order | Epic | Primary portal |
| --- | --- | --- |
| 1 | Institution, Branch, Product, and Policy Administration | System Administration |
| 2 | Roles, Permissions, and Approval Workflow Administration | System Administration |
| 3 | Individual Onboarding, KYC, and Customer 360 | Staff Operations |
| 4 | Accounts, Deposits, Restrictions, and Statements | Staff Operations |
| 5 | Payments and Transaction Enquiry | Staff Operations |
| 6 | Operations Queues, Cases, Complaints, and Documents | Staff Operations |
| 7 | Notification and Integration Administration | System Administration |
| 8 | Audit, Traceability, and Foundation Reporting | Finance/Reporting and Administration |

## Cross-epic rules

- Every route is capability- and scope-aware; backend denial remains final.
- Configuration and sensitive operations show version, effective date, prior/proposed values, approval state, and audit reference.
- Financial commands use one idempotency key per intended operation and never convert timeout into failure.
- Search results, statements, reports, and dashboards identify source, scope, freshness, currency, and timezone.
- All fixtures and screenshots are synthetic.

## Entry criteria

- Phase 0 is verified.
- Phase 1 permissions, schemas, stable errors, and test identities are available or explicitly approved as fixtures.
- Design coverage exists for each critical journey and exceptional state.

## Exit gates

- A permitted staff user can complete onboarding through approved account and basic payment journeys with authoritative references.
- Denied, cross-tenant, self-approval, stale-record, duplicate-submit, timeout, and session-expiry paths are verified.
- System configuration cannot be published without the backend-defined approval state.
- Customer and financial data is masked, access-controlled, and absent from telemetry/persistence.
- Critical journeys meet keyboard and WCAG 2.2 AA evidence requirements.

## Agent instructions

Implement vertical journeys against approved contracts. A mock-backed screen is not an integrated feature. Do not edit backend files to fill contract gaps; record the dependency and stop the affected slice.
