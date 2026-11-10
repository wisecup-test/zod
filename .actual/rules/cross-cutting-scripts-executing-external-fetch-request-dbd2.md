---
version: 2
name: cross-cutting-scripts-executing-external-fetch-request-dbd2
description: "Built-in Fetch API Boundary Usage for External Clients: Scripts Executing External Fetch Requests Validate"
metadata:
  actual:
    adr_id: dbd23d15-00e7-4d18-9b88-eca9f2268679
    status: accepted
    candidate_group_id: 48ac7a63-f307-43b4-b15a-af8c15cf1e82
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - scripts/**
---

# Built-in Fetch API Boundary Usage for External Clients: Scripts Executing External Fetch Requests Validate

Scope: applies to `scripts/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-EXT-001** SHOULD: Scripts executing external fetch requests SHOULD validate network response statuses and parse payloads using standard runtime error handling mechanisms.

### Verify

```bash
# Discover and execute the repository type-checking routine to confirm that all fetch invocations conform to runtime signature requirements.
# Discover and run the project static analysis and linting verification scripts to ensure external network requests adhere to repository security and syntax standards.
# Discover and run the project test suite to validate that script routines communicating with external boundaries handle network responses correctly.
```

**Accept when:**
- All outbound HTTP invocations in maintenance scripts use the runtime built-in fetch interface without external client dependencies.
- Type checking and static analysis verification scripts pass without errors across all script modules.
- Network response handling verifies status codes and safely parses payloads across external client invocation points.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>