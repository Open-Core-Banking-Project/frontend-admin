---
phase: "Phase 1 - Banking Foundation"
epic: "Roles, Permissions, and Approval Workflow Administration"
portals: [System Administration]
status: Ready for review
requirements: [IAM-004, IAM-005, IAM-006, IAM-007, IAM-009, IAM-010, WFL-001, WFL-002, WFL-003, WFL-004]
stories: [US-006, US-007, US-048]
backend_dependencies: [Role, capability, scope, conflict-of-duty, entitlement version and workflow-definition APIs]
last_updated: 2026-10-17
---

# Epic: Roles, Permissions, and Approval Workflow Administration

## Objective and scope

Provide controlled administration of role bundles, capability grants, contextual scopes, conflict-of-duty rules, entitlement versions, and versioned approval workflows.

The UI never creates security meaning from role names and never grants an entitlement locally.

## Experiences

- Role/capability catalog and effective-grant inspection.
- Create/edit draft role with institution, branch, resource, amount, currency, channel, expiry, and delegation scopes supported by contract.
- Conflict preview, affected-user preview, before/after diff, submission, approval, publication, revocation, and access-review handoff.
- Workflow designer using constrained schema-driven steps, not arbitrary executable expressions.

## Security and state

Privileged routes require strong authentication and enhanced masking/audit references. Self-grant and self-approval are presented as denied but backend enforcement is mandatory. Distinguish draft, invalid, conflict detected, pending, approved, active, expired, revoked, rejected, and stale entitlement.

## Implementation slices and evidence

1. Read-only capabilities, roles, scopes, and workflow definitions.
2. Draft role and scoped-grant editor with accessible tree/table behavior.
3. Conflict preview and affected-user diff.
4. Workflow definition, validation, versioning, and simulation.
5. Approval/publication/revocation and session entitlement refresh.

Test privilege escalation attempts, cross-institution grants, self-grant/self-approval, stale entitlement, conflicting roles, expired delegation, step-up, and complete keyboard navigation. No hidden control is treated as enforcement.

## Prohibited assumptions

Do not invent capability identifiers, conflict rules, approval graph semantics, inheritance, or delegation policy. Do not expose raw tokens or sensitive identity attributes.
