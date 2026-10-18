---
phase: "Phase 0 - Engineering Foundation"
epic: "API Client and Server-State Foundation"
portals: [All]
packages: [api-client, validation, forms, tables]
status: Ready for review
requirements: [API-001, API-002, API-003, API-004, DAT-004, DAT-005, NFR-OBS-001, SEC-011, SEC-013]
stories: [US-020, US-071, US-074]
backend_dependencies: [Versioned OpenAPI source, Problem-details contract, Correlation contract, Idempotency contract]
last_updated: 2026-10-17
---

# Epic: API Client and Server-State Foundation

## Objective

Create a reproducible typed API layer and safe server-state patterns that preserve tenant scope, exact statuses, correlation, idempotency, concurrency, and unknown command outcomes.

## Included scope

- OpenAPI acquisition/generation and generated-code policy.
- Approved authentication, correlation, idempotency, cancellation, and error normalization wrappers.
- Query-key factories including trusted scope.
- Bounded pagination/filter/sort contracts and accessible table adapters.
- Mutation state pattern with confirmation, duplicate prevention, conflict, timeout, status enquiry, and cache reconciliation.
- Exact money, currency, date, time, and identifier adapters for display/input boundaries.

## Safe retry policy

Reads may retry only under bounded approved rules. Commands do not inherit generic retries. A timeout after submission produces `outcome unknown`, retains the intended command identifier/idempotency key, and uses the approved status query. The UI must not generate a new command until resolution or an explicit backend-authorized action.

## Implementation slices

1. Approve schema source, generator, and compatibility check.
2. Generate a synthetic foundation client reproducibly.
3. Add transport wrapper and normalized error model.
4. Add scope-safe query, pagination, and cache patterns.
5. Add non-financial command, duplicate protection, conflict, timeout, and status enquiry.
6. Document feature consumption and prohibited bypasses.

## Tests and evidence

- Generation is deterministic and detects breaking schema changes.
- Query keys isolate institutions and branches.
- `401`, `403`, `409`, `412`, `422`, `429`, `5xx`, abort, offline, and timeout are distinct.
- Duplicate click and repeated idempotency key create one logical command.
- Unknown outcome is not rendered as success or failure.
- Sensitive request/response fields do not enter logs or test snapshots.

## Acceptance criteria

- [ ] Features consume typed wrappers rather than ad hoc fetch calls.
- [ ] Generated code is reproducible and never manually edited.
- [ ] Cache, retry, error, conflict, and timeout policies are executable and documented.
- [ ] Money and time adapters preserve contract semantics.

## Prohibited assumptions

Do not invent endpoints, enum values, error codes, fee calculations, or status transitions. `../backend` is a read-only reference, not a source to patch from this epic.
