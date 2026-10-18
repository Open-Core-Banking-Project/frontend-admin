---
phase: "Phase 2 - Regulated Operations"
epic: "Agency, Offline Capture, and Degraded Operations"
portals: [Staff Operations, System Administration]
status: Ready for review
requirements: [BRN-004, BRN-005, BRN-006, NFR-RES-001, NFR-RES-002]
stories: [US-057, US-058, US-073]
backend_dependencies: [Agent/device/limit/float, offline-capture review, synchronization, duplicate detection and degraded-mode policy APIs]
last_updated: 2026-10-17
---

# Epic: Agency, Offline Capture, and Degraded Operations

## Objective

Support back-office agent administration and controlled review of offline/degraded submissions while preventing the admin frontend from creating or replaying unauthorised offline financial commands.

## Experience

- Agent profile, status, devices, location, limits, float, commissions, settlement and risk controls.
- Onboarding/update/suspend/reactivate workflows with evidence and approval.
- Offline submission/synchronization monitor showing device, signed reference, capture time, receipt time, validation, duplicate, queued, rejected, posted, and unresolved states.
- Degraded-mode banner and feature matrix supplied by approved backend/operations policy.

## Controls

The admin web app does not manufacture offline payloads, signatures, or posting results. Requeue/replay actions require explicit backend eligibility, idempotency, reason, permission, and audit. Cached data is clearly stale and never presented as current authority.

## Slices and evidence

1. Agent/device/limit/float read views.
2. Agent lifecycle and approval flows.
3. Offline sync monitor and duplicate/conflict detail.
4. Controlled repair/requery/replay request.
5. Degraded-mode communication and operational runbook links.

Test unauthorized agent/branch, device mismatch, duplicate offline command, signature rejection, partial sync, replay denial, stale data, network recovery, self-approval, sensitive device masking, and accessible degraded warnings.

## Prohibited assumptions

Do not define cryptography, offline eligibility, reconciliation, agent commission, or degraded permissions in frontend code.
