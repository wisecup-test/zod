# Fumadocs Library Adoption for Documentation Architecture: Interactive Search Dialogs Integrate Through Fumadocs

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Context

- The documentation application requires structured navigation layouts, markdown content loading, and search integration across technical documentation and blog routes.
- Rather than assembling disconnected UI primitives or building custom documentation routing and layout scaffolding from scratch, the codebase adopts the Fumadocs library suite.
- Fumadocs UI and Fumadocs Core modules provide standardized document layouts, source adapters, and search component bindings across documentation modules.

## Problem Statement

Managing technical documentation and blog content without a unified library suite introduces fragmentation in document layouts, manual source loading overhead, and inconsistent navigation and search UX. An architectural standard is required to govern how documentation layouts, source loaders, and search components are structured using an adopted library ecosystem.

## Decision

1. SHOULD: Interactive search dialogs SHOULD integrate through `fumadocs-ui/components/dialog/search` abstractions to align with standard documentation keyboard navigation and modal behavior.

## Policy Block

- SHOULD Interactive search dialogs SHOULD integrate through `fumadocs-ui/components/dialog/search` abstractions to align with standard documentation keyboard navigation and modal behavior.

In scope:
- Documentation application layout wrappers and page routes requiring structured content hierarchies.
- Content loading, source indexing, and MDX rendering modules for technical documentation and blog pages.
- Search overlay dialogs and navigation components within the documentation workspace.

Out of scope:
- Non-documentation workspace packages or microservices that do not render markdown or technical documentation.
- Standard marketing pages that do not require documentation navigation or content hierarchy abstractions.

## Rationale

- Adopting the Fumadocs library suite centralizes layout structures, table-of-contents generation, and source loading into a cohesive framework designed for documentation workflows.
- Using Fumadocs Core and UI components reduces boilerplate and eliminates divergence between documentation and blog presentation paths across the codebase.
- Integrating Fumadocs search dialog components ensures consistent accessibility and keyboard interaction patterns without needing bespoke modal implementations.

## Consequences

Positive:
- Standardized documentation layout architecture with built-in navigation, table of contents, and sidebar coordination.
- Unified content loading pipeline through dedicated source loaders and MDX integrations.
- Reduced maintenance overhead by relying on established documentation UI and core primitives instead of custom layout scaffolding.

Negative:
- Architectural coupling to Fumadocs layout conventions and component hierarchy structures.
- Upstream breaking changes across Fumadocs releases may require coordinated migration of source loaders and layout wrappers.
- Customizing layout presentation beyond Fumadocs configuration patterns requires specialized overrides or CSS adaptations.

## Alternatives

- Custom documentation layout scaffolding and hand-rolled MDX loader pipelines (rejected)
  Rejected because: Imposes significant ongoing maintenance burden for responsive sidebars, table of contents indexing, and search dialog accessibility.
  When valid: When building an entirely bespoke interactive application that does not follow standard documentation hierarchies.
- Generic headless component primitives without documentation-specific layout abstractions (rejected)
  Rejected because: Requires reimplementing documentation-specific content tree traversal, breadcrumbs, and source loading from scratch.
  When valid: When building general web application UIs that do not present structured technical documentation or MDX collections.

## Risks

- Breaking API changes across minor or major Fumadocs updates affecting source loaders or layout props
  Mitigation: Strictly pin dependencies using repository lock artifacts and verify public API contracts against the resolved version before upgrading
  Owner: engineering team
- Inadvertent divergent styling or layout customization that conflicts with Fumadocs internal DOM structure
  Mitigation: Constrain styling modifications to Fumadocs-supported layout configuration props and designated styling classes
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
- Configure centralized source loader adapters using Fumadocs Core to expose typed page collections to layout and page route components.
- Implement documentation and blog layouts by wrapping page trees with Fumadocs UI layout components rather than embedding manual navigation bars.

## Continuation Context


Verify commands:
- Discover and execute the repository dependency audit script to confirm resolved Fumadocs package versions adhere to the lock artifact.
- Discover and run the project typecheck and lint verification tasks to confirm Fumadocs layout imports and source loader interfaces conform to design constraints.
- Discover and execute the workspace test suite to validate that documentation layouts, search components, and MDX loaders render successfully.

Accept when:
- All documentation and blog page routes resolve navigation and content via Fumadocs UI layouts and Core source loaders without runtime errors.
- Static analysis, type checking, and linting suites pass without unapproved custom documentation layout implementations.
- The project test suite passes with all documentation rendering and search dialog integration tests verified.

## Enforcement

- Verified by: Automated continuous integration checks executing typechecking, linting, and build verification.
- Verified by: Architectural peer review on pull requests touching documentation layout structures or content loaders.
- Violation handling: Pull requests introducing bespoke documentation layouts or bypassing Fumadocs source loaders will fail automated checks and review gates.
- Violation handling: Identified violations must be refactored to consume Fumadocs UI layout and Core source components before merge approval.
- Exception process: Teams requiring specialized non-documentation landing pages must submit an architectural exception documenting why standard Fumadocs layouts cannot satisfy requirements.
- Exception process: Exceptions require review and sign-off by the frontend architecture team before integration.