---
title: UI Design Direction - Core Banking Admin
version: 1.0
status: Ready for review
owners: [Product Design, Frontend Platform, Accessibility, Security]
primary_locale: en-NG
last_updated: 2026-10-17
---

# UI Design Direction - Core Banking Admin

## 1. Purpose and product vision

Create a secure, efficient, accessible, and auditable workstation for bank staff and authorized administrators. Complex financial operations must remain understandable without hiding critical information.

**North star:** Precision, clarity, trust, and operational speed.

This is not a consumer-neobank interface or a generic admin template. Avoid promotional hero sections, oversized typography, decorative gradients, excessive animation, indiscriminate card grids, ornamental charts, and empty whitespace that reduces operational efficiency. Optimize for trained employees who use the system for hours every day.

Primary locale is Nigeria (`en-NG`, `NGN`, `Africa/Lagos`), while architecture and components must support multiple currencies, locales, timezones, country packs, and institution branding.

## 2. Design principles

1. **Accuracy over decoration.** Money, dates, identities, transaction status, data freshness, and approval authority are unambiguous.
2. **Actionable density.** Present substantial information with strong hierarchy, alignment, grouping, and deliberate whitespace.
3. **Pattern consistency.** Similar operations use the same component, placement, terminology, status, confirmation, and recovery patterns.
4. **Safety by design.** Help operators detect mistakes before submitting sensitive, financial, or irreversible actions.
5. **Role-aware, server-authorized.** Present permitted work without treating hidden or disabled UI as a security boundary.
6. **Auditability.** Show initiator, approver, time, changes, reason, references, and current state when permitted.
7. **Accessible by default.** Target WCAG 2.2 AA with keyboard-complete critical workflows.
8. **Desktop-first, responsively complete.** Optimize workstations while retaining review, validation, and approval safeguards at supported smaller sizes.
9. **Backend authority.** The UI never invents balances, fees, limits, posting outcomes, permissions, approval eligibility, risk decisions, or settlement state.
10. **Distinctive restraint.** Establish recognizable banking patterns through typography, density, composition, information hierarchy, and operational components rather than decoration.

## 3. Visual identity

### 3.1 Character

The visual character is **Modern Enterprise Banking**: calm, established, credible, precise, and highly functional.

The product identity should be recognizable through:

- A deep navy application frame.
- Crisp, information-dense white and pale-slate work surfaces.
- Deliberate blue action emphasis.
- Strong typographic and numeric alignment.
- Stable page composition and action placement.
- Banking-specific status, review, trace, approval, and amount components.
- Restrained use of portal accents that never replace semantic status colors.

### 3.2 Color tokens

| Token | Hex | Typical usage |
| --- | --- | --- |
| `--color-brand-900` | `#102A43` | Application frame, sidebar, major headings |
| `--color-brand-700` | `#183A63` | Secondary brand surfaces |
| `--color-action-600` | `#2563EB` | Primary action, selected navigation, active input |
| `--color-action-700` | `#1D4ED8` | Hover and pressed action |
| `--color-canvas` | `#F8FAFC` | Main application background |
| `--color-surface` | `#FFFFFF` | Tables, panels, cards, dialogs |
| `--color-border` | `#E2E8F0` | Dividers and borders |
| `--color-text` | `#0F172A` | Primary text |
| `--color-text-muted` | `#475569` | Secondary text |
| `--color-success` | `#15803D` | Confirmed successful or completed states |
| `--color-warning` | `#A16207` | Attention and pending states |
| `--color-danger` | `#B91C1C` | Failed, rejected, destructive states |
| `--color-info` | `#0369A1` | Informational states |

Actual foreground/background pairs require automated and manual contrast verification. Status color is never the only signal; use visible text and, where helpful, an icon.

Tenant branding may map approved brand tokens but cannot redefine status meaning, reduce contrast, hide focus, or make destructive actions resemble safe actions.

### 3.3 Portal signatures

All portals share the same shell, typography, geometry, components, and semantic colors. A portal may use one restrained accent for orientation:

| Portal | Suggested orientation accent | Character |
| --- | --- | --- |
| Staff Operations | Action blue | Fast, task-oriented, customer and branch focused |
| System Administration | Deep indigo | Controlled, configuration-focused, version-aware |
| Risk, Compliance and Fraud | Muted amber | Investigative, evidence-focused, cautious |
| Finance, Reconciliation and Reporting | Teal | Analytical, exact, period and exception focused |

Accents appear in portal identity, selected navigation, section markers, or chart series. They never override success, warning, danger, information, approval, or financial-state semantics.

### 3.4 Typography

- Primary font: Inter, with `system-ui`, `-apple-system`, `Segoe UI`, and `sans-serif` fallbacks.
- Tabular monetary and numeric values use `font-variant-numeric: tabular-nums`.
- Dense desktop body text defaults to 14px; smaller-screen forms may use 16px.
- Page headings use 24–28px semibold; section headings use 16–18px semibold.
- Field labels use 13–14px medium; supporting text uses 12–13px only where legible.
- Use sentence case. Do not use decorative typefaces or all caps for ordinary operational content.
- Page titles must not consume excessive vertical space or push primary work below the fold.

### 3.5 Spacing, geometry, and surfaces

- Use a 4px base scale: 4, 8, 12, 16, 24, 32, 40.
- Inputs and buttons use approximately 6px corners; panels and dialogs use 8–12px.
- Prefer borders, grouping, and background contrast over stacked shadows.
- Use shadows primarily for overlays and temporary elevation.
- Default content maximum width is 1600px; approved workbenches and tables may use the available width.
- Support comfortable and compact density modes. Compact mode cannot remove labels, focus indicators, necessary spacing, or applicable target-size support.
- Aim for at least 44x44 CSS pixels for touch-first controls. Dense pointer-first controls still require an accessible activation target under the approved WCAG policy.

### 3.6 Iconography and motion

- Use one approved line-icon family, initially Lucide unless superseded by an ADR.
- Icons supplement labels for critical actions; they do not replace them.
- Motion communicates orientation and feedback in approximately 120–200ms.
- Honor reduced-motion preferences.
- Do not animate balances or transaction totals, use confetti, or celebrate financial posting.

## 4. Application shell and portal navigation

### 4.1 Shared desktop shell

```text
┌────────────────────────────────────────────────────────────────────────────┐
│ Brand / Portal   Scoped Search        Institution / Branch   Help  Profile │
├────────────────────┬───────────────────────────────────────────────────────┤
│ Portal navigation  │ Breadcrumbs                                           │
│                    │ Page title                 Contextual primary action    │
│                    │ Scope, freshness, business date, relevant alert        │
│                    │                                                       │
│                    │ Filters / summary / workbench                         │
│                    │                                                       │
│                    │ Main table, form, detail, or split workspace           │
└────────────────────┴───────────────────────────────────────────────────────┘
```

- Expanded sidebar is approximately 240–264px and collapses to accessible icon navigation.
- Top bar is approximately 60–64px and shows user, active context, alerts, help, and session controls.
- Breadcrumbs appear on subpages.
- Page titles, scope/freshness information, and primary actions retain stable positions.
- Context changes warn about unsaved work and clear or partition sensitive cached state.
- Global or portal search is limited to authorized scope and supported resource types.
- Environment badges are conspicuous in development, demo, sandbox, UAT, and other non-production environments.

### 4.2 Independent portal navigation

Do not create one sidebar containing every platform module. Each independently deployable portal exposes only its responsibilities and deployed capabilities.

**Staff Operations**

- Workspace and My Tasks.
- Customers and KYC.
- Accounts and Deposits.
- Transactions and Payments.
- Teller, Cash, and Branch Operations.
- Credit and Recovery Work.
- Cases, Complaints, and Approvals.

**System Administration**

- Administration Overview.
- Institutions, Branches, Calendars, and Reference Data.
- Products, Pricing, Fees, Limits, and Policies.
- Users, Roles, Permissions, and Access Reviews.
- Workflows and Approval Matrices.
- Integrations, API Clients, Providers, and Templates.
- Branding, Features, and Environment Configuration.

**Risk, Compliance and Fraud**

- Risk Workspace.
- Alerts and Screening.
- AML and Fraud Cases.
- Customer and Transaction Risk.
- Rules, Models, Versions, and Monitoring.
- Regulatory Preparation and Evidence.

**Finance, Reconciliation and Reporting**

- Finance Workspace.
- General Ledger and Financial Statements.
- Reconciliation, Settlement, and Breaks.
- Suspense and Close Controls.
- Treasury, Liquidity, and FX when deployed.
- Reports, Exports, Audit, and Traceability.

An approved portal switcher may link between deployments. It must preserve authentication safely, re-evaluate permissions, communicate context, and never rely on cross-app internal imports. Never display dead-end navigation for undeployed capabilities.

## 5. Canonical page grids

Generated and implemented screens use these compositions unless a documented workflow requires another pattern.

### 5.1 Index and work-queue page

```text
Breadcrumbs
Page title + scope/freshness                         Primary action
Short operational description
Alert or policy notice, only when actionable
Filter bar: search | primary filters | saved view | density | export
Summary strip: small number of scoped counts/totals
Full-width table or queue
Pagination and result scope
```

Avoid surrounding every filter, count, and table with separate floating cards. Use one coherent work surface.

### 5.2 Record detail page

```text
Breadcrumbs
Identity header: name/reference | status | scope      Primary safe action
Critical restriction/risk/approval banner
Summary facts in aligned definition grid
Tabs or anchored sections
Main record detail                                  Context rail
Timeline / related activity                         Audit / references
```

Keep identity, status, restrictions, and authoritative references visible without repeating them in decorative cards.

### 5.3 Form and configuration page

```text
Breadcrumbs
Page title + draft/version state                     Save/continue action
Step indicator for long workflows
Single-column form or clearly grouped two-column sections
Inline validation and policy guidance
Sticky review summary only when it materially reduces error
Cancel | Save draft | Continue / Review
```

### 5.4 Review and approval page

```text
Request identity, maker, age, scope, approval level
Risk/restriction/limit warnings
Before-and-after diff or transaction breakdown
Evidence, notes, and audit context
Decision panel: Reject with reason | Approve
```

The decision panel remains distinct from the evidence and cannot obscure the item being approved.

### 5.5 Dense investigation or reconciliation workbench

```text
Queue/table on the left or top
Selected record detail in primary pane
Evidence, timeline, or comparison in secondary pane
Persistent scope, totals, variance, and freshness
Contextual actions tied to the selected authoritative record
```

Panels collapse predictably at smaller widths and retain a clear route back to the queue.

### 5.6 Dashboard

Dashboards are operational cockpits, not marketing landing pages. Use a restrained KPI strip, prioritized work queue, exception/freshness notices, one or two decision-support visualizations with accessible data alternatives, recent material activity, and permission-aware quick actions. Avoid walls of interchangeable cards.

## 6. Role-oriented dashboard direction

| Role | Highest-priority information |
| --- | --- |
| Teller | Till position, limits, shift state, pending cash work |
| Customer Service | Scoped search, KYC tasks, onboarding drafts |
| Operations Officer | Pending/failed transactions, investigations, exceptions |
| Approver or Supervisor | Approval queue, monetary impact, risk flags, ageing |
| Finance or GL Officer | Period, unbalanced work, settlement and reconciliation exceptions |
| Compliance or Auditor | Review queues, restrictions, evidence, audit activity |
| System Administrator | Configuration versions, access requests, publication and system health |

Never assume a role may see institution-wide balances or private customer information. Dashboard data remains permission- and scope-aware.

## 7. Essential banking page patterns

### 7.1 Customer 360

- Identity header: name, customer ID, type, verification state, restrictions, branch.
- Tabs or sections: Overview, Accounts, Transactions, Documents, KYC, Relationships, Notes, Audit.
- Restrictions and risk warnings precede financial actions.
- Sensitive identifiers are masked by default; approved reveal is auditable.
- Verification and risk information shows last-updated time and source state.

### 7.2 Accounts

- Search/filter by permitted account identifier, customer, product, status, branch, and currency.
- Detail header identifies account name, masked number, status, type, currency, and booking branch.
- Distinguish ledger, available, held, lien, blocked, and uncleared values when contracts support them.
- Show restrictions, mandates, statement history, activity, and audit references.
- Freeze, unfreeze, reactivate, close, and limit actions require explicit reason and backend-defined controls.

### 7.3 Transactions and payments

- Lists include timestamp, reference, source, destination, amount, currency, type, status, channel, and initiator when permitted.
- Detail shows the exact backend lifecycle and reference chain.
- Technical response codes are secondary, expandable information with a safe explanation.
- Cancel, reject, reverse, refund, recall, dispute, requery, and retry remain distinct.
- Success or posting is never shown until authoritative state confirms it.

### 7.4 Maker-checker approvals

- Separate My Requests, Awaiting My Approval, Completed, and Rejected.
- Show initiator, action, target, monetary impact, scope, time, age/deadline, and risk flags.
- Show before/after values or a clear transaction breakdown.
- Rejection requires a reason when specified by contract.
- Unavailable decisions explain the safe reason without exposing hidden security rules.
- Final decision views are immutable and show decision maker, time, comment, and reference.

### 7.5 General ledger and reconciliation

- GL tables show code, description, hierarchy, currency, debit, credit, net, period, and as-of time.
- Draft journal forms may show exact client-side debit/credit feedback using approved decimal handling; only backend validation and posting are authoritative.
- Reconciliation distinguishes matched, unmatched, duplicate, disputed, investigating, proposed resolution, and resolved states with exact variance.
- Keep period, business date, currency, data source, and locked/closed warnings visible.
- Accountants must be able to inspect entries; charts never replace the table.

### 7.6 Teller operations

- Keep branch, teller ID, shift, till currency, authoritative balance, limits, and freshness prominent.
- Cash review shows denomination and amount details when supplied by backend contract.
- High-risk operations show dual-control and approval state.
- Duplicate protection combines an in-flight UI state with backend idempotency.

### 7.7 Loans and credit

- Show application stage, principal, currency, approved interest model, schedule, fees, tenure, collateral, arrears, and effective dates from backend contracts.
- Separate projections from posted accounting entries.
- Show calculation basis and authoritative source without recomputing the outcome.
- Restructure, write-off, disbursement, and recovery actions require explicit review and approval journeys.

## 8. Tables and data-heavy interaction

Tables are first-class operational components.

- Use server-side pagination, filtering, and sorting for large datasets.
- Use sticky headers, optional pinned identifiers, stable row identity, and predictable alignment.
- Right-align money and numeric quantities; left-align text; use tabular numerals.
- Dates include applicable timezone; exact timestamp is available in detail or an accessible disclosure.
- Support controlled density, approved column customization, and non-sensitive saved views.
- Rows are keyboard navigable with clearly labeled actions.
- Preserve critical identifiers during horizontal scroll; do not force every important field off-screen.
- Loading, empty, no-results, partial, stale, access-denied, and error states are visually distinct.
- A total states its scope: current page, selected records, filtered result, or complete result.
- Do not load an unbounded result set into the browser.

Exports are generated by an approved backend report/export service and delivered through an authorized, expiring flow. The UI requests a bounded scope and displays run state, classification, expiry, and audit reference. It does not construct an unbounded CSV/XLSX export from browser data. Export permissions, masking, formula-injection protection, retention, and audit remain backend-enforced.

## 9. Forms and workflows

- Use a single column for short forms; use labeled sections or a stepper for complex onboarding.
- Keep labels visible above controls; placeholders are never the only label.
- Mark optional and required fields using approved conventions.
- Group related inputs semantically.
- Validate inline with actionable messages and repeat authoritative validation on the backend.
- Save long drafts through approved backend persistence, never insecure browser storage.
- Use precise actions: Save Draft, Continue, Review, Submit for Approval, Approve, Reject, Cancel.
- Review high-risk submissions with target party, destination, amount, currency, fees, effective date, scope, and approval requirements.
- Preserve safe draft state after recoverable errors.
- A success toast is never the sole confirmation of a financial command; show a durable reference and authoritative pending/final state.

### 9.1 High-risk or irreversible operations

For restrictions, reversals, privileged configuration, cash disbursement, adjustments, publication, and similar actions:

1. Name the precise effect and affected entities.
2. Show current authoritative values and relevant warnings where permitted.
3. Require explicit confirmation and reason where applicable.
4. Perform step-up or approval under backend policy.
5. Submit one intended command using approved idempotency.
6. On timeout, show outcome unknown and query status rather than resubmitting.
7. Confirm only from authoritative state and show transaction/audit reference.

## 10. Status language and microcopy

Use explicit text plus semantic color and optional icon. Display labels map to approved backend states and are not a substitute state machine.

| Context | Illustrative display labels |
| --- | --- |
| Account | Active, Dormant, Frozen, Restricted, Closed |
| Payment | Draft, Pending Approval, Processing, Posted, Failed, Uncertain, Reversed, Disputed |
| Loan | Draft, Under Review, Approved, Disbursed, Performing, In Arrears, Closed |
| KYC | Not Started, In Progress, Pending Review, Verified, Rejected, Expired |
| Reconciliation | Matched, Unmatched, Investigating, Resolution Pending, Resolved |

Preferred copy is concrete, calm, and neutral:

| Situation | Preferred | Avoid |
| --- | --- | --- |
| Maker-checker submission | `Submit for approval` | `Execute now` |
| Pending payment | `Transfer submitted. Awaiting approval.` | `Transfer successful!` |
| Posted payment | `Transfer posted. Reference: TRX-...` | `Done!` |
| Rejection | `Rejected by approver. Reason: ...` | `Something went wrong` |
| Insufficient access | `You do not have permission to approve this transaction.` | `403` |
| Recoverable validation | `Enter a valid 10-digit account number.` | `Invalid input` |
| Duplicate command | `This request has already been received. View its current status.` | `Try again` |
| Ambiguous timeout | `We could not confirm the outcome. Checking the current status...` | `Transfer failed` |

## 11. Currency, numbers, identifiers, and time

- Nigeria default presentation is `₦1,250,000.00` for an NGN-only context.
- Mixed-currency views include ISO codes such as `NGN`, `USD`, and `GBP`.
- Preserve backend precision; do not silently round or hide a discrepancy.
- Never use binary floating point for authoritative money. Money input remains an exact string or approved decimal representation, and backend calculation/validation remains authoritative.
- Account numbers, references, BVNs/NINs, and other identifiers are strings: preserve leading zeros and never add numeric separators.
- Use clear dates such as `17 Oct 2026` and include timezone/offset where ambiguity exists.
- Distinguish browser-local time, institution time, transaction time, business date, posting date, value date, and settlement date.
- Operational data has an explicit as-of or last-refreshed indicator.

## 12. URL, filter, and saved-view policy

URL state may contain non-sensitive pagination, sort, selected tab, date range, public status code, and approved enumerated filters when it improves navigation or sharing.

Do not place customer names, account/card numbers, BVN/NIN values, phone/email, free-text notes, case evidence, document identifiers, access tokens, secrets, or sensitive search terms in URLs. Sensitive filters remain in memory or use an approved opaque server-side saved-view identifier. Saved views are scoped to user and institution and must not leak prior-context data.

## 13. Security and privacy UX

- Use approved MFA/step-up for sensitive actions and handle expiry clearly.
- Never expose credentials, PINs, OTPs, full sensitive identifiers, private keys, or secret tokens in UI logs, analytics, errors, screenshots, or fixtures.
- Minimize PII in tables, alerts, and notifications; mask according to backend policy.
- Explain denial without exposing protected policy internals or third-party details.
- Preserve only non-sensitive navigation context through session expiry.
- Show non-production environment identity clearly.
- Never let the UI invent effective dates, approval identity, balance, posting state, provider finality, or settlement state.

## 14. Accessibility

Target WCAG 2.2 AA.

- Make navigation, menus, filters, tables, dialogs, split workbenches, and all actions keyboard reachable.
- Provide visible focus and deterministic focus management after overlays, validation, route changes, and dynamic updates.
- Meet contrast requirements for text and relevant non-text indicators.
- Associate fields with labels, instructions, errors, and required state.
- Provide error summaries linked to invalid fields.
- Use semantic headings, landmarks, real tables for tabular data, and accessible live announcements.
- Support zoom and reflow; allow necessary grid scrolling without keyboard traps.
- Respect reduced motion.
- Provide text/table alternatives for charts and diagrams.

## 15. Responsive behavior

| Breakpoint | Experience |
| --- | --- |
| `>= 1440px` | Full sidebar, dense tables, multi-panel workbenches |
| `1024–1439px` | Full/collapsible sidebar, two-column summaries/forms |
| `768–1023px` | Collapsed navigation, simplified toolbars, preserved review flows |
| `< 768px` | Drawer navigation, stacked summaries, simplified list/detail |

Consequential operations retain the same validation, information, confirmation, and approval safeguards on every supported size. Do not hide mandatory content to make a layout fit.

## 16. Component system

### 16.1 Foundation components

`AppShell`, `PortalSwitcher`, `Sidebar`, `TopBar`, `Breadcrumbs`, `PageHeader`, `PageSection`, `ScopeBar`, `FreshnessIndicator`, `SearchInput`, `DateRangePicker`, `InstitutionSwitcher`, `BranchSwitcher`, `CurrencyAmount`, `Identifier`, `StatusBadge`, `PermissionBoundary`, `Skeleton`, `EmptyState`, `NoResultsState`, `RestrictedState`, `ErrorState`, `ConfirmationDialog`, `AuditTimeline`.

### 16.2 Banking components

`KpiStrip`, `TransactionTable`, `TransactionStatus`, `AccountSummary`, `CustomerIdentityPanel`, `KycStatusPanel`, `BalanceBreakdown`, `MoneyInput`, `MoneyBreakdown`, `ApprovalQueue`, `ApprovalDecisionPanel`, `BeforeAfterDiff`, `PostingReview`, `GlEntryTable`, `ReconciliationVariance`, `TillSummary`, `LoanRepaymentSchedule`, `RiskAlertBanner`, `EvidencePanel`, `ReferenceChain`, `UnknownOutcomePanel`.

### 16.3 Component states

Design meaningful combinations of default, hover, focus, selected, disabled/unavailable with explanation, loading, empty, no results, stale, partial, success, validation error, server error, unknown outcome, and permission denied.

### 16.4 Primitive policy

Accessible Radix UI primitives or shadcn-style source components may be considered as implementation foundations after dependency and license review. They are not the visual design system.

- Do not copy stock shadcn themes, layouts, sample dashboards, default radii, or generic card compositions directly.
- Wrap and adapt primitives behind repository-owned APIs.
- Apply approved tokens, density, focus, error, status, and banking interaction contracts.
- Remove unused variants and inaccessible defaults.
- A primitive must not leak directly across applications when a shared bank-owned component exists.

## 17. Frontend implementation alignment

The approved target is a pnpm monorepo using Next.js, React, TypeScript, Tailwind CSS with CSS-variable tokens, TanStack Query, TanStack Table, React Hook Form, Zod, approved accessible primitives, Lucide icons, and the configured test stack.

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
│   └── testing/
└── docs/design/
```

Generated screens and code follow this repository structure. Do not introduce Vite or another application runtime without an approved architecture decision.

## 18. Screen design contract

Every new screen or design image specifies:

1. User goal and permitted actor.
2. Owning portal and route or feature.
3. Institution, branch, customer, account, transaction, or case scope.
4. Primary action, if one exists.
5. Supporting actions and safe priority.
6. Backend contract and authoritative data source.
7. Permission, step-up, and approval behavior.
8. Loading, empty, no-results, pending, stale, conflict, failed, unknown, success, and denial states that apply.
9. Audit, correlation, actor, time, freshness, and reference signals.
10. Desktop, smaller-screen, keyboard, focus, and screen-reader behavior.
11. Sensitive-data classification and masking.
12. Acceptance criteria for correctness, failure recovery, and duplicate prevention.

Design images must be labeled with portal, screen name, viewport, density, state, and version. Synthetic content is mandatory.

## 19. Anti-generic UI rules

Do not:

- Use a generic dashboard template as the product shell.
- Build every section as a floating rounded card.
- Use decorative gradient backgrounds, glass effects, neon accents, or consumer-finance illustrations in operational workflows.
- Use oversized headings, slogans, or empty hero regions on staff pages.
- Add charts because a page has numbers; every chart must support an operator decision and provide a data alternative.
- Hide core data behind hover-only interactions, carousels, or gratuitous drill-down.
- Place primary actions inconsistently between pages of the same archetype.
- Create one-off status colors, date formats, money formats, table controls, confirmation dialogs, or empty states.
- Use icon-only critical actions, ambiguous kebab menus for the primary task, or generic text such as `Submit`, `Done`, and `Something went wrong` when precise language exists.
- Copy stock component-library examples without adapting tokens, density, content, states, and banking semantics.
- Mix unrelated portal navigation or duplicate the same business capability in multiple apps without an approved ownership decision.

## 20. AI coding and design-agent instructions

Before creating or changing a screen:

- Read `AGENTS.md`, the architecture, this document, the implementation phase/epic, and the approved design artifact.
- Reuse tokens, components, page grids, layout, terminology, formatting, and interaction patterns.
- Use portal-specific navigation and the restrained portal accent; retain shared shell and semantic colors.
- Prioritize information architecture, data scope, table usability, status, freshness, review, and safe recovery.
- Supply meaningful loading, empty, no-results, stale, failure, unknown-outcome, and denial states.
- Do not mock live balances or completed posting outcomes in production paths.
- Do not hard-code permissions, thresholds, rates, limits, product terms, or state machines.
- Document the backend contract that validates permission, idempotency, concurrency, and authoritative outcome for sensitive actions.
- Use clearly synthetic data in fixtures and generated images.
- Reject a generated design that violates the canonical grid, introduces an unapproved visual language, or resembles a generic admin/analytics template.

## 21. Design acceptance checklist

- [ ] Correct portal, shell, navigation, breadcrumbs, and canonical page grid.
- [ ] Recognizable enterprise-banking identity without decorative consumer patterns.
- [ ] Approved tokens, typography, density, geometry, icons, and portal accent.
- [ ] Correct business terminology, scope, freshness, money, dates, and status.
- [ ] Primary and supporting actions are consistently placed and precisely named.
- [ ] Review, confirmation, approval, conflict, timeout, and unknown outcomes are represented safely.
- [ ] Role-aware presentation with mandatory backend authorization.
- [ ] Sensitive data is masked and excluded from URLs, persistence, telemetry, fixtures, and unsafe exports.
- [ ] Tables and workbenches remain efficient, keyboard-accessible, and understandable at supported widths.
- [ ] WCAG 2.2 AA evidence covers controls and information.
- [ ] Audit, correlation, transaction, and support references appear where applicable.
- [ ] Long names, large balances, multiple currencies, timezones, translations, and edge-case statuses have been tested.
- [ ] No stock template composition, unrelated design system, or unjustified one-off component appears.

## 22. Non-goals

This document does not define complete business requirements, database schemas, accounting treatment, regulatory obligations, backend authorization, or compliance certification. Those remain in approved requirements, contracts, policies, and implementation epics.

## Final direction

Build a calm, trustworthy banking operations workstation: fast for experienced staff, safe under pressure, transparent for approvers, and traceable for auditors.
