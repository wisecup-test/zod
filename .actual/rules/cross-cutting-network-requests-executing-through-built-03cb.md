---
version: 2
name: cross-cutting-network-requests-executing-through-built-03cb
description: "Built-in Fetch API Boundary Usage for External Clients: Network Requests Executing Through Built Fetch"
metadata:
  actual:
    adr_id: 03cb0dac-f069-4ea1-9086-a50741b2a41d
    status: accepted
    candidate_group_id: 48ac7a63-f307-43b4-b15a-af8c15cf1e82
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - scripts/**
---

# Built-in Fetch API Boundary Usage for External Clients: Network Requests Executing Through Built Fetch

Scope: applies to `scripts/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-FETCH-001** MUST: Network requests executing through the built-in fetch interface MUST define explicit request headers including content types and authorization credentials when accessing authenticated endpoints.

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
Claude Code MUST NOT skip or defer verification. Automated static analysis and peer code review verification apply.
</enforcement>