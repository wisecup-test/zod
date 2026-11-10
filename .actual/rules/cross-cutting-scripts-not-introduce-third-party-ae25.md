---
version: 2
name: cross-cutting-scripts-not-introduce-third-party-ae25
description: "Built-in Fetch API Boundary Usage for External Clients: Scripts Not Introduce Third Party Http"
metadata:
  actual:
    adr_id: ae25057b-a928-4347-9421-6b765173741c
    status: accepted
    candidate_group_id: 48ac7a63-f307-43b4-b15a-af8c15cf1e82
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - scripts/**
---

# Built-in Fetch API Boundary Usage for External Clients: Scripts Not Introduce Third Party Http

Scope: applies to `scripts/**`.

These rules are ALWAYS ACTIVE for repository automation and maintenance scripts performing outbound network requests to external services, and standalone utility routines querying remote registries or external service endpoints.

### Rules

- **R-FETCH-001** MUST_NOT: Scripts MUST NOT introduce third-party HTTP client libraries for routine remote queries when runtime built-in fetch satisfies communication requirements.

### Verify

```bash
# Discover and execute repository type-checking routine
# Discover and run project static analysis and linting verification scripts
# Discover and run project test suite
```

**Accept when:**
- All outbound HTTP invocations in maintenance scripts use the runtime built-in fetch interface without external client dependencies.
- Type checking and static analysis verification scripts pass without errors across all script modules.
- Network response handling verifies status codes and safely parses payloads across external client invocation points.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>