---
phase: "Phase 0 - Engineering Foundation"
epic: "Repository, Workspace, and Build"
portals: [All]
packages: [Tooling]
status: Ready for review
requirements: [NFR-MNT-001, NFR-COMP-001, SEC-016, SEC-018]
stories: [US-079]
backend_dependencies: []
last_updated: 2026-10-17
---

# Epic: Repository, Workspace, and Build

## Objective

Create a reproducible TypeScript monorepo with independently buildable portal boundaries, centrally enforced standards, and no banking behavior.

## Scope

- Pin Node.js and pnpm; create workspace and lockfile policy.
- Scaffold the four Next.js applications with placeholder routes clearly marked non-production.
- Establish approved shared-package entry points, strict TypeScript, formatting, linting, environment validation, and architecture checks.
- Add deterministic scripts for install, format, lint, typecheck, test, and build.
- Exclude feature implementation, real identity integration, and speculative packages.

## Required structure and boundaries

Follow the architecture target. Architecture tests must reject app-to-app imports, deep imports around package APIs, cycles, and client imports of server-only modules. Each app must build independently. Templates must not add analytics, service workers, remote fonts, example secrets, or unapproved dependencies.

## Implementation slices

1. Approve runtime, framework, package-manager, and workspace ADRs.
2. Add root configuration and frozen-install policy.
3. Scaffold minimal portal entry points and shared package shells.
4. Add strict compiler, lint, formatting, and import-boundary rules.
5. Add environment schema and safe `.env.example` files.
6. Add deterministic verification scripts and contributor instructions.

## Tests and evidence

- Clean checkout reproduces install and all builds.
- Intentional forbidden imports fail architecture checks.
- Client bundle checks reject a server-only fixture.
- Each portal can build without importing another app.
- No secrets, live endpoints, or production data appear in artifacts.

## Acceptance criteria

- [ ] Runtime and package manager are pinned.
- [ ] Strict TypeScript and central quality rules apply everywhere.
- [ ] Four independent app boundaries and approved package boundaries exist.
- [ ] Frozen install and independent production builds pass.
- [ ] No banking behavior or unapproved framework is introduced.

## Prohibited assumptions and agent instructions

Do not choose production hosting, identity provider, telemetry vendor, or BFF behavior in this epic. Read the current tree first, preserve unrelated work, and report exact files and commands. `../backend` remains read-only.
