---
phase: "Phase 0 - Engineering Foundation"
status: Ready for review
portals: [All]
requirements: [API-001, API-002, API-003, API-004, NFR-USA-001, NFR-ACC-001, NFR-COMP-001, NFR-MNT-001, NFR-OBS-001, NFR-OBS-002, SEC-001, SEC-009, SEC-010, SEC-011, SEC-013, SEC-016, SEC-018]
stories: [US-005, US-006, US-007, US-070, US-071, US-074, US-076, US-079, US-080]
dependencies: []
last_updated: 2026-10-17
---

# Phase 0 - Engineering Foundation

## Objective

Create a deterministic, secure, accessible, observable, and testable frontend platform before exposing banking workflows. Phase 0 culminates in a synthetic walking skeleton proving authentication bootstrap, trusted tenant context, permission-aware navigation, a read, a non-financial idempotent command, error recovery, correlation, and accessible operation.

## Non-goals

- No real customer onboarding, account servicing, posting, payment, teller, risk, reconciliation, or production administration.
- No invented backend routes, permissions, provider behavior, regulatory rules, or production identity configuration.
- No production claim based only on mocks.

## Epics

| Order | Epic | Outcome |
| --- | --- | --- |
| 1 | Repository, Workspace, and Build | Reproducible monorepo, four app boundaries, shared-package rules |
| 2 | Design System and Accessibility | Accessible, themeable operational primitives and evidence process |
| 3 | Application Shell, Identity, and Permission Context | Secure session bootstrap, navigation, context switching, deny states |
| 4 | API Client and Server-State Foundation | Generated contracts, safe reads/commands, errors, caches, unknown outcomes |
| 5 | Testing, Observability, CI, and Delivery | Layered tests, redacted telemetry, deterministic pipeline and deployments |

## Dependency sequence

```text
Repository and Build
  -> Design System
  -> Shell and Identity
  -> API and Server State
  -> Testing, Observability, CI
  -> Walking-skeleton verification
```

Work may overlap after package, runtime, and security boundaries stabilize.

## Walking skeleton

```text
Synthetic staff identity
  -> secure session bootstrap
  -> trusted institution context
  -> capability-filtered navigation
  -> accessible synthetic record list
  -> non-financial command with correlation and idempotency
  -> authoritative status/result
  -> cache reconciliation and redacted telemetry
```

Verify missing permission, cross-tenant attempt, expired session, stale entitlement, duplicate submit, timeout with status enquiry, keyboard completion, and telemetry redaction.

## Entry criteria

- Architecture is ready for review.
- Runtime, package manager, session model, API schema source, and deployment direction have owners.
- Synthetic contracts can be clearly separated from production contracts.

## Exit gates

- Clean checkout installs, formats, lints, type-checks, tests, and builds deterministically.
- Four portal boundaries and approved shared packages exist without app-to-app imports.
- Server-only modules cannot enter client bundles.
- Shared primitives meet documented keyboard/focus/accessibility contracts.
- Session and tenant changes cannot leak prior-context data.
- API layer distinguishes validation, denial, conflict, rate-limit, dependency failure, and unknown command outcome.
- CI scans dependencies and secrets and produces independent portal artifacts.
- Walking skeleton passes automated and manual accessibility/security review.

## Required decisions

Resolve the twelve decisions in the architecture document before Phase 0 becomes `Approved`. Temporary local choices must be replaceable and explicitly marked non-production.

## Agent instructions

- Implement epics in dependency order and keep synthetic flows unmistakably synthetic.
- Do not edit `../backend`; consume only approved schemas or controlled fixtures.
- Do not let framework templates select identity storage, caching, telemetry, or deployment security by accident.
- Update this overview with evidence and accepted deviations after each epic.
