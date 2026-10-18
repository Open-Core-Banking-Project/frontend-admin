---
phase: "Phase 1 - Banking Foundation"
epic: "Operations Queues, Cases, Complaints, and Documents"
portals: [Staff Operations]
status: Ready for review
requirements: [WFL-003, WFL-004, WFL-005, WFL-006, WFL-007, WFL-008, RPT-002]
stories: [US-049, US-050, US-064, US-074]
backend_dependencies: [Work queue, assignment, SLA, case, note, evidence, approval and document APIs]
last_updated: 2026-10-17
---

# Epic: Operations Queues, Cases, Complaints, and Documents

## Objective and scope

Provide branch-, role-, institution-, priority-, and SLA-aware work queues plus controlled complaint, service-request, exception, and failed-payment cases with notes, evidence, assignment, escalation, and approval history.

## Experiences

- My work/team work queues with server-side filters, ageing, SLA and restricted-state handling.
- Case create/detail/timeline, assignment, notes, attachments, related customer/transaction references, escalation, decision, closure, reopen where authorized, and immutable history.
- Secure evidence upload/download with scanning/processing state.
- Approval inbox integrated through stable task contracts, not reconstructed from case state.

## Controls

Sensitive cases and evidence require explicit capability and scope. Notes and evidence are never stored in browser persistence or telemetry. Rejection/override requires backend-defined reason and preserves history. Concurrency conflicts must refresh rather than overwrite another operator's action.

## Implementation slices and evidence

1. Read-only queues, saved non-sensitive preferences, and case detail.
2. Create/assign/update with concurrency handling.
3. Notes, evidence, scanning, and access denial.
4. SLA/escalation and approval-task integration.
5. Closure/reopen and end-to-end complaint/investigation journeys.

Test unauthorized evidence, cross-branch assignment, simultaneous updates, expired task, self-approval, upload rejection, session expiry, SLA status semantics, keyboard table/timeline use, and secure downloads.

## Prohibited assumptions

Do not invent SLA clocks, case transitions, attachment retention, visibility rules, or override authority.
