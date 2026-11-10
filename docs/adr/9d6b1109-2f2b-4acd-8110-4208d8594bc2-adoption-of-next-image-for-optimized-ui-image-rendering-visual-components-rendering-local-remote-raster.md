---
version: 2
name: 9d6b1109-2f2b-4acd-8110-4208d8594bc2-adoption-of-next-image-for-optimized-ui-image-rendering-visual-components-rendering-local-remote-raster
description: "Adoption of next/image for Optimized UI Image Rendering: Visual Components Rendering Local Remote Raster"
metadata:
  actual:
    adr_id: 9d6b1109-2f2b-4acd-8110-4208d8594bc2
    status: accepted
    candidate_group_id: 4180091f-05d3-44bb-80df-872af0ec478d
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - app/**
      - components/**
---

# Adoption of next/image for Optimized UI Image Rendering: Visual Components Rendering Local Remote Raster

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/docs`

Applies to:
- `app/**`
- `components/**`

## Context

- User interface components across documentation packages require consistent rendering of raster assets, brand logos, and theme-sensitive media.
- Unoptimized image rendering without fixed dimensions or preloading controls risks layout instability and unmanaged bandwidth consumption across varying viewports.
- Static analysis identifies uniform adoption of the next/image module across multiple component and layout definitions.

## Problem Statement

Rendering graphical assets with native markup across client and layout components leads to inconsistent asset handling, cumulative layout shift, and unoptimized delivery of themed brand assets.

## Decision

1. MUST: All visual components rendering local or remote raster graphics and brand logos MUST import and utilize the next/image module for asset presentation.

## Policy Block

- MUST All visual components rendering local or remote raster graphics and brand logos MUST import and utilize the next/image module for asset presentation.

In scope:
- All presentation components, layouts, and brand visual elements rendering raster images.
- Client-side and shared layout components displaying logo assets and theme-dependent imagery.

Out of scope:
- Inline vector graphics rendered directly as scalable vector elements.
- Non-visual utility functions and server-side metadata endpoints that do not render graphical interface elements.

Exceptions:
- EXC-20-001: Third-party content or syndication formats require raw markup where framework-level image components cannot be evaluated.

## Rationale

- Centralizing on next/image provides uniform handling of image dimensions, responsive scaling, and asset optimization across documentation interfaces.
- Static evidence demonstrates recurrent usage across five distinct interface and layout components, showing established consensus around next/image for visual assets.
- Mandating next/image eliminates cumulative layout shifts by requiring intrinsic sizing or explicit container bindings.

## Consequences

Positive:
- Consistent image handling and layout stability across desktop and mobile viewports.
- Automatic asset optimization and responsive scaling benefits provided by the framework module.
- Simplified theme and logo swapping encapsulated within dedicated image components.

Negative:
- Requires explicit width and height configurations or wrapper styling, increasing boilerplate for simple icons.
- Tightens coupling of interface components to framework-specific asset handling abstractions.

## Alternatives

- Native HTML img Elements (rejected)
  Rejected because: Fails to provide automated layout shift prevention, responsive srcset generation, and consistent aspect ratio enforcement.
  When valid: Valid only when rendering inside isolated non-framework environments such as plain email templates.
- Custom Image Wrapper around Native Elements (rejected)
  Rejected because: Introduces custom maintenance overhead for responsive sizing and loading optimization that next/image already standardizes.
  When valid: Valid when rendering across heterogeneous framework ecosystems without next/image support.

## Risks

- Incorrect sizing props or misconfigured fill containers causing layout overflow or distorted aspect ratios.
  Mitigation: Enforce container sizing constraints and visual regression checks during integration reviews.
  Owner: Frontend Engineering
- Version divergence between framework image API contracts and component property usage across updates.
  Mitigation: Apply strict lock-version verification against release documentation before adopting newer component properties.
  Owner: Frontend Engineering

## Implementation Notes

- DISCOVERY POLICY (MANDATORY): This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.

LOCK-VERSION GROUNDING (MANDATORY) — before writing code that uses a versioned library, execute in order:
1. Find the dependency manifest in the repo. It declares ranges, not installed versions.
2. Identify the build tool from the manifest.
3. Inspect the repository lock or resolution artifact to determine the exact resolved version. This artifact is authoritative; build-tool output only verifies the active environment matches it.
4. Look up the official documentation, changelog, or public API reference for that exact version. Do not use training-data recall — fetch or search the public internet for version-specific docs.
5. Confirm every API, class, or function you will call exists in that exact version's documentation before using it.
6. For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.
- Wrap image assets in dedicated presentation components when coordinating dark and light mode logo switching or stateful interactions.
- Ensure container elements provide relative positioning when configuring fill-based image rendering.

## Continuation Context


Verify commands:
- Discover and execute the repository linter suite to check for prohibited native image markup in presentation components.
- Discover and run the project type-checker and build pipeline to verify that next/image invocations satisfy contract constraints.

Accept when:
- Repository linting rules verify no raw HTML image tags exist within documentation component modules.
- Type verification and build commands succeed with all next/image properties matching resolved module definitions.

## Enforcement

- Verified by: Automated linting rules prohibiting native image elements in component files.
- Verified by: Continuous integration type validation and build verification.
- Verified by: Pull request code review of newly introduced visual presentation components.
- Violation handling: Automated continuous integration failure upon detection of unapproved image markup.
- Violation handling: Required refactoring to replace raw tags with next/image before pull request merge.
- Exception process: Submit an exception request to the architecture team specifying the technical constraint precluding next/image adoption.
- Exception process: Obtain documented architectural approval before bypassing linting or merging code.