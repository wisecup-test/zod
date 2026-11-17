---
version: 2
name: cross-cutting-engineers-discover-ecosystem-lock-artifa-ec60
description: "Built-in Fetch API Boundary Usage for External Clients: Engineers Discover Ecosystem Lock Artifact Verify"
metadata:
  actual:
    adr_id: ec6080ad-6f71-4e55-ac85-23d5088fb414
    status: accepted
    candidate_group_id: 48ac7a63-f307-43b4-b15a-af8c15cf1e82
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - scripts/**
---

# Built-in Fetch API Boundary Usage for External Clients: Engineers Discover Ecosystem Lock Artifact Verify

Scope: applies to `scripts/**`.

These rules are ALWAYS ACTIVE for repository automation, maintenance scripts, and standalone utility routines performing outbound network requests to external services.

### Rules

- **R-FETCH-001** MUST: Engineers MUST discover the ecosystem lock artifact to verify the runtime environment and any associated dependencies before introducing external network utilities.
- **R-FETCH-002** MUST: Outbound HTTP invocations in maintenance scripts MUST use the runtime built-in fetch interface without external client dependencies.
- **R-FETCH-003** MUST: Network calls MUST retrieve credentials strictly from runtime environment variables rather than persisting credentials in source or configuration files.
- **R-FETCH-004** MUST: Network response handling MUST verify status codes and safely parse payloads across external client invocation points.

### Verify

```bash
# Discover and execute repository type-checking routine to confirm fetch invocation compliance
# Discover and run static analysis and linting verification scripts
# Discover and run the project test suite to validate network response handling
```

**Accept when:**
- All outbound HTTP invocations in maintenance scripts use the runtime built-in fetch interface without external client dependencies.
- Type checking and static analysis verification scripts pass without errors across all script modules.
- Network response handling verifies status codes and safely parses payloads across external client invocation points.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>