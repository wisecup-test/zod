---
version: 2
name: cross-cutting-data-loaders-maintain-memory-key-cc85
description: "External API Integration via HTTP Fetch with Revalidation Caching: Data Loaders Maintain Memory Key Value"
metadata:
  actual:
    adr_id: cc85913e-2f62-4acf-a405-18618a1cc46e
    status: accepted
    candidate_group_id: ca08aea7-a6f9-4743-961c-6e451b15f254
    evidence:
      source: deep
  scope:
    root: packages/docs
    paths:
      - loaders/**
---

# External API Integration via HTTP Fetch with Revalidation Caching: Data Loaders Maintain Memory Key Value

Scope: applies to `packages/docs/loaders/**`.

These rules are ALWAYS ACTIVE for modules that perform outbound HTTP requests to external third-party services to retrieve metadata or public metrics.

### Rules

- **R-EXT-001** SHOULD: Data loaders SHOULD maintain an in-memory key-value cache layer to serve retrieved entities across repeated internal queries.
- **R-EXT-002** MANDATORY: Outbound requests require bearer token authentication sourced from runtime environment variables.
- **R-EXT-003** MANDATORY: The consumer MUST follow lock-version grounding before writing code that uses a versioned library (find dependency manifest, identify build tool, inspect lock artifact, look up official documentation for that exact version, confirm every API/class/function exists).
- **R-EXT-004** MANDATORY: Verify that all external client endpoints configure appropriate time-to-live revalidation parameters matching the data freshness requirements of the consuming presentation components.
- **R-EXT-005** MANDATORY: Ensure error handlers log sufficient context including attempt count and diagnostic error details without exposing authentication headers.
- **R-EXT-006** MANDATORY: Validate environment variable availability during initialization before issuing network requests.

### Verify

```bash
# Discover and run the project repository typecheck script to verify external API client typings
# Discover and execute the project integration test suite to validate external client caching and retry behavior
```

**Accept when:**
- Static analysis and test suites execute without errors across all external client modules
- Mocked external requests confirm caching revalidation headers and retry logic function as specified

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated continuous integration test suites and peer code review.
</enforcement>