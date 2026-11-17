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

These rules are ALWAYS ACTIVE for all modules that perform outbound HTTP requests to external third-party services to retrieve metadata or public metrics.

### Rules

- **R-EXT-001** MUST: When external integration depends on versioned client libraries, consumers MUST inspect the repository lock artifact to verify the exact resolved version prior to implementation.
- **R-EXT-002** MUST: Execute lock-version grounding in order (find manifest, identify build tool, inspect lock/resolution artifact, look up official documentation for exact version, confirm every API/class/function exists, and re-run per dependency at point of use).
- **R-EXT-003** MUST: Configure appropriate time-to-live revalidation parameters matching the data freshness requirements of consuming presentation components.
- **R-EXT-004** MUST: Ensure error handlers log sufficient context including attempt count and diagnostic error details without exposing authentication headers.

### Verify

```bash
# Discover and run the project repository typecheck script
# Discover and execute the project integration test suite
```

**Accept when:**
- Static analysis and test suites execute without errors across all external client modules
- Mocked external requests confirm caching revalidation headers and retry logic function as specified

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated continuous integration test suites and peer code review.
</enforcement>