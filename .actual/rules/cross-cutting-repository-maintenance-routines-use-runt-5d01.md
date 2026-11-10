---
version: 2
name: cross-cutting-repository-maintenance-routines-use-runt-5d01
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

Scope: applies to `scripts/**`.

These rules are ALWAYS ACTIVE for repository automation, maintenance scripts performing outbound network requests to external services, and standalone utility routines querying remote registries or external service endpoints.

### Rules

- **R-MAINT-001** MUST: Repository maintenance routines MUST use the runtime built-in fetch interface for outbound HTTP communications when no shared internal client abstraction is required.

### Verify

```bash
# Discover and execute the repository type-checking routine
# Discover and run the project static analysis and linting verification scripts
# Discover and run the project test suite
```

**Accept when:**
- All outbound HTTP invocations in maintenance scripts use the runtime built-in fetch interface without external client dependencies.
- Type checking and static analysis verification scripts pass without errors across all script modules.
- Network response handling verifies status codes and safely parses payloads across external client invocation points.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>