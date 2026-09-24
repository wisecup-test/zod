# Adopt @inkeep/cxkit-react for Client-Side Documentation Search and Support: Server Only Private Secrets Unverified Environment

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Context

- Documentation user interfaces require interactive search dialogs and conversational assistance widgets to help users navigate content.
- Integrating conversational AI support directly into documentation frontends requires specialized UI components and client-side lifecycle management.
- Client-side components must consume public configuration securely while isolating external widget rendering to the browser.

## Problem Statement

Documentation frontends require a consistent, maintainable approach for delivering interactive AI-assisted search and contextual support widgets while maintaining explicit client-side runtime boundaries and secure configuration handling.

## Decision

1. MUST_NOT: Server-only private secrets or unverified environment variables MUST NOT be passed to @inkeep/cxkit-react client components.

## Policy Block

- MUST_NOT Server-only private secrets or unverified environment variables MUST NOT be passed to @inkeep/cxkit-react client components.

In scope:
- Documentation user interface components implementing search dialogs, support bubbles, or interactive assistance widgets.

Out of scope:
- Server-rendered backend endpoints, static markdown content processing, and non-interactive documentation layout components.

## Rationale

- Adopting @inkeep/cxkit-react across documentation components provides dedicated search and chat dialog capabilities with minimal custom UI code.
- Marking integrating modules with client directives ensures external interactive widgets remain isolated to the browser runtime.
- Using designated public environment variables through the runtime environment interface enables secure client-side initialization without leaking sensitive server secrets.

## Consequences

Positive:
- Standardizes interactive documentation search and contextual AI support through a dedicated React integration library.
- Isolates dynamic third-party rendering to explicitly declared client boundary components.
- Leverages managed search dialogs and assistance widgets without custom client-side conversational UI implementation.

Negative:
- Introduces an external runtime dependency on third-party client libraries and remote service availability.
- Increases client-side script bundle size within documentation pages rendering interactive search and bubble components.
- Exposes public integration keys to client browsers, requiring strict API key permission scoping at the vendor service level.

## Alternatives

- Custom internal search modal and conversational assistant interface (rejected)
  Rejected because: Increases maintenance burden and requires building and maintaining indexing, vector search, and conversational UI components in-house.
  When valid: When strict data sovereignty forbids third-party client integrations or when completely offline documentation is required.
- Server-side search rendering without client-side widget libraries (rejected)
  Rejected because: Precludes real-time conversational chat assistance and interactive modal overlays provided by the client component ecosystem.
  When valid: When building static, non-interactive documentation interfaces that strictly avoid browser client runtime scripts.

## Risks

- Exposure of public environment keys in client bundles could lead to unauthorized API query consumption.
  Mitigation: Ensure the public environment key is restricted strictly to read-only search operations and domain-restricted origins within the vendor dashboard.
  Owner: engineering team
- Upstream third-party availability issues or script errors could degrade documentation user experience.
  Mitigation: Wrap widget initialization within error boundaries and client lifecycle hooks to prevent rendering interruptions in documentation content.
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
- Locate the project dependency declaration to confirm the declared package range and verify compatibility with existing documentation framework packages.
- Ensure the public environment variable is defined in the appropriate deployment environment configuration before deploying documentation components.

## Continuation Context


Verify commands:
- Discover the project verification script from the repository manifest and execute it to validate compilation and static type checking across documentation components.
- Discover and execute the repository linting suite to ensure proper client directive placement and hook lifecycle dependencies.

Accept when:
- Client documentation components successfully render interactive search and assistance interfaces powered by @inkeep/cxkit-react.
- Static analysis confirms all @inkeep/cxkit-react consumer modules declare the client boundary directive and handle lifecycle effects within useEffect.
- Configuration verification confirms that only public client environment variables are exposed to the browser runtime.

## Enforcement

- Verified by: Automated static analysis and linting checks in continuous integration pipelines.
- Verified by: Peer code reviews of pull requests introducing documentation UI components.
- Verified by: Dependency auditing scripts checking client bundle contents.
- Violation handling: Pull requests introducing non-standard search components without approval will be blocked.
- Violation handling: Static analysis failures flagging missing client boundary directives or unverified secrets will fail build checks.
- Violation handling: Unapproved client dependencies must be refactored to align with the standard integration.
- Exception process: Submit an architectural exception request detailing reasons why alternative search or assistance mechanisms are required.
- Exception process: Obtain approval from documentation and frontend engineering leads before integrating alternate client-side search widgets.
- Exception process: Document approved exceptions within the relevant repository module documentation.