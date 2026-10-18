---
title: Frontend Admin Architecture
status: Ready for review
owners: [Frontend Platform, Security, Product, Accessibility]
last_updated: 2026-10-17
---

# Frontend Admin Architecture

## 1. Purpose

This document defines the target architecture for the staff-facing web applications in `frontend-admin`. It turns the product blueprint, SRS, user stories, and repository rules into boundaries that implementation agents can apply consistently.

`../design/UI_DESIGN_DIRECTION.md` is the mandatory companion visual standard. It defines the recognizable product identity, portal-specific navigation, canonical page grids, density, component patterns, microcopy, and anti-generic UI rules within these architectural boundaries.

The architecture supports four independently deployable portals:

1. Staff Operations.
2. System Administration.
3. Risk, Compliance, and Fraud.
4. Finance, Reconciliation, and Reporting.

The applications are operational clients of approved backend APIs. They are not authoritative sources for identity, permission, tenant scope, balances, postings, fees, workflow state, provider outcomes, reconciliation, reports, or audit evidence.

## 2. Source requirements

The primary frontend requirements are:

- `US-074`: role-aware staff operations portal.
- `US-076`: accessible and localised interfaces.
- `NFR-USA-001`: keyboard-complete, responsive, role-aware staff workflows.
- `NFR-ACC-001`: WCAG 2.2 AA target for web frontends.
- `NFR-COMP-001`: supported current major browsers under release policy.
- `API-001` through `API-004`: controlled, versioned, authenticated and validated APIs.
- `DAT-004` and `DAT-005`: exact money/currency and distinct date/time concepts.
- `SEC-002`, `SEC-003`, `SEC-009` through `SEC-013`, and `SEC-018`: frontend cryptography boundary, server-side authorization, step-up, browser threats, masking, and safe non-production data.
- `NFR-OBS-001` and `NFR-OBS-002`: correlation without sensitive telemetry.
- `BR-005` through `BR-010`: duplicate prevention, uncertain outcomes, untrusted frontend values, segregation of duties, secret protection, and audited manual adjustments.

Domain journeys inherit the requirements and stories named by their implementation epic. Requirements remain authoritative even when a screen makes a rule appear obvious.

## 3. Architectural principles

1. Backend authority: every privileged or financial outcome comes from an approved backend contract.
2. Deny by default: UI capability checks improve safety and usability but never replace server enforcement.
3. Tenant-safe by construction: institution and branch context are trusted session properties, included in cache boundaries, and cleared on context changes.
4. Exact operational state: pending, processing, failed, rejected, reversed, disputed, and uncertain are not interchangeable.
5. Accessible by default: shared primitives enforce semantic, keyboard, focus, contrast, and announcement behavior.
6. Contract first: transport schemas and stable error codes precede feature wiring.
7. Independent delivery: portals deploy independently while shared packages use explicit, versioned boundaries.
8. Minimum browser persistence: sensitive and authoritative data remains in memory or server-managed sessions unless an approved design says otherwise.
9. Observable without disclosure: measure failures and journeys without recording secrets or prohibited personal data.
10. Honest readiness: proposed or mocked capability is never represented as implemented production behavior.

## 4. System context

```text
Staff browser
  -> portal deployment / approved edge
     -> optional Next.js server boundary or approved BFF
        -> controlled API gateway
           -> backend domain services
           -> identity provider
           -> document/export delivery services

Portal telemetry
  -> approved redacting telemetry endpoint
     -> monitoring and incident tooling
```

No browser or Next.js process may connect directly to a service database. Provider credentials, signing keys, private encryption keys, and privileged integration tokens remain outside client bundles.

## 5. Portal topology

| Portal | Primary users | Responsibilities | Explicit non-responsibilities |
| --- | --- | --- | --- |
| Staff Operations | Tellers, customer service, account officers, supervisors, operations | Onboarding, customer 360, account service, payments, cash, queues, cases, approvals | Authoritative posting, permission grants, provider finality |
| System Administration | Platform, institution, security, product, workflow and integration administrators | Institution/branch setup, products, policies, roles, workflows, integrations, branding | Secret disclosure, direct database configuration, bypassed publication |
| Risk, Compliance and Fraud | AML, fraud, risk, investigators, compliance | Alerts, screening, cases, evidence, decisions, regulatory preparation | Direct balance mutation, unexplained automated final decisions |
| Finance, Reconciliation and Reporting | Finance, reconciliation, settlement, auditors, management | GL views, settlement, breaks, close controls, reports, secure exports | Treating read models as ledger authority, unaudited manual correction |

Shared navigation may link between portals, but applications must not import one another's internal modules or assume a shared deployment lifecycle.

## 6. Target monorepo structure

```text
frontend-admin/
├── apps/
│   ├── staff-operations/
│   ├── system-admin/
│   ├── risk-compliance/
│   └── finance-reporting/
├── packages/
│   ├── ui/
│   ├── design-tokens/
│   ├── api-client/
│   ├── authentication/
│   ├── permissions/
│   ├── forms/
│   ├── tables/
│   ├── validation/
│   ├── observability/
│   ├── testing/
│   └── utilities/
├── docs/
│   ├── architecture/
│   ├── adr/
│   ├── implementation/
│   ├── security/
│   ├── testing/
│   └── runbooks/
├── tooling/
├── .github/workflows/
└── package.json
```

This is a target, not evidence that the directories have been scaffolded.

## 7. Dependency boundaries

Allowed dependency direction:

```text
apps
  -> feature modules inside the same app
  -> domain-neutral shared packages
     -> design tokens and narrowly scoped utilities

api-client -> no app imports
ui -> design-tokens only, plus approved accessibility utilities
authentication -> api-client/session contracts, never app features
permissions -> typed permission contracts, never route components
```

Rules:

- A package exposes a deliberate public API; consumers do not deep-import internals.
- `ui` contains presentation and interaction primitives, not banking policy.
- `permissions` describes capabilities and scopes but does not manufacture entitlements.
- `api-client` owns transport mechanics and generated types, not screen-specific presentation.
- `utilities` stays small, dependency-light, and domain-neutral.
- Domain-specific reusable components remain in their owning portal until a second real consumer proves a stable shared abstraction.
- Architecture checks should reject app-to-app imports, client imports of server-only modules, dependency cycles, and bypasses of package public entry points.

## 8. Runtime and rendering model

Next.js is the recommended application framework. Each route must choose rendering deliberately:

- Use a server boundary for session bootstrap, policy-safe initial data, response headers, and operations that require server-held credentials.
- Use client components for interactive forms, tables, dialogs, and live workflow behavior.
- Do not move sensitive data into HTML merely to avoid a client request.
- Do not cache privileged user-specific responses in shared edge or public caches.
- Mark freshness and revalidation explicitly; default framework caching must not make operational state appear current when it is stale.
- A backend-for-frontend is introduced only through an approved decision defining ownership, authentication, deployment, audit, and failure behavior. Next.js route handlers must not silently become a new domain backend.

The server/client boundary is enforced by linting, imports, and tests. A module containing secrets, privileged tokens, private endpoints, or server-only session material must be impossible to bundle for the browser.

## 9. Authentication and session architecture

The approved identity service owns authentication. The frontend provides:

- Secure sign-in, MFA, challenge, step-up, and sign-out experiences.
- Session bootstrap and expiry handling.
- Trusted institution, branch, role, and capability context obtained from approved responses.
- Consistent handling of revoked, expired, stale, or elevated sessions.
- Reauthentication return paths that do not preserve secrets or replay unsafe commands.

Prefer secure, HTTP-only, same-site cookies managed by an approved server boundary. Do not place long-lived tokens in local storage. Any exception requires a threat model and ADR.

Logout must clear in-memory server state, query caches, persisted preferences that are identity-bound, service-worker entries, and visible protected content. Cross-tab logout and entitlement invalidation must be defined before production use.

## 10. Authorization model

The frontend consumes stable capability permissions, such as `customer.profile.view`, with contextual scopes. It does not infer permissions from role display names.

Each protected route and action defines:

- Required capability.
- Institution and branch scope.
- Resource-specific scope.
- Step-up requirement.
- Maker-checker or multi-level approval behavior.
- Safe forbidden and stale-entitlement states.

Route guards reduce accidental exposure. Component checks control presentation. The backend independently authorizes every request. A permission utility returns an explicit result such as allowed, denied, out-of-scope, stale, or step-up-required instead of only a boolean when the distinction affects UX.

## 11. Tenant and operator context

Institution context comes from the authenticated session or an approved context-switch endpoint. User-controlled route or form values never establish authority.

On institution, branch, role, or effective-entitlement change:

1. Stop in-flight scope-sensitive reads where safe.
2. Clear or partition relevant query caches.
3. Clear selected records and drafts.
4. Rebootstrap navigation and permissions.
5. Prevent previous-context data from flashing during transition.

Query keys include every trusted scope that changes a response. Tenant isolation receives component, integration, and end-to-end negative tests.

## 12. API client architecture

The preferred contract path is:

```text
approved OpenAPI schema
  -> reproducible code generation
     -> generated transport types/client
        -> thin handwritten policy wrapper
           -> feature query/command hooks
              -> screens
```

Generated files are not edited manually. Wrappers add authentication integration, correlation, idempotency metadata, error normalization, cancellation, telemetry, and safe retry policy.

Stable frontend error categories include:

- Unauthenticated.
- Forbidden or out of scope.
- Validation failed.
- Conflict or stale version.
- Precondition or step-up required.
- Rate limited.
- Dependency unavailable.
- Command outcome unknown.
- Unexpected failure with a safe support reference.

Raw internal errors are never rendered.

## 13. Query, command, and cache model

TanStack Query is the recommended remote-state layer.

Queries:

- Use deterministic, scope-complete keys.
- Use bounded server-side pagination and filters.
- Declare freshness according to operational risk.
- Cancel obsolete reads when safe.
- Never allow prior-tenant data as placeholder content.

Commands:

- Generate or obtain an idempotency key once per intended command and retain it across safe recovery.
- Disable accidental duplicate submission while in flight.
- Do not optimistically finalize privileged or financial state.
- On timeout or disconnect after submission, enter an explicit unknown state and query authoritative status.
- Reconcile caches only after a confirmed outcome.

Local state is reserved for ephemeral UI. Global state is limited to genuine cross-cutting presentation concerns. Server data must not be duplicated wholesale into another store.

## 14. Forms and validation

React Hook Form and Zod are recommended for complex forms, subject to repository configuration. Runtime validation at frontend trust boundaries complements backend validation; it does not establish business authority.

All high-risk forms provide:

- Explicit labels, help, constraints, and associated errors.
- Previous and proposed values where relevant.
- Target institution, resource, amount, currency, date, and consequence.
- Review and confirmation before submission.
- Approval and step-up expectations.
- Backend validation and stable error mapping.
- Safe recovery from conflicts and unknown outcomes.

Money input remains an exact string until an approved decimal representation is used. Never use binary floating point to calculate authoritative values. Do not default currency, account, beneficiary, approval state, or policy silently.

## 15. Workflow and state presentation

Shared workflow patterns must render legal backend states exactly and make terminality clear. A state badge is a view of contract data, not a state machine owned by the browser.

Every workflow screen supports, where applicable:

- Draft, submitted, pending approval, approved, rejected, expired, cancelled, processing, completed, failed, reversed, disputed, and unknown.
- Maker/checker identities and timestamps when permitted.
- Required reason, notes, evidence, and resubmission history.
- Concurrency conflict and eligibility refresh.
- Audit and correlation references.

Color is never the only status signal.

## 16. Tables, search, dashboards, and exports

Operational tables use server-side pagination, sorting, and filtering. They provide semantic headers, keyboard-safe controls, loading and empty states, scope and freshness context, stable row identity, and accessible detail navigation.

Search is authorized and scoped. Search indexes are never presented as ledger authority. Sensitive identifiers are masked by default and revealed only through an approved, audited action.

Dashboards state source, scope, currency, timezone, date range, and freshness. Charts include textual or tabular alternatives.

Exports are backend-generated or use an approved secure delivery flow. The UI presents requested scope, status, expiry, and audit reference. It must not fetch an unbounded dataset into the browser to construct a file.

## 17. Design system and accessibility

The shared design system provides:

- Tokens for typography, spacing, color, elevation, density, motion, and institution theming.
- Semantic primitives for buttons, links, inputs, dialogs, alerts, navigation, tables, tabs, menus, comboboxes, pagination, and status presentation.
- High-density operational layouts without sacrificing target size or readability.
- Consistent destructive, warning, approval, pending, and unknown-outcome patterns.
- Documented keyboard and focus behavior.

The design system must implement the tokens, canonical page grids, portal signatures, component contracts, primitive-adaptation policy, and anti-generic rules in `../design/UI_DESIGN_DIRECTION.md`. Generic component-library themes and stock admin-dashboard compositions are not acceptable product designs.

WCAG 2.2 AA is the target. Automated scanning is necessary but insufficient. Critical journeys require keyboard, zoom/reflow, reduced-motion, contrast, focus, and screen-reader-oriented verification.

Accessibility defects blocking authentication, core operations, approvals, risk investigation, reconciliation, or reports are release blockers.

## 18. Internationalization, money, date, and time

- Visible text uses approved message catalogs; do not concatenate translated fragments.
- Locale affects presentation, not contract semantics.
- Money always retains amount and ISO currency.
- Business date, transaction timestamp, posting date, value date, and settlement date have distinct labels.
- Timestamps retain authoritative offset and display the applicable timezone.
- Date and number parsing is explicit and tested across supported locales.
- Right-to-left support, country packs, and institution-specific terminology are introduced only with approved scope, without hard-coding English layout assumptions into primitives.

## 19. Documents, evidence, and uploads

Documents and evidence use backend-provided secure upload and download mechanisms. The frontend:

- Validates obvious file type and size constraints for timely feedback.
- Shows scanning, processing, rejected, available, expired, and restricted states.
- Avoids reading sensitive file content unnecessarily.
- Prevents file names or previews from introducing script or markup injection.
- Uses expiring, authorized download links and avoids persistent browser caches where required.
- Never embeds production documents in fixtures or screenshots.

Backend services remain responsible for malware scanning, authoritative classification, retention, legal hold, and access evidence.

## 20. Security and privacy architecture

Minimum controls include:

- TLS-only approved endpoints.
- CSP and framing controls.
- CSRF protection compatible with the session architecture.
- Output encoding and approved sanitization for exceptional rich content.
- No secrets or privileged tokens in browser bundles or public environment variables.
- No prohibited data in URLs, analytics, logs, screenshots, or error monitoring.
- Dependency, secret, and artifact scanning in CI.
- Threat modeling for authentication, tenant switching, exports, uploads, impersonation, step-up, and privileged administration.

Selected frontend payload encryption under `SEC-002` is additive to TLS. Only approved public keys may reach clients. Key identifiers, rotation behavior, unsupported-browser behavior, and failure handling require an approved contract before implementation.

## 21. Observability and supportability

The frontend emits approved, redacted telemetry for:

- Page and route performance.
- API latency and normalized error categories.
- Session bootstrap and expiry failures.
- Unknown command outcomes and reconciliation attempts.
- Accessibility and client rendering failures where measurable.
- Critical journey completion without sensitive payloads.

Correlation identifiers propagate through approved requests and are displayed as support references when permitted. Telemetry is not immutable audit evidence and must not record raw forms, customer records, documents, tokens, or complete API bodies.

## 22. Performance and reliability

Define budgets during Phase 0 for JavaScript, route loading, interaction latency, layout stability, and large-table behavior. Measure representative low-spec staff devices and constrained branch networks.

Reliability rules:

- Cached data shows freshness and is not presented as live during an outage.
- Read retries are bounded and observable.
- Command retries follow contract idempotency, never generic client defaults.
- Error boundaries isolate failures without retaining protected content after logout.
- Service workers require explicit security and cache policy; they are not enabled by template default.
- Degraded modes are feature-specific and approved, never inferred from a network failure.

## 23. Testing architecture

| Layer | Purpose |
| --- | --- |
| Unit | Pure validation, formatting, permission interpretation, state mapping |
| Component | Accessible interaction, forms, error states, masking, responsive components |
| Contract | Generated client compatibility, enums, errors, idempotency and correlation metadata |
| Integration | Routes/features with controlled API responses and session/scope changes |
| End-to-end | Critical operator journeys, denials, conflicts, timeout recovery, cross-tenant isolation |
| Accessibility | Automated checks plus manual/assisted keyboard and screen-reader-oriented evidence |
| Visual | Stable shared primitives and critical status layouts where configured |

Tests control identity, permission, tenant, time, locale, timezone, identifiers, and network behavior. Production data and public networks are prohibited.

## 24. Delivery and deployment

Each portal produces an independent, immutable artifact. Shared packages are built reproducibly from the same workspace and do not force synchronized portal release unless a breaking contract requires it.

The pipeline should perform:

1. Frozen dependency installation.
2. Formatting verification.
3. Lint and architecture rules.
4. Type checking.
5. Unit, component, contract, and accessibility tests.
6. Production builds for affected portals.
7. Dependency, secret, and artifact scanning.
8. End-to-end smoke tests in an approved environment.
9. Controlled promotion with evidence and rollback.

Environment configuration is validated without revealing secrets. A non-production build must not silently target production APIs.

## 25. Phased delivery

```text
Phase 0 - Engineering Foundation
  -> Phase 1 - Banking Foundation
  -> Phase 2 - Regulated Operations
  -> Phase 3 - Growth Channels
  -> Phase 4 - Advanced Banking
  -> Phase 5 - Optimisation and Intelligence
```

Frontend phases align to backend capability readiness. A portal may receive features in several phases. A UI can use contract fixtures before a backend capability is available, but it must remain explicitly non-production and cannot be declared integrated until contract and end-to-end evidence exists.

## 26. Architecture decisions required before Phase 0 approval

1. Node.js and pnpm versions and upgrade policy.
2. Next.js version and rendering/deployment model.
3. Monorepo task runner, if any.
4. Identity/session pattern and CSRF model.
5. API gateway versus approved BFF responsibilities.
6. OpenAPI generation tool and schema acquisition process.
7. Design-system foundation and theming approach.
8. Internationalization library and initial supported locales.
9. Telemetry provider, consent basis, and redaction policy.
10. Supported browsers, devices, and branch-network performance budgets.
11. Test runners, browser matrix, and accessibility evidence policy.
12. Hosting, CSP, environment configuration, promotion, and rollback approach.

Record accepted decisions in `docs/adr/`. Do not allow templates or package defaults to decide security boundaries implicitly.

## 27. Architecture compliance

Architecture is verified through:

- Import-boundary and server/client-boundary tests.
- Generated-client reproducibility and contract tests.
- Cross-tenant and permission negative tests.
- Secret and sensitive-data scans.
- Accessibility acceptance for shared primitives and critical journeys.
- Bundle and performance budgets.
- Deployment configuration and security-header checks.
- Manual review of high-risk commands, timeout recovery, exports, and uploads.

Any exception must name its owner, risk, affected portals, expiry or review date, and removal plan.
