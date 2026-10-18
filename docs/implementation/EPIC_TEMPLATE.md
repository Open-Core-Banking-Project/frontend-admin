---
phase: "Phase N - Name"
epic: "Epic name"
portals: []
packages: []
status: Draft
requirements: []
stories: []
backend_dependencies: []
design_dependencies: []
adrs: []
last_updated: YYYY-MM-DD
---

# Epic: Name

## 1. Objective

State the measurable operator and business outcome. Name the portals and users that benefit.

## 2. Success measures

- Functional outcome.
- Accessibility and usability outcome.
- Security, reliability, or performance outcome.
- Evidence required for completion.

## 3. Scope

### Included

- Capabilities delivered by this epic.

### Excluded

- Adjacent capabilities and the epic or phase that owns them.

## 4. Actors, permissions, and scope

| Actor | Capability permission | Contextual scope | Step-up | Approval |
| --- | --- | --- | --- | --- |
| Example | `domain.resource.action` | Institution/branch/resource | When required | None/maker-checker/multi-level |

Define deny, stale-entitlement, conflict-of-duty, delegated-access, and self-approval behavior.

## 5. Routes and experiences

| Route or surface | Purpose | Required capability | Primary states |
| --- | --- | --- | --- |
| `/example` | Example | `domain.resource.view` | Loading/empty/ready/error/forbidden |

Describe navigation, responsive layout, keyboard path, focus behavior, and screen-reader announcements.

## 6. Interaction and state model

Define:

- Backend-owned states and legal transitions.
- Local draft and confirmation behavior.
- Loading, empty, restricted, stale, conflict, timeout, unknown, and terminal states.
- What must never be inferred or optimistically finalized by the frontend.

## 7. Backend contracts

| Operation | Method/contract | Permission | Idempotency | Frontend behavior |
| --- | --- | --- | --- | --- |

State schema source/version, pagination/filtering, stable errors, correlation, cache policy, status enquiry, and unavailable-contract behavior. Never invent a route or field.

## 8. Components and package changes

- App feature modules.
- Shared primitives justified by multiple consumers.
- Generated-client changes.
- Server-only versus client-only boundaries.

## 9. Security and privacy

- Threats and abuse cases.
- Tenant and resource isolation.
- Data classification and masking.
- Browser persistence restrictions.
- Upload/download/export controls.
- Telemetry redaction and negative tests.

## 10. Accessibility and localization

- Semantic structure and accessible names.
- Keyboard and focus behavior.
- Status and error announcements.
- Contrast, zoom/reflow, reduced motion, and table/chart alternatives.
- Locale, currency, date, time, and translation behavior.

## 11. Failure, concurrency, and recovery

- Validation and authorization failures.
- Stale records and conflict handling.
- Retry-safe reads and retry-unsafe commands.
- Timeout and unknown command outcomes.
- Session expiry and context change.
- Approved operator recovery paths.

## 12. Implementation slices

1. Approved contract fixtures and failing acceptance tests.
2. Accessible route and component structure.
3. Queries, commands, permissions, and states.
4. Failure, conflict, timeout, and recovery behavior.
5. Telemetry, documentation, and end-to-end evidence.

Each slice must leave the repository buildable and keep incomplete features inaccessible outside approved test environments.

## 13. Test plan

| Test ID | Requirement/story | Level | Scenario | Expected evidence |
| --- | --- | --- | --- | --- |

Include success, validation, permission denial, cross-tenant denial, accessibility, responsive behavior, conflict, timeout, sensitive-data, and recovery scenarios as applicable.

## 14. Acceptance criteria

- [ ] Approved requirements and stories are implemented.
- [ ] Permissions, scopes, step-up, and approvals are represented correctly and backend-enforced.
- [ ] Required UI states and recovery paths are complete.
- [ ] Contract, security, accessibility, and automated evidence passes.
- [ ] Traceability and operator documentation are complete.

## 15. Definition of Done

Reference the repository Definition of Done and add epic-specific release gates.

## 16. Open decisions

| Decision | Impact | Owner | Required by | Status |
| --- | --- | --- | --- | --- |

## 17. Prohibited assumptions

- List product, policy, permission, API, and design decisions agents must not invent.
- State safe behavior while each decision remains unresolved.

## 18. Agent implementation instructions

- Required reading:
- Expected frontend paths:
- Read-only external references:
- Boundaries that must not change:
- Required commands and evidence:
- Conditions requiring an explicit decision:
