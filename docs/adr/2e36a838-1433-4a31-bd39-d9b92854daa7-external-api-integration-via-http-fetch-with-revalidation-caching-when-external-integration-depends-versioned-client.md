---
version: 2
name: 2e36a838-1433-4a31-bd39-d9b92854daa7-external-api-integration-via-http-fetch-with-revalidation-caching-when-external-integration-depends-versioned-client
description: "External API Integration via HTTP Fetch with Revalidation Caching: When External Integration Depends Versioned Client"
metadata:
  actual:
    adr_id: 2e36a838-1433-4a31-bd39-d9b92854daa7
    status: accepted
    candidate_group_id: ca08aea7-a6f9-4743-961c-6e451b15f254
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - loaders/**
---

# External API Integration via HTTP Fetch with Revalidation Caching: When External Integration Depends Versioned Client

Status: proposed
Date: 2025-05-18
Deciders: Detection Pipeline (automated)

## Scope Paths

Root: `packages/docs`

Applies to:
- `loaders/**`

## Context

- External service data fetching is required to load remote statistics for documentation presentation
- Outbound requests require bearer token authentication sourced from runtime environment variables
- External API rate limits and transient network failures necessitate response caching and retry error logging

## Problem Statement

Documentation components requiring external service metrics must perform authenticated network calls without exhausting remote rate limits or failing silently during network interruptions.

## Decision

1. MUST: When external integration depends on versioned client libraries, consumers MUST inspect the repository lock artifact to verify the exact resolved version prior to implementation

## Policy Block

- MUST When external integration depends on versioned client libraries, consumers MUST inspect the repository lock artifact to verify the exact resolved version prior to implementation

In scope:
- Modules that perform outbound HTTP requests to external third-party services to retrieve metadata or public metrics

Out of scope:
- Internal cross-module function calls within the repository that do not cross network boundaries

## Rationale

- Caching external API responses with daily revalidation intervals reduces latency and prevents rate-limit exhaustion against third-party endpoints
- Isolating secrets resolution to runtime environment variables ensures external API tokens remain protected and environment-specific
- In-memory caching provides fast retrieval across internal calls during page generation

## Consequences

Positive:
- Reduces outbound HTTP calls to third-party endpoints through scheduled revalidation caching
- Prevents credential leakage by resolving authorization tokens dynamically at runtime
- Ensures visibility into transient remote failures through logged retry attempts

Negative:
- Data served to consumers may become stale within the revalidation caching window
- In-memory cache structures are ephemeral and do not persist across isolated process restarts

## Alternatives

- Direct unauthenticated and uncached remote fetching on every request (rejected)
  Rejected because: Exceeds third-party rate limits and increases page rendering latency significantly
  When valid: Valid only in local testing environments with mock network backends
- External distributed cache service (deferred)
  Rejected because: Introduces unnecessary operational complexity for low-frequency documentation metadata
  When valid: Valid when external data volumes or update frequencies exceed single-process memory limits

## Risks

- External service outages may cause repeated retry logging without successful data retrieval
  Mitigation: Return fallback values or cached entries when retry attempts are exhausted
  Owner: engineering team
- Expired or missing runtime authentication tokens will cause remote requests to fail with authentication errors
  Mitigation: Validate environment variable availability during initialization before issuing network requests
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
- Verify that all external client endpoints configure appropriate time-to-live revalidation parameters matching the data freshness requirements of the consuming presentation components
- Ensure error handlers log sufficient context including attempt count and diagnostic error details without exposing authentication headers

## Continuation Context


Verify commands:
- Discover and run the project repository typecheck script to verify external API client typings
- Discover and execute the project integration test suite to validate external client caching and retry behavior

Accept when:
- Static analysis and test suites execute without errors across all external client modules
- Mocked external requests confirm caching revalidation headers and retry logic function as specified

## Enforcement

- Verified by: Automated continuous integration test suites
- Verified by: Peer code review of data loader and external client implementations
- Violation handling: Pull requests lacking credential protection or caching configurations will be rejected during code review
- Exception process: Exceptions for endpoints requiring real-time updates without caching must be documented and approved by the engineering leads