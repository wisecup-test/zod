---
version: 2
name: cross-cutting-test-configurations-not-export-unvalidat-240b
description: "Adoption of vitest/config Module for Standardized Test Harness Configuration: Test Configurations Not Export Unvalidated Plain"
metadata:
  actual:
    adr_id: 240b0ffa-9927-4352-a715-922a55bd70b7
    status: accepted
    candidate_group_id: faecdf74-995d-4074-a45b-1d15234f9404
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - "**"
      - "!packages/bench/**"
      - "!packages/docs/**"
      - "!packages/integration/**"
      - "!packages/mini/**"
      - "!packages/resolution/**"
      - "!packages/treeshake/**"
      - "!packages/tsc/**"
      - "!packages/zod/**"
---

# Adoption of vitest/config Module for Standardized Test Harness Configuration: Test Configurations Not Export Unvalidated Plain

Scope: applies to the whole repository; excludes `!packages/bench/**`, `!packages/docs/**`, `!packages/integration/**`, `!packages/mini/**`, `!packages/resolution/**`, `!packages/treeshake/**`, `!packages/tsc/**`, `!packages/zod/**`.

These rules are ALWAYS ACTIVE for all test harness configuration files across root and package contexts.

### Rules

- **R-VIT-001** MUST_NOT: Test configurations MUST NOT export unvalidated plain JavaScript objects or bypass the standard configuration factory.

### Verify

```bash
# Discover the repository dependency manifest and lock artifact, verify the resolved dependency entry, and execute the project verification pipeline to validate configuration integrity.
```

**Accept when:**
- All test configuration definitions export structures declared through the adopted configuration factory API.
- Repository lock verification confirms synchronization between the active environment and declared dependency ranges.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated static analysis verifying that test configuration files consume the designated configuration factory API and code reviews checking adherence to lock-file grounding and module isolation rules.
</enforcement>