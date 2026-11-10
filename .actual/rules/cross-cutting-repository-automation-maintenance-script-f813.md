---
version: 2
name: cross-cutting-repository-automation-maintenance-script-f813
description: "Direct process.env Runtime Configuration Access in Automation Scripts: Repository Automation Maintenance Scripts Read Execution"
metadata:
  actual:
    adr_id: f813affa-2393-44ee-9c6e-b632b0bd4298
    status: accepted
    candidate_group_id: 2cca4728-a9b2-4bc1-8b4e-e02788c4b31b
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - scripts/**
---

# Direct process.env Runtime Configuration Access in Automation Scripts: Repository Automation Maintenance Scripts Read Execution

Scope: applies to `scripts/**`.

These rules are ALWAYS ACTIVE for all repository automation, validation, and maintenance scripts reading execution parameters and pipeline signaling variables.

### Rules

- **R-ENV-001** MUST: Repository automation and maintenance scripts MUST read execution configuration flags and pipeline signaling variables through process.env property references only when such values represent non-sensitive execution parameters.

### Verify

```bash
# Discover and run project repository script verification and type-checking suites across automation scripts
# Execute repository linting and static analysis suite to check for unvalidated environment variable references
```

**Accept when:**
- All automation and maintenance scripts execute cleanly without unhandled undefined environment variable exceptions.
- Static analysis and type checking pass across all repository automation scripts without unhandled configuration types.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory.
</enforcement>