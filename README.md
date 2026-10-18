# Core Banking Platform — Frontend Admin

Administrative and staff-facing web applications for the Core Banking Platform.

> **Project status:** Active development by a volunteer team. The applications are **not approved for production banking use**, handling real customer data, or processing real funds.

## Scope and repository boundaries

`frontend-admin` contains internal banking web portals for bank staff, administrators, risk/compliance analysts, finance teams, and authorized auditors.

| Application | Users | Core workflows |
| --- | --- | --- |
| Staff Operations Portal | Tellers, customer-service officers, account officers, supervisors, operations managers | Onboarding, customer 360, KYC, account operations, cash services, service requests, branch work queues, maker-checker approvals |
| System Administration Portal | Platform/institution/security/product/operations administrators | Institutions, branches, products, pricing, limits, policies, users, roles, workflows, feature flags, integrations, branding |
| Risk, Compliance & Fraud Portal | AML/fraud/risk analysts, investigators, security/compliance officers | Alerts, customer risk, sanctions/PEP reviews, cases, evidence, investigations, regulatory workflows, audit access |
| Finance, Reconciliation & Reporting Portal | Finance/reconciliation/settlement officers, accountants, auditors, management | GL/trial balance/P&L, settlement, reconciliation, exceptions, financial close, reporting, exports |

Other repositories remain separate:

- `frontend-user`: individual and corporate internet banking (customer-facing web).
- `frontend-mobile`: Flutter customer and agent banking apps (Android/iOS).

The backend is the source of truth for user privileges, workflow approval, financial calculations, balances, audit events, and transaction status. Frontends only access approved APIs.

## Architecture and implementation instructions

Before implementing a feature, read:

1. [`AGENTS.md`](AGENTS.md) for repository-wide instructions and non-negotiable safety rules.
2. [`docs/architecture/FRONTEND_ADMIN_ARCHITECTURE.md`](docs/architecture/FRONTEND_ADMIN_ARCHITECTURE.md) for the target portal, package, runtime, security, accessibility, state, and delivery architecture.
3. [`docs/design/UI_DESIGN_DIRECTION.md`](docs/design/UI_DESIGN_DIRECTION.md) for visual identity, canonical layouts, portal navigation, banking components, interaction language, and anti-generic UI rules.
4. [`docs/implementation/README.md`](docs/implementation/README.md), the applicable phase overview, and the applicable epic document for executable scope, backend dependencies, UI states, tests, and acceptance gates.

Implementation follows the platform phases from engineering foundation through banking foundation, regulated operations, growth channels, advanced banking, and governed optimisation. A documented feature is planned scope until its epic is approved and its implementation evidence is complete.

## Objectives

- Provide secure, reliable internal operational workflows across branches/institutions.
- Keep staff permissions and maker-checker responsibilities explicit.
- Support accessibility, keyboard-heavy data entry, and large operational datasets.
- Maintain consistent design patterns across portals.
- Keep portals independently deployable while sharing approved components and API contracts.
- Support multiple institutions, currencies, regions, languages, and branding configurations.

## Primary features

### Staff Operations Portal

- Customer search and 360-degree profiles
- Individual/corporate onboarding and KYC management
- Account opening, maintenance, and restrictions
- Cash deposits and withdrawals where approved
- Transfers, transaction enquiries, receipts, and statements
- Service requests, complaints, and branch operational dashboards
- Maker-checker approvals, work queues, teller balancing, and audit context

### System Administration Portal

- Institution, branch, region, currency, calendar, and holiday configuration
- Banking product, pricing, fee, limit, and policy configuration
- User administration, roles/permissions, segregation of duties, and approval rules
- Workflow, feature flag, country pack, and branding configuration
- API client/integration configuration and notification templates
- Environment and audit policy settings, subject to authorization

### Risk, Compliance & Fraud Portal

- AML/fraud alert dashboards and case assignment
- Customer and transaction risk investigation
- Sanctions, PEP, and watchlist screening and review
- Evidence handling, notes, escalation, approvals, and audit trails
- Regulatory reporting, false-positive review, and model monitoring where provided by backend services

### Finance, Reconciliation & Reporting Portal

- General ledger, trial balance, P&L, and balance sheet reports
- Settlement dashboards and reconciliation workbench
- Suspense, unmatched entries, and provider/Nostro reconciliation
- Financial-close controls and period-end approvals
- Management/regulatory reports and safe export of permitted data

Features listed here are **planned scope**, not a statement that each feature is already implemented.

## Recommended stack

- Next.js, React, TypeScript, and Tailwind CSS
- React Hook Form and Zod for forms and client-side feedback
- TanStack Query for API state; TanStack Table for operational tables
- OpenAPI-generated typed API clients where practical
- Approved authentication and permissions utilities
- Playwright for end-to-end tests; Jest or Vitest for unit/component tests
- Storybook for shared components; ESLint and Prettier for quality

Use the versions and package manager pinned by the repository configuration.

## Proposed repository structure

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
│   └── utilities/
├── docs/
│   ├── architecture/
│   ├── authentication/
│   ├── approvals/
│   ├── security/
│   ├── testing/
│   └── deployment/
├── .github/workflows/
├── CONTRIBUTING.md
├── CODE_OF_CONDUCT.md
├── SECURITY.md
├── LICENSE
└── README.md
```

This is a proposed design, not an assertion that these directories currently exist. Reuse packages where it makes sense, without coupling unrelated deployments or copying sensitive configuration across applications.

## Local setup

Prerequisites: Git, repository-approved Node.js LTS, the pinned package manager, and access to development APIs/test identities.

Example commands **for a pnpm workspace once scaffolded**:

```bash
pnpm install
pnpm --filter staff-operations dev
pnpm --filter system-admin dev
pnpm --filter risk-compliance dev
pnpm --filter finance-reporting dev
```

Workspace package names and ports should be confirmed against each app's `package.json`. Do not switch package managers or regenerate lockfiles without approval.

### Environment variables

Provide `.env.example` with **public, non-secret** placeholders only:

```dotenv
NEXT_PUBLIC_APP_NAME=Core Banking Platform — Admin
NEXT_PUBLIC_API_BASE_URL=http://localhost:5000
NEXT_PUBLIC_ENVIRONMENT=development
```

`NEXT_PUBLIC_` exposes its value in browser code. Never put credentials, API secrets, signing keys, or privileged integration tokens in public environment variables. Any server-only secrets must be managed using approved environment/secret management. Use synthetic data for development.

## Authentication, authorization, and approvals

- Authenticate through approved identity services with MFA/step-up verification where required.
- Treat authorization as **backend-enforced**; UI checks improve UX but do not provide final access control.
- Scope every customer, branch, account, report, and workflow action to the authorized institution and role.
- Apply segregation of duties: users must not approve their own restricted submissions.
- Show maker/checker identity, approval level, reason, audit reference, and current state when permitted.
- Protect sessions against fixation, CSRF, XSS, and unintended exposure; adopt approved cookie/session patterns.
- Never assume a user can invoke an endpoint simply because the interface contains a button.

## Financial and operational workflows

For sensitive changes (e.g. account restrictions, transfer instructions, product/fee edits, user permission changes):

1. Capture data with clear validation and permitted context.
2. Show the previous and proposed values when applicable.
3. Explain the effects, fees, limits, and required approvals.
4. Present a review/confirmation step.
5. Submit once using backend-supported idempotency where relevant.
6. Show pending/approved/rejected/processing/failed/unknown states accurately.
7. Provide backend-generated references and audit metadata.

A network timeout does **not** mean a banking operation failed. Query authoritative status rather than blindly replaying requests. The backend must determine balances, fees, transaction posting, and approval eligibility.

## Operational UI and accessibility

- Prioritize readable data, keyboard navigation, clear focus and keyboard shortcuts where appropriate.
- Aim for WCAG 2.1 AA or the later approved standard.
- Provide loading, empty, error, restricted, session-expired, review, and success states.
- Use server-side pagination/filtering for large transaction histories and audit tables.
- Include audit-friendly timestamps, currency codes, status labels, references, and time-zone context.
- Never rely on color alone to communicate state or risk.
- Design primarily for desktop/laptop but remain usable on supported tablet/mobile browser sizes.
- Confirm irreversible/high-risk actions before submission.

## API integration and error handling

- Use approved authenticated APIs only; never access databases directly from the browser.
- Prefer typed, generated API clients and explicit request/response contracts.
- Handle authorization errors, validation failures, timeouts, connection loss, account restrictions, conflicting changes, and duplicate submissions.
- Implement safe request cancellation, correlation IDs, and narrowly scoped retry policies.
- Sanitize displayed errors: never show stack traces, database internals, secrets, or private identifiers.
- Backend enforcement and audit logging remain mandatory for all sensitive operations.

## Security and data protection

**Never commit or log:** passwords, OTPs, session tokens, full card data/CVV, full BVN/NIN, production API keys, private certificates, or live customer documents.

- Minimize browser caching and client-side persistence of sensitive financial data.
- Avoid sensitive values in local/session storage, URLs, analytics, browser logs, and screenshots.
- Protect exports with authorization, minimal data, controlled retention, and audit trails.
- Apply appropriate CSP, secure cookie, CSRF, XSS, and clickjacking protections.
- Treat uploaded KYC/evidence files as sensitive; use backend-supplied secure upload/download mechanisms.
- Use redacted/synthetic examples in issues, pull requests, fixtures, and screenshots.
- Report vulnerabilities privately through `SECURITY.md`.

## Testing

Test utility/validation logic, components, integrations, role restrictions, institution scoping, approvals, and end-to-end workflows. Prioritize:

- Sign-in, MFA, logout, and session expiration
- Customer onboarding and account opening
- Cash deposit/withdrawal UI and transaction-status reconciliation
- Maker-checker: submit, approve, reject, self-approval denial, and expired approval
- Permission escalation attempts and cross-institution isolation
- Fraud case creation/escalation and evidence access
- Reconciliation exception handling and report export
- Timeout, network interruption, duplicates, partial failure, and unknown outcomes
- Accessibility, keyboard navigation, responsive layout, and screen-reader compatibility

Typical workspace checks (once configured):

```bash
pnpm lint
pnpm test
pnpm build
```

Also run configured type checks, Playwright suites, accessibility checks, and security scans. Do not assume these scripts exist until scaffolded.

## CI/CD and deployment

Each portal should be built and deployed independently where practical. CI should cover formatting, linting, type checking, tests, dependency/secret scans, build validation, and approved deployments. Environments may include development, test, staging, UAT, and production. Keep privileged services and integration credentials on secured backend infrastructure.

## Contributing

This is currently an **unpaid volunteer project**. Participation is not employment and does not guarantee future compensation.

- Read `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`, and `SECURITY.md`.
- Do not push directly to `main`.
- Use branches such as `feature/TASK-0301-customer-search` or `fix/TASK-0302-approval-state`.
- Use conventional commits, e.g. `feat: add reconciliation exception filters`.
- PRs should document issue/task, portal/module, screenshots with synthetic data, API dependencies, testing, responsive behavior, accessibility, and security considerations.

A change is done only after approved requirements, functional tests, auth/permission checks, all necessary UI states, accessibility, security review, documentation, and code review have been completed.

## License and disclaimer

See `LICENSE` when included; contributors must have permission to submit their code and assets.

This repository is for learning, research, and engineering collaboration. It must **not** process real banking transactions or real customer data until security, legal, regulatory, privacy, accessibility, penetration-testing, performance, disaster-recovery, and production-readiness approvals have been completed.
