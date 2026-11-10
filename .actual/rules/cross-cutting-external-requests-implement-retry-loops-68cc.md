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

These rules are ALWAYS ACTIVE for modules that perform outbound HTTP requests to external third-party services to retrieve metadata or public metrics.

### Rules

- **R-EXT-001** SHOULD: External requests SHOULD implement retry loops with structured error logging to record failed fetch attempts before returning cached or fallback values.
- **R-EXT-002** MANDATORY: This ADR omits all tool names, file names, commands, package managers, and version numbers. The consumer MUST derive them from the project repository.
- **R-EXT-003** MANDATORY: Before writing code that uses a versioned library, execute in order: 1. Find dependency manifest. 2. Identify build tool. 3. Inspect repository lock or resolution artifact. 4. Look up official documentation for that exact version. 5. Confirm API/class/function existence. 6. Re-run per dependency at point of use.
- **R-EXT-004** MANDATORY: Verify that all external client endpoints configure appropriate time-to-live revalidation parameters matching data freshness requirements of consuming presentation components.
- **R-EXT-005** MANDATORY: Ensure error handlers log sufficient context including attempt count and diagnostic error details without exposing authentication headers.

### Verify

```bash
# Discover and run the project repository typecheck script
# Discover and execute the project integration test suite to validate external client caching and retry behavior
```

**Accept when:**
- Static analysis and test suites execute without errors across all external client modules
- Mocked external requests confirm caching revalidation headers and retry logic function as specified

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory via automated continuous integration test suites and peer code reviews.
</enforcement>