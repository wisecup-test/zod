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

These rules are ALWAYS ACTIVE for:
- Repository automation and maintenance scripts performing outbound network requests to external services.
- Standalone utility routines querying remote registries or external service endpoints.

### Rules

- **R-IA-001** MUST: Repository maintenance routines MUST use the runtime built-in fetch interface for outbound HTTP communications when no shared internal client abstraction is required.

### Verify

- Discover and execute the repository type-checking routine to confirm that all fetch invocations conform to runtime signature requirements.
- Discover and run the project static analysis and linting verification scripts to ensure external network requests adhere to repository security and syntax standards.
- Discover and run the project test suite to validate that script routines communicating with external boundaries handle network responses correctly.

**Accept when:**

- All outbound HTTP invocations in maintenance scripts use the runtime built-in fetch interface without external client dependencies.
- Type checking and static analysis verification scripts pass without errors across all script modules.
- Network response handling verifies status codes and safely parses payloads across external client invocation points.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated static analysis checks in continuous integration pipelines.
- Verified by: Peer code review verification for any modifications to maintenance scripts or external network boundaries.
- Violation handling: Pull requests introducing unapproved third-party HTTP client dependencies or invalid network invocations will be blocked by automated review policies.
- Violation handling: Identified non-compliant network calls must be refactored to use standard runtime built-in fetch interfaces before merging.
- Exception process: Submit an architectural exception request detailing the specific technical constraints preventing the use of the runtime built-in fetch API, subject to review and sign-off by the engineering team.
</enforcement>
