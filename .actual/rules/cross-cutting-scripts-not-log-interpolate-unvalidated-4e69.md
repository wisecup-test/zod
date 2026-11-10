---
version: 2
name: cross-cutting-scripts-not-log-interpolate-unvalidated-4e69
description: "Direct process.env Runtime Configuration Access in Automation Scripts: Scripts Not Log Interpolate Unvalidated Process"
metadata:
  actual:
    adr_id: 4e69fd0e-0898-4f8e-badb-ff150fd070ee
    status: accepted
    candidate_group_id: 2cca4728-a9b2-4bc1-8b4e-e02788c4b31b
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - scripts/**
---

# Direct process.env Runtime Configuration Access in Automation Scripts: Scripts Not Log Interpolate Unvalidated Process

Scope: applies to `scripts/**`.

These rules are ALWAYS ACTIVE for repository automation, validation, and maintenance scripts reading execution parameters and pipeline signaling variables.

### Rules

- **R-ENV-001** SHOULD_NOT: Scripts SHOULD_NOT log or interpolate unvalidated process.env configuration values into standard error or standard output streams where pipeline logs are visible.

### Verify

```bash
# Discover and run the project repository script verification and type-checking suites across automation scripts.
# Execute the repository linting and static analysis suite to check for unvalidated environment variable references.
```

**Accept when:**
- All automation and maintenance scripts execute cleanly without unhandled undefined environment variable exceptions.
- Static analysis and type checking pass across all repository automation scripts without unhandled configuration types.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>