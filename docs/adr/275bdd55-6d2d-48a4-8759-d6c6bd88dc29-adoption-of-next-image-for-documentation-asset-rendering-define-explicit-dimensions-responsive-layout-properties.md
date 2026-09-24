# Adoption of next/image for Documentation Asset Rendering: Define Explicit Dimensions Responsive Layout Properties

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Context

- Documentation components and layout configurations render visual assets including branding marks, sidebar logos, and explanatory diagrams
- Rendering unoptimized raster assets directly causes layout shifts and performance degradation on content pages
- Static analysis identifies repeated imports of the framework image module across documentation UI components

## Problem Statement

Inconsistent image rendering across documentation components risks cumulative layout shift and unoptimized asset delivery. A standardized image rendering module is required to guarantee layout stability and uniform asset optimization across documentation views.

## Decision

1. MUST: Define explicit dimensions or responsive layout properties on all image component invocations to prevent layout shift.

## Policy Block

- MUST Define explicit dimensions or responsive layout properties on all image component invocations to prevent layout shift.

In scope:
- Rendering raster images, branding logos, and content illustrations within documentation UI components and layouts

Out of scope:
- Rendering inline vector icon components that do not require external bitmap asset optimization
- Rendering text-based diagrams or code presentation blocks

## Rationale

- Evidence demonstrates consistent adoption of next/image across multiple independent documentation UI components
- Standardizing on next/image centralizes image optimization policies and ensures consistent rendering behavior across documentation themes
- Enforces layout shift prevention through framework-level layout and sizing mechanics

## Consequences

Positive:
- Standardizes asset rendering across documentation header, sidebar, and body presentation components
- Eliminates cumulative layout shift by enforcing dimension constraints or responsive layout modes
- Automates modern image format serving and dimension-based scaling for client presentation

Negative:
- Introduces architectural coupling to framework-specific image rendering semantics and configuration
- Requires explicit dimensions or layout containment strategies to prevent rendering errors
- Demands awareness of framework version changes regarding image loader and optimization behavior

## Alternatives

- Standard HTML image elements (rejected)
  Rejected because: Lacks automated layout shift mitigation, responsive srcset generation, and build-time optimization hooks provided by the framework module
  When valid: Static documentation environments without modern framework runtime support or when rendering simple SVG placeholders
- Custom picture wrapper component with manual responsive source sets (rejected)
  Rejected because: Increases maintenance overhead by requiring manual responsive breakpoint calculations and custom asset resolution logic
  When valid: Decoupled multi-platform design systems requiring vendor-agnostic markup across distinct rendering engines

## Risks

- Breaking API changes in upstream framework image components during major version upgrades
  Mitigation: Verify locked dependency artifacts and consult matching framework documentation before adopting version-specific image component attributes
  Owner: Frontend Engineering
- Incorrect dimension definitions leading to improper aspect ratio scaling or layout deformation
  Mitigation: Enforce lint rules requiring explicit width and height attributes or fill mode configuration
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
- Discover image component configuration options and layout modes from the authoritative documentation corresponding to the resolved framework version
- Maintain dark and light mode asset separation through declarative component styling rather than duplicate unmanaged element structures

## Continuation Context


Verify commands:
- Discover and run the repository linter to detect unoptimized image tag usage
- Discover and execute the repository type checker to validate image component properties
- Discover and execute the repository build script to confirm asset resolution and compilation integrity

Accept when:
- All image rendering in documentation presentation components passes automated lint and static analysis without unoptimized image violations
- Type verification succeeds across all component properties consuming the image module
- Repository build verification completes without missing asset or unresolved component errors

## Enforcement

- Verified by: Automated linting rules checking for unoptimized HTML image element usage
- Verified by: Repository static type checking and build verification scripts
- Verified by: Peer code review during documentation component pull requests
- Violation handling: Pull requests introducing unoptimized image tags will be blocked by automated repository checks
- Violation handling: Violations flagged in code review must be refactored to use the standardized image component before merge
- Exception process: Exceptions require review by the frontend architecture team and documented justification demonstrating why framework-managed image optimization cannot be used
- Exception process: Approved exemptions must include a tracking ticket and scheduled migration plan back to the standard image component