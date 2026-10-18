---
phase: "Phase 3 - Growth Channels"
epic: "Corporate Users, Mandates, and Payment Approvals"
portals: [Staff Operations]
status: Ready for review
requirements: [IAM-004, IAM-006, IAM-007, PAY-011, WFL-002]
stories: [US-059, US-060]
backend_dependencies: [Corporate profile/user, signatory, mandate, entitlement, limit, payment approval and audit APIs]
last_updated: 2026-10-17
---

# Epic: Corporate Users, Mandates, and Payment Approvals

## Objective

Allow authorized staff to administer corporate user relationships, signatories, mandates, limits, and support/oversight of multi-level payment approvals without acting as the corporate customer or bypassing corporate authority.

## Experience and controls

- Corporate hierarchy, accounts, users, signatories, mandate versions, signing combinations, limits, delegations, and effective dates.
- Draft/change/compare/submit/approve/publish/revoke workflows with prior/proposed values.
- Corporate payment approval trace and authorized operational intervention only where contract permits.
- Clear separation between bank staff capabilities and corporate-user entitlements.

Frontend does not evaluate mandate satisfaction or approve on behalf of a signatory. Self-approval and conflicted administration are denied by backend and represented accurately.

## Slices and evidence

1. Read-only corporate authority and entitlement views.
2. User/signatory/mandate draft forms and evidence.
3. Limit/delegation changes and conflict preview.
4. Approval/publication/revocation.
5. Payment approval trace and operational support.

Test cross-corporate access, expired mandate, insufficient signatories, conflicted user, self-approval, stale mandate, concurrent edit, step-up, masking, and accessible relationship/approval views.

## Prohibited assumptions

Do not infer authority from job title, user role, uploaded document, or client-side combination logic. Do not implement corporate customer self-service here.
