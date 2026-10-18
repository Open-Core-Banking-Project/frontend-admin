---
phase: "Phase 0 - Engineering Foundation"
epic: "Application Shell, Identity, and Permission Context"
portals: [All]
packages: [authentication, permissions, ui]
status: Ready for review
requirements: [IAM-001, IAM-002, IAM-003, IAM-004, IAM-006, IAM-010, SEC-009, SEC-010, SEC-011, SEC-013]
stories: [US-005, US-006, US-007, US-074]
backend_dependencies: [Approved identity/session contract, Entitlement contract, Tenant-context contract]
last_updated: 2026-10-17
---

# Epic: Application Shell, Identity, and Permission Context

## Objective

Provide secure portal entry, session lifecycle, trusted institution context, capability-aware navigation, and consistent unauthenticated, forbidden, stale, and step-up states.

## Experiences

- Sign-in, challenge/MFA, session bootstrap, sign-out, expiry, revocation, and step-up return.
- Portal shell with skip links, landmarks, breadcrumbs, responsive navigation, user context, and environment identity.
- Institution/branch switching only through an approved trusted flow.
- Capability-aware route and action presentation using stable permission identifiers.

## State model

Distinguish unauthenticated, authenticating, authenticated/loading-entitlements, ready, forbidden, out-of-scope, step-up-required, stale-entitlement, session-expired, revoked, and identity-service-unavailable. Do not expose protected navigation or prior-context content while resolving state.

## Security rules

Prefer secure HTTP-only cookies under the approved model. Never treat decoded unverified claims as authority or store long-lived tokens in browser storage. Clear caches and protected state on logout or trusted-context change. Backend denial remains authoritative.

## Implementation slices

1. Approved session and entitlement contract fixtures.
2. Accessible shell and protected-route boundary.
3. Session bootstrap, expiry, logout, and cross-tab behavior.
4. Permission interpreter and capability-aware navigation/actions.
5. Trusted context switching, cache-clear hooks, step-up, and negative tests.

## Test evidence

- Authentication/MFA success and failure; expiry and revocation.
- Direct navigation without permission, out-of-scope resource, stale entitlement, and self-approval presentation denial.
- Institution switch cannot flash or reuse previous data.
- Logout clears caches and browser history does not reveal protected content.
- Complete keyboard and focus path through shell, dialogs, and errors.

## Acceptance criteria

- [ ] Session and context use approved contracts.
- [ ] Routes and actions fail closed while authority is unresolved.
- [ ] Role names are not used as permission checks.
- [ ] Context changes clear or partition sensitive state.
- [ ] Security and accessibility evidence passes.

## Prohibited assumptions

Do not invent identity endpoints, token storage, permission mappings, impersonation, or tenant-switch semantics. Stop for an explicit decision if the approved contract is absent.
