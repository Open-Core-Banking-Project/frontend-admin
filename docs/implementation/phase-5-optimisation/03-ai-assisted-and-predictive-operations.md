---
phase: "Phase 5 - Optimisation and Intelligence"
epic: "AI-Assisted Service and Predictive Operations"
portals: [All]
status: Ready for review
requirements: [RSK-005, RSK-006, RSK-007, RPT-004, RPT-006, SEC-009, SEC-013]
stories: [US-080]
backend_dependencies: [Approved assistant/recommendation, model registry/version, explanation, feedback, drift, evaluation and kill-switch APIs]
last_updated: 2026-10-17
---

# Epic: AI-Assisted Service and Predictive Operations

## Objective

Introduce narrowly scoped, explainable, human-controlled assistance for search, summarization, queue prioritization, next-best operational action, anomaly surfacing, and forecasting only after governance, evaluation, and backend controls are approved.

## Allowed interaction pattern

```text
Authorized scoped context
  -> approved backend assistant/model service
  -> versioned suggestion with sources, confidence/limits and safety state
  -> human review
  -> ordinary permissioned workflow action
  -> backend validation, approval and audit
```

Generated output never invokes privileged APIs directly, posts money, approves a case, changes a risk outcome, or becomes audit evidence by itself.

## Required controls

- Use-case-specific capability, data minimization, prompt/input restrictions, output schema, citations/source references, model version, evaluation status, monitoring, feedback, override, and kill switch.
- Make suggestion, uncertainty, missing context, refusal, degraded/unavailable, and human-decision states clear.
- Prevent prompt injection from documents, notes, external content, or model output from becoming instructions to tools or privileged workflows.
- Do not send protected data to an unapproved external model or retain it outside approved policy.

## Implementation slices and evidence

1. Approve one bounded use case, threat model, data map, evaluation set, and human-control design.
2. Read-only suggestion component with sources/version/limitations.
3. Feedback, override, refusal, and unavailable states.
4. Handoff into an ordinary permissioned workflow with explicit human action.
5. Drift/quality monitoring, kill switch, audit references, and red-team/evaluation evidence.

Test data leakage, cross-tenant context, prompt injection, fabricated reference, unsafe recommendation, low confidence, model timeout, stale model, disabled model, permission denial, override, keyboard/screen-reader use, and no direct privileged action.

## Acceptance criteria

- [ ] Approved evaluations meet defined thresholds and known limitations are visible.
- [ ] Human review and backend enforcement cannot be bypassed.
- [ ] Scope, model version, source references, feedback, and decisions are traceable.
- [ ] Kill switch and graceful non-AI fallback are verified.
- [ ] No sensitive data appears in model telemetry or unauthorized retention.

## Prohibited assumptions

Do not create a general-purpose banking chatbot, let free text choose permissions or transactions, treat model confidence as approval, hide uncertainty, or auto-execute a generated recommendation.
