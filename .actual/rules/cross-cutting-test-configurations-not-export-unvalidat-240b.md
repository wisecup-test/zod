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

Scope: applies to `**`; excludes `!packages/bench/**`, `!packages/docs/**`, `!packages/integration/**`, `!packages/mini/**`, `!packages/resolution/**`, `!packages/treeshake/**`, `!packages/tsc/**`, `!packages/zod/**`.

These rules are ALWAYS ACTIVE for:
- All test harness configuration files across root and package contexts.

### Rules

- **R-LM-001** MUST_NOT: Test configurations MUST NOT export unvalidated plain JavaScript objects or bypass the standard configuration factory.

### Verify

- Discover the repository dependency manifest and lock artifact, verify the resolved dependency entry, and execute the project verification pipeline to validate configuration integrity.

**Accept when:**

- All test configuration definitions export structures declared through the adopted configuration factory API.
- Repository lock verification confirms synchronization between the active environment and declared dependency ranges.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated static analysis verifying that test configuration files consume the designated configuration factory API.
- Verified by: Code reviews checking adherence to lock-file grounding and module isolation rules.
- Violation handling: Flagged configurations fail build and pull request checks until brought into compliance.
- Violation handling: Non-compliant configuration exports must be refactored to use the standardized configuration factory.
- Exception process: Submit an architectural exception request detailing why custom test execution flags cannot be expressed through the standard configuration factory.
- Exception process: Obtain review and sign-off from the architectural governance leads before committing unvalidated test configurations.
</enforcement>
