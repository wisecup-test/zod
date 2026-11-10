---
version: 2
name: 8d00d28f-6669-4487-a338-6c60e989417b-adoption-of-fumadocs-ui-for-documentation-application-layouts-documentation-fallback-status-boundaries-within-route
description: "Adoption of fumadocs-ui for Documentation Application Layouts: Documentation Fallback Status Boundaries Within Route"
metadata:
  actual:
    adr_id: 8d00d28f-6669-4487-a338-6c60e989417b
    status: accepted
    candidate_group_id: ac811e8d-24b1-44b1-9dc6-e30b8032ba34
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - app/**
---

# Adoption of fumadocs-ui for Documentation Application Layouts: Documentation Fallback Status Boundaries Within Route

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/docs`

Applies to:
- `app/**`

## Context

- The documentation application requires cohesive, standardized presentation layouts for documentation hierarchy, navigation, and fallback routes.
- Static analysis detects repeated adoption of fumadocs-ui layout and page primitives across documentation route components.

## Problem Statement

Maintaining fragmented layout structures for documentation content causes navigation inconsistencies, duplicate styling logic, and increased maintenance overhead across documentation routes.

## Decision

1. SHOULD: Documentation fallback and status boundaries within the documentation route tree SHOULD align their presentation tokens with the documentation UI theme tokens.

## Policy Block

- SHOULD Documentation fallback and status boundaries within the documentation route tree SHOULD align their presentation tokens with the documentation UI theme tokens.

In scope:
- All documentation route layouts, content pages, and related status fallback boundaries within the documentation application.

Out of scope:
- Non-documentation application routes and external presentation pages that do not render documentation trees.

## Rationale

- Adopting fumadocs-ui provides purpose-built documentation layout structures that handle navigation trees and page layout responsibilities consistently.
- Centralizing documentation presentation around established library components prevents diverging UI patterns across documentation routes and status pages.

## Consequences

Positive:
- Standardizes documentation presentation, navigation menus, and content layouts across all documentation routes.
- Eliminates redundant boilerplate for documentation page shells and status fallbacks.

Negative:
- Couples documentation route structures to the lifecycle and layout conventions of the external documentation UI library.
- Upgrades require lock-file grounding to verify compatibility with existing layout configurations.

## Alternatives

- Custom documentation layout primitives authored from baseline UI components (rejected)
  Rejected because: Increases ongoing maintenance overhead and requires custom re-implementation of documentation navigation, tree structures, and table-of-contents mechanics.
  When valid: Valid only when documentation requirements demand branding or navigational paradigms unsupported by documentation UI frameworks.
- Alternative third-party documentation layout engines (rejected)
  Rejected because: Introduces conflicting styling systems and redundant presentation abstractions across documentation routes.
  When valid: Valid if an ecosystem migration is planned across all documentation workspaces.

## Risks

- Upstream library breaking changes in layout APIs could disrupt documentation navigation rendering.
  Mitigation: Adhere to lock-version grounding before updating documentation library dependencies and audit upstream release changelogs for breaking layout contract changes.
  Owner: engineering team
- Inflexible layout constraints could impede edge-case customization required by specific documentation pages.
  Mitigation: Encapsulate custom navigation attributes within shared configuration modules rather than forking baseline layout wrappers.
  Owner: engineering team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Inspect the active documentation layout configuration to ensure shared navigation props are correctly routed into documentation layout wrappers.
- Ensure fallback and error boundaries within documentation segments share consistent styling attributes derived from the documentation UI theme contract.

## Continuation Context


Verify commands:
- Discover and execute the project verification script from the repository manifest to confirm import validity and type consistency across documentation routes.
- Run the repository automated linting check to verify that documentation layouts do not import unapproved layout alternatives.

Accept when:
- All documentation layout routes import documentation scaffolding components exclusively from the designated documentation UI library.
- Repository verification scripts pass without unresolved module imports or layout contract mismatches.

## Enforcement

- Verified by: Automated linting and import boundaries verified during pull request validation.
- Verified by: Architectural peer review of all documentation layout route additions and updates.
- Violation handling: Pull requests introducing ad-hoc documentation layout wrappers without exception approval are blocked from merge.
- Violation handling: Violations identified during code review must be refactored to consume approved documentation UI primitives.
- Exception process: Submit an architectural exception request detailing layout constraints that cannot be satisfied by the documentation UI library.
- Exception process: Obtain documented approval from documentation module maintainers prior to merging custom layout alternatives.