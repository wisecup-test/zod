---
version: 2
name: cross-cutting-engineers-discover-ecosystem-lock-artifa-84c3
description: "Direct process.env Runtime Configuration Access in Automation Scripts: Engineers Discover Ecosystem Lock Artifact Confirm"
metadata:
  actual:
    adr_id: 84c3922c-9359-452a-a457-3c46b8e8abe9
    status: accepted
    candidate_group_id: 2cca4728-a9b2-4bc1-8b4e-e02788c4b31b
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - scripts/**
---

# Direct process.env Runtime Configuration Access in Automation Scripts: Engineers Discover Ecosystem Lock Artifact Confirm

Scope: applies to `scripts/**`.

These rules are ALWAYS ACTIVE for all repository automation, validation, and maintenance scripts reading execution parameters and pipeline signaling variables.

### Rules

- **R-ENV-001** MUST: Engineers MUST discover the ecosystem lock artifact and confirm all dependency versions prior to introducing external environment parsing libraries.
- **R-ENV-002** MUST: Discover repository script definitions through the project configuration manifest and verify environment variable requirements prior to script execution.
- **R-ENV-003** MUST: Ensure all environment variable access points define clear fallback default values when variables are omitted in local development environments.
- **R-ENV-004** MUST: Enforce strict isolation between operational execution flags and secrets, and avoid dumping environment dictionaries to logging streams.
- **R-ENV-005** MUST: Implement defensive presence checks and explicit string-to-number validation with fallback defaults for environment variables.

### Verify

```bash
# Discover and run repository script verification, type-checking, and linting suites across automation scripts
npm test -- --runInBand || yarn test
npm run lint || yarn lint
```

**Accept when:**
- All automation and maintenance scripts execute cleanly without unhandled undefined environment variable exceptions.
- Static analysis and type checking pass across all repository automation scripts without unhandled configuration types.

<enforcement>
Claude Code MUST NOT skip or defer verification. Pull requests introducing unvalidated or sensitive credential handling via plain environment variables are blocked until remediated.
</enforcement>