---
version: 2
name: cross-cutting-external-requests-implement-retry-loops-68cc
description: "External API Integration via HTTP Fetch with Revalidation Caching: External Requests Implement Retry Loops Structured"
metadata:
  actual:
    adr_id: 68cc8902-f5ef-4ae7-be0f-792ebc502f99
    status: accepted
    candidate_group_id: ca08aea7-a6f9-4743-961c-6e451b15f254
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - loaders/**
---

# External API Integration via HTTP Fetch with Revalidation Caching: External Requests Implement Retry Loops Structured

Scope: applies to `packages/docs/loaders/**`.

These rules are ALWAYS ACTIVE for:
- Modules that perform outbound HTTP requests to external third-party services to retrieve metadata or public metrics

### Rules

- **R-IA-001** SHOULD: External requests SHOULD implement retry loops with structured error logging to record failed fetch attempts before returning cached or fallback values

### Verify

- Discover and run the project repository typecheck script to verify external API client typings
- Discover and execute the project integration test suite to validate external client caching and retry behavior

**Accept when:**

- Static analysis and test suites execute without errors across all external client modules
- Mocked external requests confirm caching revalidation headers and retry logic function as specified

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated continuous integration test suites
- Verified by: Peer code review of data loader and external client implementations
- Violation handling: Pull requests lacking credential protection or caching configurations will be rejected during code review
- Exception process: Exceptions for endpoints requiring real-time updates without caching must be documented and approved by the engineering leads
</enforcement>
