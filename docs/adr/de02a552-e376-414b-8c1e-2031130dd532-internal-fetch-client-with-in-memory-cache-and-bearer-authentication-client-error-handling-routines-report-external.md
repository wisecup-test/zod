# Internal Fetch Client with In-Memory Cache and Bearer Authentication: Client Error Handling Routines Report External

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Context

- External data fetching for documentation assets requires querying upstream HTTP APIs with bearer token credentials.
- Queried values are held in an in-memory map data structure and requested via timed revalidation configurations to limit upstream query volume.
- The pattern is confined to a single data loader file and relies on runtime built-in network and collection primitives rather than a shared external client package.

## Problem Statement

Direct invocations of remote HTTP endpoints within individual loader routines introduce ad-hoc credential handling, inconsistent caching semantics, and uncoordinated upstream API integration across internal boundaries.

## Decision

1. MUST: Client error handling routines MUST report external API failure events to standard error channels without leaking secret credentials or runtime environment details.

## Policy Block

- MUST Client error handling routines MUST report external API failure events to standard error channels without leaking secret credentials or runtime environment details.

In scope:
- Internal data loader routines querying remote HTTP service endpoints.
- Modules managing cached external API integration data.

Out of scope:
- Direct client-side browser network requests.
- First-party internal service-to-service communication mechanisms.

## Rationale

- In-memory caching and timed revalidation prevent redundant network calls to external rate-limited endpoints.
- Isolating external API calls to dedicated loader routines limits the blast radius of upstream API changes and network failures.
- Environment-based credential injection prevents hardcoded secrets while enabling execution across different operational environments.

## Consequences

Positive:
- Upstream external API requests are minimized through combined in-memory and timed revalidation caching.
- Authentication secrets remain separated from application source code via environment variable injection.
- External request failures are captured and logged to prevent unhandled process termination.

Negative:
- Single-file ad-hoc client implementations lack shared retry, circuit-breaking, and rate-limiting infrastructure across the project.
- In-memory map caching does not persist across process restarts or distribute across independent execution instances.

## Alternatives

- Ad-hoc direct HTTP fetch without local caching (rejected)
  Rejected because: Results in repeated remote requests, exhausting upstream API rate limits and degrading loader responsiveness.
  When valid: Valid only for dynamic queries where responses must never be cached.
- Centralized external client gateway package (deferred)
  Rejected because: Premature abstraction given that external API querying is currently restricted to a single loader file.
  When valid: Valid when multiple internal packages must coordinate requests against the same external APIs.

## Risks

- Unbounded growth of in-memory caching map causing excessive memory consumption over prolonged runtimes.
  Mitigation: Establish cache eviction policies or rely on runtime revalidation boundaries to constrain memory usage.
  Owner: engineering team
- Missing or invalid external authentication credentials causing silent loader failures.
  Mitigation: Log clear diagnostic warnings instructing developers on required configuration without revealing secret values.
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
- Verify that all external client endpoints define explicit cache revalidation intervals matching route staleness requirements.
- Ensure environment variable lookups for external authentication tokens are validated prior to initiating outbound HTTP requests.

## Continuation Context


Verify commands:
- Discover the repository test runner from the root manifest and execute the test suite covering data loader modules.
- Discover the repository static analysis script from configuration artifacts and run lint checks across external client integrations.

Accept when:
- Data loader modules retrieve external records and verify cached responses before initiating outbound network requests.
- Static analysis and test suites pass without reporting unhandled credential references or unvalidated external network calls.

## Enforcement

- Verified by: Automated test suites executing data loader scenarios in isolated environments.
- Verified by: Continuous integration static analysis checks for secret handling and network boundaries.
- Verified by: Peer code review for all new external API client integrations.
- Violation handling: Continuous integration jobs fail when unhandled external network calls or missing environment checks are detected.
- Violation handling: Pull requests introducing unencapsulated external API requests require architectural review and remediation before merge.
- Exception process: Submit an architectural exception request detailing why the external client cannot utilize standard cache layers or environment credential injection.
- Exception process: Obtain approval from the lead architect and document the rationale in module documentation.