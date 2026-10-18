---
phase: "Phase 2 - Regulated Operations"
epic: "Corporate Onboarding and Lending Operations"
portals: [Staff Operations]
status: Ready for review
requirements: [CUS-001, CUS-002, CUS-005, CUS-007, ACC-008, WFL-002, WFL-006, RPT-001, RPT-002]
stories: [US-012, US-024, US-038, US-039, US-040, US-041, US-042]
backend_dependencies: [Corporate party, beneficial owner, KYC, loan product, application, approval, schedule, collateral, delinquency and recovery APIs]
last_updated: 2026-10-17
---

# Epic: Corporate Onboarding and Lending Operations

## Objective

Support staff workflows for corporate party onboarding and approved lending operations, including applications, evidence, decisions, schedules, collateral/guarantors, delinquency, and recovery tasks.

## Experience

- Corporate hierarchy, directors/signatories/beneficial owners, verification, KYC status, documents, duplicate detection, and approval.
- Loan product read-only terms, application capture, backend affordability/offer results, review, multi-level approval, disbursement status, repayment schedule, collateral, arrears, promise-to-pay, and recovery cases.
- Fixed-deposit maturity instructions may be included only with an approved contract and explicit story coverage.

## Integrity and privacy

Frontend does not calculate affordability, interest, schedule, collateral value, arrears, penalty, or disbursement outcome. Sensitive ownership, identity, legal, and credit data is minimized, masked, and never persisted unsafely. Approval and disbursement are distinct states.

## Slices and evidence

1. Corporate onboarding and relationship/evidence model.
2. Corporate KYC/duplicate/approval journey.
3. Loan application, backend assessment, offer, and approval.
4. Schedule, collateral, guarantor, and servicing views.
5. Delinquency and recovery work queues/cases.

Test permission/tenant denial, duplicate corporate, beneficial-owner evidence, stale offer, conflicting approval, self-approval, declined/expired/withdrawn states, schedule precision display, sensitive masking, secure documents, and accessible complex forms.

## Prohibited assumptions

Do not invent credit policy, scoring, legal structure, collateral valuation, accounting, repayment allocation, or recovery treatment.
