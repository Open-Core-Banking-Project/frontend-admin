# Frontend Admin Agent Instructions

## Scope

These instructions apply to the entire `frontend-admin` repository. A more specific `AGENTS.md` in an application or package may add or tighten rules for that area, but it must not weaken the security, authorization, tenant-isolation, financial-integrity, accessibility, privacy, or testing requirements defined here.

This repository contains internal, staff-facing web applications for a multi-institution core-banking platform. Treat correctness, clarity, security, auditability, accessibility, and safe failure handling as product features. Prefer explicit, easily reviewed code over clever abstractions.

The sibling repositories are outside this repository's write scope. In particular, `../backend` may be inspected for approved contracts and integration context when necessary, but do not edit it unless the user explicitly assigns a backend change. Never couple frontend work to uncommitted backend implementation details.

## Authoritative context

Before making architectural, workflow, security, or domain-significant changes, read the applicable sources:

1. `README.md` for repository scope, portal responsibilities, the proposed structure, technology direction, and baseline safety rules.
2. `docs/architecture/FRONTEND_ADMIN_ARCHITECTURE.md` for portal topology, dependency boundaries, runtime model, cross-cutting patterns, and decisions required before foundation approval.
3. `docs/design/UI_DESIGN_DIRECTION.md` for mandatory visual identity, canonical page grids, portal navigation, component patterns, density, microcopy, and anti-generic UI rules.
4. `docs/implementation/README.md`, the applicable phase overview, and the applicable epic instructions for executable scope, sequence, backend dependencies, UI states, tests, and acceptance gates.
5. The current task, issue, acceptance criteria, and approved design artifacts.
6. The applicable requirement and user story in:
   - `../Core_Banking_Software_Requirements_Specification.pdf`
   - `../Core_Banking_User_Stories.pdf`
   - `../Core_Banking_Blueprint.pdf`
7. Approved API schemas, generated clients, ADRs, design-system documentation, authentication guidance, and testing conventions once they exist in this repository.
8. Backend OpenAPI or event contracts when an integration detail cannot be established from the frontend repository. Treat the backend repository as read-only unless explicitly told otherwise.

When sources conflict, use this precedence:

1. The current user request or approved work item.
2. This file and any applicable child `AGENTS.md`.
3. Approved API contracts, ADRs, and security or design-system policies.
4. `docs/architecture/FRONTEND_ADMIN_ARCHITECTURE.md`, `docs/design/UI_DESIGN_DIRECTION.md`, and approved implementation epics.
5. The SRS and its financial, authorization, privacy, and audit invariants.
6. User stories and acceptance criteria.
7. The architecture blueprint.
8. The README and contribution guidance.

Do not invent regulatory rules, accounting treatments, permission semantics, provider behavior, or institution policy. If an unresolved detail can affect funds, customer access, approval authority, regulatory evidence, privacy, or operational recovery, surface it as a decision or blocker instead of silently guessing.

The repository is currently at an early stage. Proposed directories, applications, packages, commands, and dependencies in documentation are not evidence that they exist. Inspect the tree before referring to a script or component, and never claim that a build or test passed unless it was actually run successfully.

## Work method

Before editing:

1. Read every applicable `AGENTS.md` from the repository root to the target directory.
2. Read the relevant README, requirement, user story, API contract, design artifact, and existing implementation or test patterns.
3. Identify the affected portal, user roles, capability permissions, tenant/branch scope, approval workflow, sensitive data, and financial or operational states.
4. Check the working tree and preserve unrelated or user-authored changes.
5. Define the smallest complete change that satisfies the acceptance criteria.
6. Identify all required UI states, including loading, empty, error, forbidden, offline or timed-out, stale, conflict, pending, success, and unknown outcome where applicable.

While editing:

- Keep changes focused on the assigned task.
- Follow established patterns unless they conflict with an explicit rule here.
- Update tests, stories, schemas, fixtures, and documentation with behavior changes.
- Prefer typed contracts, compile-time constraints, and executable tests over prose-only safeguards.
- Keep domain language aligned with approved backend contracts and product terminology.
- Do not perform broad refactors during a narrow feature unless the refactor is necessary and explained.
- Do not introduce speculative infrastructure for future applications or requirements.
- Use synthetic, redacted data in source, fixtures, snapshots, screenshots, and documentation.

Before completion:

- Run the narrowest relevant checks, then the broader affected checks supported by the repository.
- Run formatting, linting, type checking, tests, build validation, and accessibility checks when configured.
- Inspect the diff for secrets, customer data, sensitive screenshots, accidental generated files, backend edits, and unrelated changes.
- Verify important paths using the actual UI or end-to-end tests when practical.
- Report commands run, results, assumptions, and remaining risks.

Never claim that a build, test, accessibility audit, browser flow, or API integration passed unless it was actually executed successfully.

## Repository and application architecture

The intended repository is a TypeScript web monorepo containing independently deployable staff portals and deliberately shared packages. Until approved configuration establishes otherwise, the planned applications are:

- Staff Operations Portal.
- System Administration Portal.
- Risk, Compliance, and Fraud Portal.
- Finance, Reconciliation, and Reporting Portal.

Use Next.js, React, and TypeScript when scaffolding is approved, with the repository-pinned Node.js version, package manager, framework versions, and workspace tooling. Do not switch package managers, regenerate a lockfile with a different tool, or add a second frontend framework without explicit approval.

Keep application responsibilities explicit:

- `apps/*` contains deployable portals, route composition, portal-specific workflows, and application configuration.
- `packages/ui` contains reusable presentation primitives and accessible interaction patterns, not banking authorization logic.
- `packages/design-tokens` contains approved visual tokens and themes.
- `packages/api-client` contains generated or carefully maintained transport contracts and client infrastructure.
- `packages/authentication` contains session integration and authentication UI helpers, not an independent source of identity truth.
- `packages/permissions` contains typed capability checks and display helpers; the backend remains the enforcement boundary.
- `packages/forms`, `packages/tables`, and `packages/validation` contain stable reusable patterns when real duplication justifies them.
- `packages/utilities` remains small and domain-neutral. Do not turn it into a dumping ground.

Additional architecture rules:

- Prefer feature-oriented modules within each portal over global folders grouped only by file type.
- Keep server-only code, browser code, and shared code clearly separated.
- Never import server-only secrets or privileged clients into a client bundle.
- Keep business workflows out of generic visual components.
- Do not create a universal form, table, repository, or state abstraction merely to remove a few repeated lines.
- Avoid deep cross-application imports. Reuse code through approved packages with deliberate public APIs.
- Do not make one portal depend on another portal's internal modules.
- Keep packages acyclic and enforce boundaries with tooling when the workspace supports it.
- Prefer composition over deeply configurable components with many boolean props.
- Use server rendering, client rendering, and caching deliberately according to data sensitivity, freshness, and interaction needs.

## Technology baseline

Follow repository configuration when present. Until more specific configuration exists, prefer:

- TypeScript in strict mode; do not use `any` to bypass contract or domain uncertainty.
- Next.js and React using current repository-approved patterns.
- Tailwind CSS and approved design tokens for styling.
- React Hook Form and Zod for complex forms and client-side feedback.
- TanStack Query for remote server state.
- TanStack Table for large operational tables.
- OpenAPI-generated typed API clients where practical.
- Vitest or Jest with Testing Library for unit and component tests.
- Playwright for critical end-to-end journeys.
- Storybook for reusable visual components when configured.
- ESLint and Prettier for static quality and consistent formatting.

Do not add a dependency until existing platform or repository capabilities have been considered. For every new dependency, assess maintenance, license, security history, bundle impact, accessibility, browser support, transitive dependencies, and whether the functionality belongs in shared code. Use exact workspace conventions for versions and dependency placement.

Avoid dependencies that duplicate framework capabilities, require unsafe HTML, leak data to third parties, or materially enlarge privileged admin bundles without clear value.

## Backend authority and financial integrity

The frontend is never authoritative for balances, postings, fees, limits, permissions, approval eligibility, workflow state, provider outcomes, or audit evidence.

For every money-related or operationally sensitive flow:

1. Display backend-provided values and currency explicitly.
2. Collect only permitted input and validate it for timely user feedback.
3. Submit the exact approved API contract without client-invented authority.
4. Use backend-supported idempotency for commands when required.
5. Treat the backend response or authoritative status query as the source of truth.
6. Preserve and display stable transaction, correlation, workflow, and audit references where permitted.
7. Represent pending, processing, approved, rejected, failed, reversed, cancelled, and unknown or uncertain outcomes distinctly.

Never:

- Calculate an authoritative balance, fee, interest amount, exchange result, or posting outcome in the browser.
- Treat a disabled or hidden control as authorization enforcement.
- infer success from a redirect, closed dialog, optimistic update, provider page, or network disconnect.
- Blindly retry a timed-out or ambiguous financial command.
- Replace a backend status with a friendlier but materially different status.
- Allow stale cached values to appear current without a freshness indicator where that could mislead an operator.
- Use JavaScript floating-point arithmetic for authoritative monetary calculations.

Formatting money for display is allowed. Keep the original amount and ISO currency from the contract, use locale-aware formatting, and do not discard precision. When collecting decimal input, preserve it as a string or another exact representation until the backend validates and processes it.

Business date, transaction time, posting date, value date, and settlement date are different concepts. Label them accurately and include timezone context where relevant.

## Authentication, sessions, and authorization

- Integrate only with the approved identity and session mechanism.
- The backend is the final authorization boundary. Frontend permission checks exist to present the correct experience and reduce invalid requests.
- Use stable capability permissions such as `payment.transfer.initiate`; do not hard-code security behavior to display names or assume role names are permissions.
- Deny or hide privileged interactions when identity, capability, scope, or entitlement freshness cannot be established, while still expecting backend denial.
- Respect institution, branch, channel, account, customer, corporate mandate, amount, currency, device, and step-up scopes supplied by authoritative services.
- Do not decode a token and treat unverified claims as trusted authorization state.
- Do not persist access tokens, refresh tokens, OTPs, PINs, or sensitive entitlement data in browser storage unless an approved security design explicitly requires it.
- Handle session expiration consistently, preserving only non-sensitive recoverable state.
- Prevent post-logout data from remaining visible through caches, history, tabs, service workers, or client stores.
- Require reauthentication or step-up authentication when instructed by the backend or approved policy.
- A maker must not be offered self-approval for restricted actions, but the backend must still enforce the prohibition.

Permission-aware UI must distinguish at least:

- The user is not authenticated.
- The user is authenticated but lacks a capability.
- The user has the capability but lacks scope for this resource.
- The action requires approval or step-up verification.
- The user's entitlement is stale or has changed.
- The resource no longer exists or is no longer actionable.

Avoid exposing protected data while deciding which of these states applies.

## Tenancy and resource scoping

- Every tenant-owned view and action must use institution context obtained from a trusted authenticated source.
- Never trust a route parameter, query string, form field, local storage value, or table filter as proof of tenant or branch authority.
- Do not provide a fallback production institution or silently retain the previous institution after a context switch.
- Clear or partition caches when institution, branch, role, user, or effective permission context changes.
- Include tenant and scope in query keys when responses differ by those values.
- Prevent stale data from one institution, branch, customer, or account flashing in another context.
- Treat cross-institution access failures as security-relevant behavior and test them.
- Do not merge or compare records across institutions unless the API and the operator's permission explicitly support it.

## Forms and high-risk actions

Forms for financial, identity, product, configuration, case-management, reconciliation, and approval operations require deliberate behavior:

- Use explicit labels, descriptions, constraints, and error associations.
- Preserve user input after recoverable validation errors without retaining secrets longer than needed.
- Validate client-side for usability, but display backend validation as authoritative.
- Prevent accidental duplicate submission while a request is in flight.
- Do not permanently disable recovery after an ambiguous response; provide status enquiry or an approved next step.
- Show the previous and proposed values for sensitive changes when contracts provide them.
- Provide a review step for high-risk or irreversible submissions.
- State the target institution, branch, customer/account, amount, currency, effect, and approval requirement clearly.
- Require an explicit reason when the approved workflow requires one.
- Do not invent defaults for money, currency, beneficiary, institution, approval, product, or security settings.
- Do not silently coerce malformed or out-of-range values.
- Warn before discarding meaningful unsaved work, without trapping users indefinitely.

Confirmation dialogs must name the action and its consequence. Generic prompts such as "Are you sure?" are insufficient for privileged or financial operations.

Optimistic UI is inappropriate for authoritative financial posting, permission changes, approval decisions, account restrictions, product publication, reconciliation resolution, and other high-risk state transitions unless an approved design explicitly defines safe reconciliation and rollback behavior.

## API integration and server state

- Consume approved, versioned APIs through typed clients.
- Prefer generated clients from committed or reproducibly fetched OpenAPI schemas when practical.
- Do not edit generated code manually; change the generator, schema, or wrapper as appropriate.
- Map transport errors to stable user-facing states without leaking stack traces, SQL details, internal hostnames, tokens, or sensitive identifiers.
- Preserve correlation and request identifiers for support and audit where permitted.
- Cancel obsolete reads when safe. Do not cancel or misreport a command after the backend may have committed it.
- Retry safe reads conservatively. Retry mutations only when the contract and idempotency semantics prove it is safe.
- Use bounded pagination, filtering, and sorting for large operational datasets.
- Keep query keys deterministic and include every scope that changes the response.
- Invalidate or update caches only when the authoritative outcome is known.
- Handle `401`, `403`, `404`, `409`, `412`, `422`, `429`, and `5xx` responses according to their distinct semantics.
- Treat timeouts and connection loss during commands as unknown outcomes until an authoritative status check resolves them.
- Do not scrape, reach into databases, or call private service endpoints from the browser.

Published API contracts are compatibility commitments. Do not guess a missing request field, enum value, permission, or state transition. Surface contract gaps and coordinate them without writing into the backend unless the user explicitly requests backend work.

## Workflow, approvals, and concurrency

- Render workflow state from backend data, not from which page the user reached.
- Show maker, checker, approval level, reason, timestamps, and audit references only when permitted.
- Make terminal and non-terminal states visually and programmatically distinct.
- Expect records to change while open. Use version, ETag, or other concurrency mechanisms supplied by the API.
- On conflict, do not overwrite blindly. Show that the record changed and provide a safe refresh or comparison path.
- Do not assume an action remains eligible because its button was rendered earlier.
- Refresh or reconcile after approval, rejection, reassignment, escalation, publication, reconciliation resolution, or other workflow transitions.
- Preserve server-provided reasons and error codes accurately. Do not collapse rejection, cancellation, expiration, and failure into one generic state.

## Data protection and frontend security

Never commit, render unnecessarily, log, or include in telemetry:

- Passwords, PINs, OTPs, access tokens, refresh tokens, session cookies, private keys, or API secrets.
- Full card data, CVV, complete BVN/NIN values, full account numbers where masking is required, or live customer documents.
- Production customer records or unredacted evidence in fixtures, screenshots, tests, stories, issues, or documentation.

Security rules:

- Escape untrusted content by default. Do not use raw HTML rendering without an approved sanitizer and a documented need.
- Do not build URLs, CSS, selectors, or executable code from unsanitized user-controlled input.
- Keep secrets out of public environment variables and client bundles. Values prefixed for browser exposure are public.
- Apply approved CSP, secure-cookie, CSRF, XSS, clickjacking, and referrer policies at the correct layer.
- Avoid sensitive data in URLs, page titles, analytics, error monitoring, browser logs, clipboard helpers, caches, and persisted state.
- Treat uploaded KYC documents, evidence, and exports as sensitive. Use backend-provided secure transfer mechanisms.
- Validate file type, size, and state for usability, while relying on backend scanning and enforcement.
- Prevent tabnabbing on external links and clearly identify external destinations.
- Do not introduce third-party analytics, chat, fonts, scripts, or error tracking into privileged portals without privacy and security approval.
- Use dependency and secret scanning configured by the repository.

If a secret or live customer data is found, stop exposing it, report it, and require the appropriate rotation or incident response. Removing the visible string alone may not be sufficient.

## Accessibility and operational usability

Target WCAG 2.1 AA or the later repository-approved standard. Accessibility is part of acceptance, not a final polish step.

- Use semantic HTML before ARIA.
- Ensure every control is keyboard operable with a visible focus indicator.
- Preserve logical focus order and move focus deliberately after dialogs, route changes, validation failures, and dynamic updates.
- Give inputs programmatic labels and connect descriptions and errors.
- Announce material asynchronous status changes without creating excessive noise.
- Do not use color alone to represent status, severity, risk, or selection.
- Meet approved contrast and target-size requirements.
- Support zoom, text resizing, reflow, reduced motion, high contrast, and common assistive technologies.
- Use accessible tables for tabular data, including meaningful headers, captions where useful, and keyboard-safe interactions.
- Provide alternatives for charts and visual-only summaries.
- Avoid disabling browser zoom or intercepting standard keyboard behavior without strong justification.
- Localize visible text and formatting through approved internationalization utilities; do not concatenate translated fragments.

Internal staff portals are keyboard-heavy operational tools. Optimize frequent paths for speed without hiding meaning or weakening safeguards. Destructive shortcuts must require deliberate confirmation and must not conflict with assistive technology or browser conventions.

## Tables, search, filters, and exports

- Use server-side pagination, sorting, and filtering for large datasets unless bounded size is proven.
- Keep filters shareable only when doing so does not put sensitive values in URLs.
- State timezone, currency, units, date range, freshness, and applied scope where relevant.
- Preserve stable row identity; do not use array indexes for mutable operational records.
- Represent loading, empty, no-results, partial, stale, error, and restricted states distinctly.
- Avoid rendering unbounded result sets or exporting all data from the browser.
- Exports require explicit authorization, minimum necessary fields, safe delivery, auditability, and a visible scope summary.
- Do not use CSV or spreadsheet export patterns that allow formula injection; follow the approved server-side export contract.
- Mask sensitive identifiers consistently while preserving permitted ways to distinguish records.

## Design system and presentation

- Reuse approved tokens and accessible components before creating local variants.
- Keep visual meaning consistent across portals, especially statuses, severity, risk, approvals, money, and destructive actions.
- Components must support required states rather than relying on consumers to improvise them.
- Do not hard-code tenant branding into shared components.
- Prefer responsive layouts that support primary desktop use and approved tablet or smaller-browser fallbacks.
- Avoid decorative motion in high-density operational workflows; honor reduced-motion preferences.
- Screenshots and visual fixtures must contain synthetic data only.

When no design system exists yet, establish the smallest coherent foundation required by the assigned feature. Do not attempt to build an exhaustive component library speculatively.

## State management and browser persistence

- Treat remote API data as server state and keep it in the approved query layer.
- Use component or feature-local state for ephemeral interactions.
- Introduce global client state only for genuinely cross-cutting, non-authoritative concerns.
- Do not mirror all server data into a second global store.
- Keep sensitive data out of local storage, session storage, IndexedDB, service-worker caches, and persisted state unless explicitly approved.
- Scope and clear persisted preferences by user and institution when they could otherwise leak context.
- Do not persist privileged draft data by default.
- Make cache freshness, invalidation, and logout cleanup explicit.

## Error handling, observability, and supportability

- Provide actionable, plain-language errors while preserving stable machine error codes for support.
- Distinguish user-correctable validation, authorization denial, concurrency conflict, rate limiting, dependency failure, and unknown command outcome.
- Error boundaries must prevent a local rendering failure from exposing sensitive details or corrupting the surrounding workflow.
- Capture approved telemetry with data minimization and redaction.
- Never send raw form values, tokens, customer records, document content, or full API payloads to analytics or error monitoring.
- Propagate correlation context through approved clients.
- Instrument meaningful workflow failures and performance without treating telemetry as audit evidence.
- Provide recovery actions such as retry-safe read, refresh, return to queue, or status enquiry according to the failure type.

## Performance and reliability

- Set measurable performance expectations for dense tables, search, dashboards, and critical workflows.
- Avoid unnecessary client bundles, duplicate fetching, waterfall requests, and excessive re-renders.
- Virtualize only when it preserves accessibility and interaction correctness.
- Lazy-load large, non-critical features where it improves real user experience.
- Use image, font, and asset loading that respects CSP, privacy, and layout stability.
- Design degraded and offline behavior explicitly. Do not present cached banking data as live.
- Never trade authorization, correctness, accessibility, or audit context for a superficial performance improvement.

## Testing requirements

Every behavioral change requires proportionate automated evidence.

Use:

- Unit tests for formatting, validation, pure policies, reducers, and state mappings.
- Component tests for accessible interaction, form behavior, conditional capability UI, error states, and sensitive-data masking.
- Contract tests for API client generation, schema assumptions, enum and error mappings, and compatibility-critical adapters.
- Integration tests for routed features with realistic mocked or controlled APIs.
- End-to-end tests for critical staff journeys against safe test environments and synthetic data.
- Accessibility tests combining automated checks with keyboard and assistive-technology-oriented verification for critical flows.
- Visual regression tests for stable shared components and high-risk status presentation when configured.

Tests must cover, where applicable:

- Authentication, MFA or step-up, logout, session expiration, and entitlement changes.
- Capability denial, scope denial, self-approval denial, and cross-institution access denial.
- Loading, empty, forbidden, error, stale, conflict, pending, success, and unknown-outcome states.
- Duplicate submission prevention and idempotency key behavior at the client boundary.
- Network timeout after command submission and safe authoritative status enquiry.
- Concurrent record change and conflict recovery.
- Maker-checker submission, approval, rejection, reassignment, expiration, and terminal states.
- Exact money and currency display, boundary values, negative values where valid, and locale changes.
- Timezone, business-date, and daylight-saving boundaries where supported regions require them.
- Masking and non-persistence of sensitive data.
- Keyboard navigation, focus management, accessible names, announcements, contrast, zoom, and reduced motion.
- Server-side pagination, filters, sorting, empty results, and export scope.
- Responsive behavior at repository-supported viewports.

Tests must be deterministic. Control time, identifiers, locale, timezone, network behavior, and API fixtures. Do not rely on arbitrary sleeps. Avoid snapshots that hide behavioral assertions or store sensitive and unstable output.

Do not test only that a button exists. For sensitive actions, assert permission presentation, confirmation, request shape, duplicate protection, authoritative response handling, cache reconciliation, audit/reference display, and error recovery as applicable.

## API mocks and test data

- Use contract-shaped synthetic fixtures.
- Keep mock behavior aligned with approved schemas, including error and transitional states.
- Do not create mocks that make impossible backend states appear supported without documenting why.
- Include realistic but fictitious institution, customer, account, transaction, case, and user identifiers.
- Do not copy production payloads into fixtures, even after superficial masking.
- Make exceptional states easy to exercise locally and in tests.
- Prefer a shared, typed fixture builder only when it improves clarity and contract maintenance.

## Documentation and traceability

For material behavior, preserve traceability:

```text
Requirement ID -> User Story -> design/decision -> API contract -> UI implementation -> tests -> operational evidence
```

- Mention applicable requirement and story IDs in work items, tests, stories, or supporting documentation where practical.
- Update API usage documentation, UI states, configuration, environment variables, and runbooks with behavior changes.
- Document permission, tenant, approval, timeout, concurrency, and recovery behavior for sensitive workflows.
- Record consequential cross-portal, security, caching, state-management, or accessibility decisions in an ADR when the repository establishes that process.
- Add a child `AGENTS.md` when a portal or shared package requires durable local rules that do not belong globally.
- Do not copy entire source documents into code comments or agent instructions. Link to authoritative material and record only the local decision needed to implement and verify the feature.

## TypeScript and React standards

- Keep TypeScript strict and model domain states explicitly.
- Prefer discriminated unions for mutually exclusive workflow and result states.
- Do not use non-null assertions or type casts to silence unresolved contract uncertainty.
- Avoid `any`; use `unknown` at untrusted boundaries and narrow it safely.
- Validate data at trust boundaries when static types alone cannot guarantee runtime shape.
- Use clear banking and operational language. Avoid abbreviations that obscure meaning.
- Keep components cohesive and props minimal.
- Prefer controlled domain wrappers around generic components rather than scattering domain interpretation across screens.
- Keep effects focused on synchronization with external systems. Do not use effects for derived state that can be computed during render.
- Clean up subscriptions, timers, and requests.
- Use stable identifiers for keys; never use a mutable array index when rows can change.
- Do not suppress lint, hook dependency, accessibility, or type errors without a narrow documented reason.
- Comments explain intent, security constraints, domain meaning, or surprising trade-offs; they do not restate syntax.
- Remove dead code instead of commenting it out.

## Configuration and environments

- Commit `.env.example` files with non-secret placeholders only.
- Treat every browser-exposed environment variable as public.
- Validate required configuration at startup or build time with clear, non-sensitive errors.
- Do not silently point a development build at production services.
- Make environment identity visible enough to prevent operator confusion without exposing infrastructure details.
- Keep privileged integration credentials on secured backend infrastructure.
- Do not add real test accounts, passwords, API keys, certificates, or tokens to scripts or documentation.

## Dependency, build, and supply-chain safety

- Use the repository-pinned runtime and package manager.
- Preserve lockfile integrity and review dependency changes.
- Do not run package install scripts from untrusted packages without understanding their impact.
- Prefer maintained packages with clear ownership and licensing.
- Keep CI reproducible and fail on type, lint, test, build, secret-scan, and critical security issues according to approved policy.
- Do not disable a security check or pin a vulnerable version merely to make CI green.
- Document and time-bound any approved exception.

## Prohibited shortcuts

Do not:

- Treat UI visibility as authorization.
- Calculate or mutate authoritative balances, fees, limits, approvals, or transaction outcomes in the frontend.
- Retry an ambiguous financial command blindly.
- Present a timeout as a confirmed failure or success.
- Use floating-point arithmetic for authoritative money calculations.
- Trust tenant, branch, user, role, permission, fee, balance, ownership, or approval values supplied by editable client state.
- Store secrets, tokens, or sensitive banking data in unsafe browser persistence.
- Expose stack traces, internal errors, private endpoints, or sensitive identifiers.
- Render unsanitized HTML.
- Disable security, accessibility, validation, type checking, linting, or tests to make a feature pass.
- Add speculative abstractions or infrastructure for an unapproved future requirement.
- Edit sibling repositories, especially `../backend`, unless explicitly assigned that work.
- Claim proposed scripts, packages, portals, tests, or directories already exist.
- Use real customer or production data in development, tests, demos, screenshots, or documentation.

## Definition of done

A frontend-admin change is complete only when:

- The approved requirement and acceptance criteria are implemented in the correct portal or package.
- Backend authority, financial integrity, authorization, tenant isolation, segregation of duties, and privacy are preserved.
- All applicable UI states and recovery paths are implemented.
- Relevant unit, component, integration, contract, end-to-end, and accessibility tests pass.
- Formatting, linting, type checking, build validation, and configured security checks pass.
- Keyboard navigation, focus behavior, semantics, responsive layout, and supported browser behavior are verified proportionately.
- API contract use, command idempotency, timeout behavior, concurrency, cache invalidation, and unknown outcomes are handled where applicable.
- No secrets, live customer data, unsafe screenshots, temporary files, generated noise, backend edits, or unrelated changes are included.
- Documentation, traceability, configuration examples, stories, and runbooks are updated as needed.
- Remaining assumptions, limitations, unrun checks, and risks are stated explicitly.

Once the workspace is scaffolded, the normal verification sequence should use the repository's actual scripts and be equivalent to:

```powershell
pnpm install --frozen-lockfile
pnpm format:check
pnpm lint
pnpm typecheck
pnpm test
pnpm build
pnpm test:e2e
```

Run only scripts that actually exist, using the pinned package manager and documented environment. At the current documentation-only stage, verify content and repository diff honestly rather than inventing a successful application build.

## Review priorities

When reviewing frontend-admin work, prioritize findings in this order:

1. Incorrect, duplicate, missing, or misleading financial and approval outcomes.
2. Privilege escalation, cross-tenant exposure, sensitive-data leakage, unsafe session behavior, or bypassed step-up controls.
3. Blind retries, stale authority, concurrency loss, cache contamination, or incorrect unknown-outcome handling.
4. Contract breakage, destructive configuration behavior, audit/reference loss, or unrecoverable operational flows.
5. Accessibility barriers in critical workflows and misleading status presentation.
6. Missing tests, observability, documentation, or recovery evidence.
7. Maintainability, performance, and style issues with concrete user or operational impact.

Do not approve a privileged or money-related flow solely because its happy path renders and submits successfully.
