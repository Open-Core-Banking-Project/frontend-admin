---
phase: "Phase 0 - Engineering Foundation"
epic: "Design System and Accessibility Foundation"
portals: [All]
packages: [ui, design-tokens]
status: Ready for review
requirements: [NFR-USA-001, NFR-ACC-001, NFR-COMP-001]
stories: [US-074, US-076]
backend_dependencies: []
last_updated: 2026-10-17
---

# Epic: Design System and Accessibility Foundation

## Objective

Deliver the smallest accessible, institution-themeable component foundation needed for operational applications, with documented interaction contracts and automated evidence.

The implementation must follow `../../design/UI_DESIGN_DIRECTION.md`. That document is the required visual and interaction baseline, including canonical page grids, portal signatures, primitive adaptation, banking-specific components, microcopy, and anti-generic UI rules.

## Included scope

- Tokens for typography, spacing, color, density, focus, motion, and semantic status.
- Foundations for button, link, input, select/combobox, checkbox/radio, alert, dialog, menu, tabs, breadcrumb, pagination, table shell, skeleton, empty state, error state, and status badge.
- Light/dark or brand modes only if approved; high contrast and reduced motion always respected.
- Story/demo surfaces with synthetic data, accessibility tests, keyboard contracts, and visual baselines where configured.
- Canonical index, detail, form, review/approval, workbench, and dashboard compositions demonstrated with synthetic banking content.
- A visual review gate that rejects stock admin templates, direct component-library themes, inconsistent action placement, and unjustified one-off patterns.

## Design rules

Use semantic HTML before ARIA. Components expose accessible names, descriptions, errors, disabled and busy state, deterministic focus, and escape/return-focus behavior. Status and risk never rely on color alone. Theming cannot reduce contrast or hide focus.

## Implementation slices

1. Approve token taxonomy, browser baseline, and theming contract.
2. Add reset, typography, layout, focus, and status primitives.
3. Build form and feedback primitives.
4. Build overlays, navigation, and table/pagination primitives.
5. Add documentation, automated accessibility checks, keyboard matrices, and visual evidence.
6. Verify canonical page grids across all four portal signatures and both supported density modes.

## Required evidence

- Automated accessibility tests pass for every primitive and state.
- Keyboard-only paths, focus return, zoom/reflow, reduced motion, and high contrast are reviewed.
- Theme fixtures meet contrast requirements.
- No component accepts unsafe raw HTML or embeds domain authorization.

## Acceptance criteria

- [ ] Critical primitives meet WCAG 2.2 AA expectations.
- [ ] Staff workflows can be composed without app-specific accessibility workarounds.
- [ ] Institution theming is token-driven and cannot override security/status meaning.
- [ ] Documentation names semantics, keyboard behavior, content rules, and prohibited use.
- [ ] Canonical page grids and anti-generic design checks pass visual review.

## Prohibited assumptions

Do not build an exhaustive speculative library, copy an external design system wholesale, or encode financial workflow policy into `ui`. Missing product design decisions remain explicit.
