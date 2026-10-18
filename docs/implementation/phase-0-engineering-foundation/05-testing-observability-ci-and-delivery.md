---
phase: "Phase 0 - Engineering Foundation"
epic: "Testing, Observability, CI, and Delivery"
portals: [All]
packages: [testing, observability, Tooling]
status: Ready for review
requirements: [NFR-MNT-001, NFR-OBS-001, NFR-OBS-002, NFR-PERF-001, NFR-COMP-001, SEC-016, SEC-018]
stories: [US-070, US-071, US-079, US-080]
backend_dependencies: [Correlation contract, Approved test environment]
last_updated: 2026-10-17
---

# Epic: Testing, Observability, CI, and Delivery

## Objective

Establish deterministic layered testing, redacted frontend telemetry, performance budgets, security checks, and independent portal delivery with verifiable rollback.

## Included scope

- Unit/component, contract, end-to-end, accessibility, and optional visual-test foundations.
- Typed synthetic fixture builders and controlled network/session/permission/time/locale utilities.
- Redacted logs, metrics, traces, journey events, and safe support references.
- CI checks, dependency/secret scanning, build artifacts, preview/test deployment, promotion, smoke test, and rollback evidence.
- Browser matrix and performance budgets approved for representative staff environments.

## Telemetry restrictions

No raw form data, credentials, tokens, full identifiers, customer records, documents, or complete request/response bodies. Frontend telemetry is operational evidence, not the immutable audit trail.

## Implementation slices

1. Establish test taxonomy, fixtures, and deterministic controls.
2. Add component and accessibility harnesses.
3. Add contract and browser end-to-end harnesses.
4. Add redacting observability wrapper and correlation propagation.
5. Add CI, scans, artifact provenance, deployment smoke tests, and rollback runbook.
6. Verify the Phase 0 walking skeleton.

## Required evidence

- Clean CI run from a fresh checkout.
- Intentional secret, accessibility violation, contract break, type error, and forbidden import each fail the appropriate gate.
- Telemetry redaction tests cover sensitive fixtures.
- Browser matrix and keyboard journey pass.
- Independent artifacts are traceable to source and can be rolled back.

## Acceptance criteria

- [ ] All quality gates are deterministic and documented.
- [ ] Tests do not use production data or public networks.
- [ ] Observability is useful without sensitive disclosure.
- [ ] Each portal builds and deploys independently under controlled promotion.
- [ ] Walking-skeleton security, accessibility, and recovery evidence passes.

## Prohibited assumptions

Do not select a production telemetry, hosting, or CI vendor without approval. Do not weaken gates to accommodate unstable tests; fix determinism or record a time-bound approved exception.
