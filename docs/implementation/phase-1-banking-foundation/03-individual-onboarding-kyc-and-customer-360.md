---
phase: "Phase 1 - Banking Foundation"
epic: "Individual Onboarding, KYC, and Customer 360"
portals: [Staff Operations]
status: Ready for review
requirements: [CUS-001, CUS-002, CUS-003, CUS-004, CUS-005, CUS-006, CUS-007, CUS-008, CUS-009, CUS-010, RPT-002, SEC-013]
stories: [US-011, US-013, US-014, US-015, US-064]
backend_dependencies: [Customer search, duplicate detection, onboarding, KYC evidence, screening outcome, risk-tier, document and customer-360 APIs]
last_updated: 2026-10-17
---

# Epic: Individual Onboarding, KYC, and Customer 360

## Objective and scope

Enable authorized staff to search safely, onboard an individual, collect required information and evidence, resolve potential duplicates through approved flows, track identity verification, assign backend-approved KYC/risk state, and view an audited masked customer 360 profile.

## Experiences

- Scoped customer search with minimum necessary results and safe no-result behavior.
- Resumable multi-step onboarding draft, review, submission, validation, duplicate warning, verification pending, evidence request, approval, rejection, and activation states.
- Customer 360 summary with masked identity/contact data, accounts, relationships, cases, documents, risk/KYC status, and access reason where required.
- Secure upload/download using backend-issued mechanisms.

## Controls and failure behavior

Viewing sensitive data requires capability, scope, and logged backend access. Do not place BVN/NIN, documents, or full account identifiers in URLs, telemetry, browser persistence, or fixtures. Provider timeout remains pending/unknown; frontend never maps raw provider results to a canonical identity decision.

## Implementation slices

1. Authorized customer search and masked result patterns.
2. Onboarding draft and client feedback against contract schema.
3. Duplicate review and approved resolution handoff.
4. Identity/KYC verification and document states.
5. Customer 360, audit context, and end-to-end journey.

## Required evidence

Test permission and cross-tenant denial, sensitive-access reason, masking/reveal policy, duplicate candidates, provider pending/failure, stale draft, upload rejection, session expiry, keyboard completion, and screen-reader form errors. Customer activation is shown only after authoritative confirmation.

## Prohibited assumptions

Do not invent mandatory KYC fields, merge policy, risk score, evidence retention, or provider interpretation. Corporate onboarding is Phase 2.
