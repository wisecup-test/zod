---
version: 2
name: 5d014d49-6d1d-4d2d-9eb6-269bb00798ad-built-in-fetch-api-boundary-usage-for-external-clients-repository-maintenance-routines-use-runtime-built
description: "Built-in Fetch API Boundary Usage for External Clients: Repository Maintenance Routines Use Runtime Built"
metadata:
  actual:
    adr_id: 5d014d49-6d1d-4d2d-9eb6-269bb00798ad
    status: accepted
    candidate_group_id: 48ac7a63-f307-43b4-b15a-af8c15cf1e82
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - scripts/**
---

# Built-in Fetch API Boundary Usage for External Clients: Repository Maintenance Routines Use Runtime Built

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `.` (whole repository)

Applies to:
- `scripts/**`

## Context

- Repository maintenance routines require interactions with external remote endpoints to retrieve metadata and publish synchronization status.
- External HTTP communication is performed via direct calls to the runtime built-in fetch interface rather than adopting an external client library or shared client wrapper.
- Request configurations such as HTTP methods, headers, and serialized payloads are defined inline at each invocation site.
- The codebase maintains no centralized HTTP client abstraction or third-party dependency for routine script-level network operations.

## Problem Statement

Standalone repository maintenance routines require network communication with external services but lack a formal architectural convention governing whether to introduce dedicated client dependencies or rely directly on runtime built-in interfaces.

## Decision

1. MUST: Repository maintenance routines MUST use the runtime built-in fetch interface for outbound HTTP communications when no shared internal client abstraction is required.

## Policy Block

- MUST Repository maintenance routines MUST use the runtime built-in fetch interface for outbound HTTP communications when no shared internal client abstraction is required.

In scope:
- Repository automation and maintenance scripts performing outbound network requests to external services.
- Standalone utility routines querying remote registries or external service endpoints.

Out of scope:
- Core library runtime modules distributed to end consumers.
- Internal cross-module communication that does not cross network boundaries.

Exceptions:
- EXC-26-001: An external remote endpoint requires specialized authentication flows or transfer protocols unsupported by the runtime built-in fetch API.

## Rationale

- Direct utilization of the runtime built-in fetch interface avoids introducing additional third-party dependencies into repository maintenance workflows.
- Observed patterns across repository scripts establish that native fetch handles all necessary HTTP verbs, custom headers, and payload serialization without supplemental client libraries.
- Eliminating external HTTP client libraries minimizes maintenance overhead and reduces supply-chain exposure across repository tooling.

## Consequences

Positive:
- Reduces external dependency surface area by using runtime built-in network capabilities.
- Avoids version synchronization overhead across independent utility scripts that require network communication.
- Maintains zero-dependency footprints for repository automation and maintenance tasks.

Negative:
- Lacks a centralized middleware layer for automatic retries, exponential backoff, and unified telemetry across scripts.
- Requires repetitive inline header and payload configuration across disparate utility routines.

## Alternatives

- Adoption of a third-party HTTP client library across all utility scripts (rejected)
  Rejected because: Introducing a third-party dependency adds external maintenance overhead and dependency audit requirements without delivering capabilities not already fulfilled by the runtime built-in fetch interface.
  When valid: When external service integrations require complex interceptor chains, automatic connection pooling, or streaming transformations not provided by native runtime utilities.
- Centralized shared internal client wrapper module (rejected)
  Rejected because: The limited number and disparate target endpoints of maintenance scripts do not justify the abstraction overhead of a shared internal networking package.
  When valid: When multiple internal modules share identical remote API contracts, authentication mechanisms, and retry policies.

## Risks

- Inconsistent error handling and lack of unified retry logic across independent fetch calls may cause transient network failures to fail script execution.
  Mitigation: Implement standard status code validation and explicit try-catch blocks surrounding fetch invocations in critical maintenance routines.
  Owner: engineering team
- Credential leakage or improper token handling in header declarations for authenticated remote requests.
  Mitigation: Retrieve credentials strictly from runtime environment variables rather than persisting credentials in source or configuration files.
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
- Ensure outbound fetch requests declare appropriate content type and user agent headers to ensure compatibility with external API rate-limiting and identification requirements.
- Consume response bodies according to expected payload format by awaiting the appropriate response parsing methods provided by the runtime fetch API.

## Continuation Context


Verify commands:
- Discover and execute the repository type-checking routine to confirm that all fetch invocations conform to runtime signature requirements.
- Discover and run the project static analysis and linting verification scripts to ensure external network requests adhere to repository security and syntax standards.
- Discover and run the project test suite to validate that script routines communicating with external boundaries handle network responses correctly.

Accept when:
- All outbound HTTP invocations in maintenance scripts use the runtime built-in fetch interface without external client dependencies.
- Type checking and static analysis verification scripts pass without errors across all script modules.
- Network response handling verifies status codes and safely parses payloads across external client invocation points.

## Enforcement

- Verified by: Automated static analysis checks in continuous integration pipelines.
- Verified by: Peer code review verification for any modifications to maintenance scripts or external network boundaries.
- Violation handling: Pull requests introducing unapproved third-party HTTP client dependencies or invalid network invocations will be blocked by automated review policies.
- Violation handling: Identified non-compliant network calls must be refactored to use standard runtime built-in fetch interfaces before merging.
- Exception process: Submit an architectural exception request detailing the specific technical constraints preventing the use of the runtime built-in fetch API, subject to review and sign-off by the engineering team.