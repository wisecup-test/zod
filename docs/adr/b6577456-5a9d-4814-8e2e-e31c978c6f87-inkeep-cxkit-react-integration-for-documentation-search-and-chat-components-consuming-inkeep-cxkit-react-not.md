---
version: 2
name: b6577456-5a9d-4814-8e2e-e31c978c6f87-inkeep-cxkit-react-integration-for-documentation-search-and-chat-components-consuming-inkeep-cxkit-react-not
description: "@inkeep/cxkit-react Integration for Documentation Search and Chat: Components Consuming Inkeep Cxkit React Not"
metadata:
  actual:
    adr_id: b6577456-5a9d-4814-8e2e-e31c978c6f87
    status: accepted
    candidate_group_id: b85fcc00-74b9-4972-9289-84379d156c19
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - components/**
---

# @inkeep/cxkit-react Integration for Documentation Search and Chat: Components Consuming Inkeep Cxkit React Not

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/docs`

Applies to:
- `components/**`

## Context

- Documentation user interfaces require interactive search dialogs and conversational assistance to help users navigate content effectively.
- Multiple documentation components coordinate external AI search dialogs and chat bubble widgets using client-side rendering boundaries.
- Widget initialization depends on client-accessible runtime environment configuration keys and component lifecycle synchronization.

## Problem Statement

Documentation platforms require embedded, interactive search and conversational Q&A capabilities, but maintaining bespoke vector search infrastructure and custom chat UI components introduces significant operational overhead and development complexity.

## Decision

1. MUST_NOT: Components consuming @inkeep/cxkit-react MUST NOT expose private API credentials or server-only secret tokens to the client environment.

## Policy Block

- MUST_NOT Components consuming @inkeep/cxkit-react MUST NOT expose private API credentials or server-only secret tokens to the client environment.

In scope:
- Frontend documentation user interface components requiring search dialogs or floating assistant widgets.

Out of scope:
- Server-rendered backend routes and static non-interactive documentation generation modules.

## Rationale

- Adopting @inkeep/cxkit-react standardizes documentation discovery and interactive support across the documentation suite without bespoke search infrastructure.
- Client-side rendering boundaries and React lifecycle hooks ensure smooth widget mounting without server-side hydration mismatches.
- Binding client configuration to designated public environment keys decouples deployment environments from hardcoded service credentials.

## Consequences

Positive:
- Offloads search indexing, conversational reasoning, and AI widget maintenance to a specialized external documentation search provider.
- Provides turnkey search dialogs and interactive assistance bubbles with consistent client-side behavior.
- Standardizes client-side integration patterns through well-defined React lifecycle hooks and environment key configuration.

Negative:
- Creates runtime dependency and network coupling to third-party widget hosting and backend search availability.
- Introduces client bundle overhead and browser execution overhead for interactive documentation components.
- Exposes search service integration parameters to the browser via public environment variables.

## Alternatives

- In-house custom documentation search modal and conversational AI backend (rejected)
  Rejected because: Requires building, hosting, and maintaining custom vector index search pipelines and chat orchestrations rather than consuming a managed documentation widget.
  When valid: When documentation requires strict air-gapped data residency or offline search support without external network dependencies.
- Static keyword-based client-side search dialog (rejected)
  Rejected because: Lacks natural language query understanding and conversational assistant capabilities provided by the integrated AI service.
  When valid: When operating in low-bandwidth environments with minimal documentation content and zero external service reliance.

## Risks

- Third-party service availability degradation could impact documentation search and assistant widget responsiveness.
  Mitigation: Implement resilient fallback handling and graceful UI degradation when remote service endpoints are unreachable.
  Owner: Frontend engineering team
- Client bundle size increase from external widget dependency impacting initial page load performance.
  Mitigation: Isolate widget imports to dedicated client components loaded lazily or mounted on user interaction.
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
- Configure public environment keys in the repository environment template and inject them during deployment without baking private secrets into client bundles.
- Isolate third-party component wrappers in dedicated documentation interface modules to maintain clean architectural boundaries between core documentation layouts and external widget integrations.

## Continuation Context


Verify commands:
- # Discover and run the workspace lint script to verify client boundary directives and environment variable usage.
- # Discover and run the workspace typecheck script to validate component bindings against library interfaces.
- # Discover and run the workspace test runner to confirm documentation component mounting.

Accept when:
- Static analysis verification confirms all widget wrapper components declare client boundaries.
- Type checking completes with zero unresolved symbols or incompatible interface references.
- Component mounting tests verify proper configuration resolution and lifecycle initialization.

## Enforcement

- Verified by: Automated pull request checks running repository linting and typecheck scripts.
- Verified by: Architecture and code review validating client boundary declarations and credential exposure rules.
- Violation handling: Pull requests introducing unapproved documentation search libraries or unvalidated client secrets must be blocked.
- Exception process: Exceptions require architectural review and documentation of alternative search and widget delivery mechanisms.