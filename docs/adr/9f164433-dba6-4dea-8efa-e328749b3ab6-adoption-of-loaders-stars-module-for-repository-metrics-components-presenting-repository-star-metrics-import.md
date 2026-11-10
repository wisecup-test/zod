---
version: 2
name: 9f164433-dba6-4dea-8efa-e328749b3ab6-adoption-of-loaders-stars-module-for-repository-metrics-components-presenting-repository-star-metrics-import
description: "Adoption of @/loaders/stars Module for Repository Metrics: Components Presenting Repository Star Metrics Import"
metadata:
  actual:
    adr_id: 9f164433-dba6-4dea-8efa-e328749b3ab6
    status: accepted
    candidate_group_id: 43667bb6-7881-43a1-aeec-aa06921cc0ca
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - components/**
---

# Adoption of @/loaders/stars Module for Repository Metrics: Components Presenting Repository Star Metrics Import

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/docs`

Applies to:
- `components/**`

## Context

- Multiple documentation presentation components display GitHub repository star counts and ecosystem metrics.
- Ad-hoc external network calls within UI components introduce inconsistent loading states, duplicated network requests, and maintenance friction.
- A centralized internal loader module @/loaders/stars provides a single interface for repository star metrics.

## Problem Statement

Directly embedding third-party API queries or ad-hoc data fetching logic within documentation presentation components leads to duplicated network requests, inconsistent caching behaviors, and tight coupling between UI styling and external data structures. A dedicated architectural boundary is required to encapsulate repository metric retrieval.

## Decision

1. MUST: Components presenting repository star metrics MUST import star data exclusively from the internal @/loaders/stars module.

## Policy Block

- MUST Components presenting repository star metrics MUST import star data exclusively from the internal @/loaders/stars module.

In scope:
- Documentation UI components displaying repository star counts or ecosystem popularity metrics.
- Presentation elements requiring standardized star pill indicators or ecosystem summaries.

Out of scope:
- Backend build scripts or external data synchronizers operating outside the documentation presentation layer.
- Unrelated UI components that do not render repository star counts.

## Rationale

- Adopting @/loaders/stars enforces separation of concerns by keeping data retrieval separate from visual rendering.
- A single loader interface enables centralized rate limit handling, caching strategies, and metric formatting across all documentation pages.
- Shared module consumption eliminates divergent data states across disparate components presenting the same repository metrics.

## Consequences

Positive:
- Centralizes data retrieval and ingestion logic for repository star counts into a single maintainable module.
- Decouples visual presentation components from remote API rate limits, authentication requirements, and transport protocols.
- Facilitates consistent caching and formatting of ecosystem metrics across all documentation views.

Negative:
- Introduces an internal coupling where presentation components depend on the interface and availability of the @/loaders/stars module.
- Changes to repository star schema or loading contracts require coordinated updates across all consumer components.

## Alternatives

- Direct remote API fetching inside presentation components (rejected)
  Rejected because: Duplicates network fetching logic, exposes components to upstream rate limits, and tightly couples visual rendering to external API shapes.
  When valid: Rapid prototyping in isolated one-off scripts where module structure is not preserved.
- Inline hardcoded metric constants in UI components (rejected)
  Rejected because: Prevents dynamic or build-time updates to repository metrics, causing data drift across documentation surfaces.
  When valid: Static design mockups or offline storybook tests with fixed test fixtures.

## Risks

- Outages or contract shifts in external repository APIs could break all dependent UI components simultaneously.
  Mitigation: Ensure @/loaders/stars implements robust fallback values or cached responses when upstream data is unavailable.
  Owner: engineering team
- Loader interface changes require synchronized refactoring across all consuming presentation components.
  Mitigation: Document and type the returned metric contract to prevent breaking consumer components during internal loader refactoring.
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
- Consumer components should treat the data returned by @/loaders/stars as read-only presentation models.
- Any caching, revalidation, or fallback handling must remain encapsulated within the loader module boundary.

## Continuation Context


Verify commands:
- Discover and run the project static analysis and module boundary verification scripts to confirm that star metrics imports originate exclusively from @/loaders/stars.
- Discover and execute the project test runner to verify that components consuming @/loaders/stars render metric data according to the module contract.

Accept when:
- All UI components rendering repository star metrics import star data exclusively from the @/loaders/stars module.
- Static analysis and module boundary checks pass with zero unauthorized direct network imports for repository metadata in presentation components.

## Enforcement

- Verified by: Automated linting and module boundary checks verifying import sources for repository star data.
- Verified by: Mandatory peer code review for all new UI components presenting ecosystem or repository metrics.
- Violation handling: Pull requests containing direct external metric fetches in UI components are blocked by automated review gates.
- Violation handling: Code violations must be refactored to consume the @/loaders/stars module prior to merge.
- Exception process: Submit an architectural exception request detailing why the internal loader module cannot fulfill the specific metric retrieval requirements.
- Exception process: Require formal approval from the documentation architecture leads before introducing alternative metric sources.