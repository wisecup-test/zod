---
version: 2
name: cross-cutting-scripts-reading-numeric-boolean-configur-9dca
description: "Direct process.env Runtime Configuration Access in Automation Scripts: Scripts Reading Numeric Boolean Configuration Variables"
metadata:
  actual:
    adr_id: 9dca4f26-fa4c-413c-9a75-b842ef08bbdb
    status: accepted
    candidate_group_id: 2cca4728-a9b2-4bc1-8b4e-e02788c4b31b
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - scripts/**
---

# Direct process.env Runtime Configuration Access in Automation Scripts: Scripts Reading Numeric Boolean Configuration Variables

Scope: applies to `scripts/**`.

These rules are ALWAYS ACTIVE for repository automation, validation, and maintenance scripts reading execution parameters and pipeline signaling variables.

### Rules

- **R-ENV-001** SHOULD: Scripts reading numeric or boolean configuration variables from process.env SHOULD parse and validate input strings before passing them to execution routines or schema constructors.

### Verify

```bash
# Discover and run the project repository script verification and type-checking suites across automation scripts.
# Execute the repository linting and static analysis suite to check for unvalidated environment variable references.
```

**Accept when:**
- All automation and maintenance scripts execute cleanly without unhandled undefined environment variable exceptions.
- Static analysis and type checking pass across all repository automation scripts without unhandled configuration types.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory.
</enforcement>