---
version: 2
name: 78b67f20-7774-4b31-91b8-54ec6e4f07eb-adoption-of-fumadocs-ui-layout-components-for-documentation-route-shells-route-layouts-adopting-fumadocs-ingest-shared
description: "Adoption of fumadocs-ui Layout Components for Documentation Route Shells: Route Layouts Adopting Fumadocs Ingest Shared"
metadata:
  actual:
    adr_id: 78b67f20-7774-4b31-91b8-54ec6e4f07eb
    status: accepted
    candidate_group_id: 3eda226b-0493-41c6-8697-5bf32b4fdf24
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - app/**
---

# Adoption of fumadocs-ui Layout Components for Documentation Route Shells: Route Layouts Adopting Fumadocs Ingest Shared

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/docs`

Applies to:
- `app/**`

## Context

- Route hierarchies for documentation, technical references, and blog publishing require structured navigation chrome, responsive drawers, and table-of-contents handling.
- Maintaining disparate custom layout shells across documentation sections and publishing feeds introduces visual divergence, duplicated navigation logic, and configuration drift.
- The project delegates structural presentation for documentation and content routes to specialized layout primitives from fumadocs-ui while standardizing shared metadata and options through a centralized layout configuration module.

## Problem Statement

Maintaining bespoke layout shells across documentation and publishing route hierarchies leads to visual inconsistency, duplicated responsive navigation logic, and fragmented header and sidebar configurations across application segments.

## Decision

1. MUST: Route layouts adopting fumadocs-ui MUST ingest shared navigation, brand identity, and structural options through a centralized layout configuration module rather than declaring local inline navigation schemas.

## Policy Block

- MUST Route layouts adopting fumadocs-ui MUST ingest shared navigation, brand identity, and structural options through a centralized layout configuration module rather than declaring local inline navigation schemas.

In scope:
- Route layout modules governing documentation, technical guides, reference material, and content publishing sections.

Out of scope:
- Application routes independent of documentation or editorial publishing, including isolated API endpoints and standalone utility interfaces.

Exceptions:
- EXC-20-001: A specialized content route requires full-bleed canvas styling that cannot be accommodated within fumadocs-ui layout container contracts.

## Rationale

- Observed imports across layout modules demonstrate reliance on fumadocs-ui layout components to construct documentation and blog viewing experiences.
- Binding route layouts to a common layout configuration module prevents configuration drift and centralizes site-wide navigation updates.
- Adopting specialized documentation layout modules eliminates the need to author and maintain custom responsive navigation, dark mode toggling, and table-of-contents scaffolding.

## Consequences

Positive:
- Enforces uniform navigation chrome, responsive sidebars, and document outline tracking across all documentation route segments.
- Eliminates redundant layout boilerplate by consuming standardized layout primitives from fumadocs-ui.
- Centralizes global navigation, repository references, and brand presentation within a single shared layout configuration module.

Negative:
- Couples documentation route presentation and layout customization to the API contracts and structural conventions of fumadocs-ui.
- Customizing layout containers outside supported component slots requires overriding library styling contracts or coordinating upstream updates.

## Alternatives

- Custom In-House Documentation Layout Shells (rejected)
  Rejected because: Authoring bespoke responsive sidebars, navigation drawers, and table-of-contents trackers introduces significant maintenance overhead and creates visual divergence across routes.
  When valid: Valid when application interface requirements completely diverge from technical documentation and editorial publication paradigms.
- General-Purpose Application UI Framework Shells (rejected)
  Rejected because: Standard application UI frameworks lack built-in documentation navigation trees, automatic table-of-contents generation, and specialized technical content framing.
  When valid: Valid for administrative dashboards and transactional workflows that do not host hierarchical prose documentation.

## Risks

- Breaking contract changes in upstream fumadocs-ui layout components could disrupt route rendering during dependency upgrades.
  Mitigation: Adhere to the mandatory lock-version grounding process and validate layout rendering against version-specific documentation before updating dependencies.
  Owner: Frontend engineering team
- Inconsistent configuration across disparate route segments could lead to divergent navigation chrome or missing brand elements.
  Mitigation: Enforce ingestion of the centralized layout configuration across all layout implementations via static checks and peer review.
  Owner: Frontend engineering team

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Route layout definitions must import specialized fumadocs-ui layout wrappers and pass shared configuration properties derived from the centralized layout configuration module.
- When structuring technical documentation route shells, bind the layout to the source loader navigation tree to ensure automatic sidebar hierarchy generation.

## Continuation Context


Verify commands:
- Discover the repository build and static analysis scripts declared in the project manifest, and execute the type-checking pipeline to confirm layout component type conformance.
- Discover and execute the project test runner to verify that route layout components render with required configuration properties.
- Inspect layout imports across documentation route hierarchies to confirm layout components are sourced from fumadocs-ui layout entry points and bind to the centralized configuration module.

Accept when:
- Static type analysis passes with zero errors across all documentation route layout modules.
- Documentation and content route layouts render navigation headers, sidebars, and main content containers without runtime exceptions.
- All route layout implementations ingest the centralized layout configuration module without local duplication of global navigation structures.

## Enforcement

- Verified by: Automated continuous integration checks executing static type analysis and application build verification.
- Verified by: Peer code review for all pull requests that introduce or modify route layout modules.
- Violation handling: Pull requests that implement custom layout shells for documentation or blog routes without utilizing fumadocs-ui layout primitives or an approved exception will be blocked from merging.
- Exception process: Submit an exception request detailing the structural layout incompatibility to the architecture and documentation platform leads for review.