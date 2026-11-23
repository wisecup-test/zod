---
version: 2
name: cross-cutting-when-external-integration-depends-versio-2e36
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

Scope: applies to `packages/docs/loaders/**`.

These rules are ALWAYS ACTIVE for:
- Modules that perform outbound HTTP requests to external third-party services to retrieve metadata or public metrics

### Rules

- **R-IA-001** MUST: When external integration depends on versioned client libraries, consumers MUST inspect the repository lock artifact to verify the exact resolved version prior to implementation

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
