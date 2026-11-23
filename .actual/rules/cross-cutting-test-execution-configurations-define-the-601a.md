---
version: 2
name: cross-cutting-test-execution-configurations-define-the-601a
description: "Adoption of vitest/config Module for Standardized Test Harness Configuration: Test Execution Configurations Define Their Configuration"
metadata:
  actual:
    adr_id: 601a0a45-3fc8-4d9d-a638-fe80ce647d36
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

# Adoption of vitest/config Module for Standardized Test Harness Configuration: Test Execution Configurations Define Their Configuration

Scope: applies to `**`; excludes `!packages/bench/**`, `!packages/docs/**`, `!packages/integration/**`, `!packages/mini/**`, `!packages/resolution/**`, `!packages/treeshake/**`, `!packages/tsc/**`, `!packages/zod/**`.

These rules are ALWAYS ACTIVE for:
- All test harness configuration files across root and package contexts.

### Rules

- **R-LM-001** MUST: All test execution configurations MUST define their configuration objects using the defineConfig helper exported by the vitest/config module.

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
