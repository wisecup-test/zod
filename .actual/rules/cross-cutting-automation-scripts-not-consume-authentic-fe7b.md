---
version: 2
name: cross-cutting-automation-scripts-not-consume-authentic-fe7b
description: "Direct process.env Runtime Configuration Access in Automation Scripts: Automation Scripts Not Consume Authentication Tokens"
metadata:
  actual:
    adr_id: fe7bd9cb-3657-4e44-a5e2-622e3a6cabbe
    status: accepted
    candidate_group_id: 2cca4728-a9b2-4bc1-8b4e-e02788c4b31b
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - scripts/**
---

# Direct process.env Runtime Configuration Access in Automation Scripts: Automation Scripts Not Consume Authentication Tokens

Scope: applies to `scripts/**`.

These rules are ALWAYS ACTIVE for repository automation, validation, and maintenance scripts reading execution parameters and pipeline signaling variables.

### Rules

- **R-AUTO-001** MUST_NOT: Automation scripts MUST NOT consume authentication tokens, private keys, or sensitive credentials directly via plain-text process.env references without dedicated credential masking or secret management isolation.

### Verify

```bash
# Discover and run the project repository script verification and type-checking suites across automation scripts
# Execute the repository linting and static analysis suite to check for unvalidated environment variable references
```

**Accept when:**
- All automation and maintenance scripts execute cleanly without unhandled undefined environment variable exceptions.
- Static analysis and type checking pass across all repository automation scripts without unhandled configuration types.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>