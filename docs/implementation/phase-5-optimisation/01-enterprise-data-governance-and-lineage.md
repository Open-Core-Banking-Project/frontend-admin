---
phase: "Phase 5 - Optimisation and Intelligence"
epic: "Enterprise Data Governance and Lineage"
portals: [System Administration, Risk Compliance]
status: Ready for review
requirements: [RPT-006, RPT-007, DAT-001, DAT-006, DAT-007, DAT-008]
stories: [US-066]
backend_dependencies: [Glossary, data asset, owner/steward, classification, lineage, quality rule/issue and access-approval APIs]
last_updated: 2026-10-17
---

# Epic: Enterprise Data Governance and Lineage

## Objective

Provide governed discovery and administration of business terms, data assets, owners/stewards, classifications, lineage, quality rules/issues, and access approvals.

## Experience and controls

- Searchable glossary/catalog with institution scope, version, owner, classification, retention, source, consumers, and quality state.
- Accessible upstream/downstream lineage with a tabular alternative.
- Draft/review/approve/publish workflows for glossary and classification changes.
- Quality issue queue, evidence, assignment, remediation status, and affected-report/model links.
- Sensitive field samples are prohibited unless an explicitly authorized secure preview contract exists.

## Slices and evidence

1. Glossary/catalog read views and search.
2. Ownership/classification/version workflows.
3. Lineage graph and accessible table.
4. Quality rules/issues and remediation workflow.
5. Access request/approval integration and evidence.

Test cross-domain/institution denial, restricted classification, stale lineage, orphan asset, conflicting edit, self-approval, quality issue escalation, sensitive preview denial, and keyboard/screen-reader lineage navigation.

## Prohibited assumptions

Do not infer lineage from frontend calls, expose raw records, invent retention/classification, or allow UI edits to rewrite source-system history.
