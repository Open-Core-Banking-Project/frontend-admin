---
phase: "Phase 3 - Growth Channels"
status: Ready for review
portals: [Staff Operations, System Administration, Finance Reporting]
requirements: [PAY-010, PAY-011, PAY-012, CFG-006, API-001, API-002, API-004, API-008]
stories: [US-030, US-031, US-059, US-060, US-061, US-062, US-063, US-067]
dependencies: [Phase 2 verified, Approved corporate/card/merchant/partner contracts]
last_updated: 2026-10-17
---

# Phase 3 - Growth Channels

## Objective

Add governed operations for corporate users and mandates, bulk/payroll and virtual-account services, card and merchant operations, and partner API administration without pulling customer-facing portal responsibilities into frontend-admin.

## Epics

| Order | Epic | Primary portal |
| --- | --- | --- |
| 1 | Corporate Users, Mandates, and Payment Approvals | Staff Operations |
| 2 | Bulk/Payroll Payments and Virtual Accounts | Staff Operations/Finance Reporting |
| 3 | Card and Merchant Operations | Staff Operations/Finance Reporting |
| 4 | Partner API and Integration Operations | System Administration |

## Phase gates

- Corporate authority and mandates come from backend contracts, not frontend role inference.
- File uploads use secure, asynchronous validation and never become executable payment authority by themselves.
- Card data is minimized and masked; CVV/PIN/full PAN never enters admin telemetry or fixtures.
- API credentials and webhook secrets are write-only or reference-only and cannot be read back.
- Bulk and settlement views preserve per-item and aggregate authoritative outcomes.

## Exit criteria

Critical journeys pass permission, mandate/scope, self-approval, duplicate, partial failure, timeout, sensitive-data, accessibility, and secure-export evidence.

## Agent instructions

Do not move corporate self-service UI into the admin repository. Admin portals operate governed back-office functions only. Contract gaps remain explicit and backend stays read-only.
