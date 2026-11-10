---
version: 2
name: cross-cutting-developers-discover-ecosystem-lock-artif-3485
description: "Adoption of vitest/config Module for Standardized Test Harness Configuration: Developers Discover Ecosystem Lock Artifact Verify"
metadata:
  actual:
    adr_id: 3485d055-8d1f-4b8e-9b5e-7879300512d6
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

# Adoption of vitest/config Module for Standardized Test Harness Configuration: Developers Discover Ecosystem Lock Artifact Verify

Scope: applies to the whole repository; excludes `!packages/bench/**`, `!packages/docs/**`, `!packages/integration/**`, `!packages/mini/**`, `!packages/resolution/**`, `!packages/treeshake/**`, `!packages/tsc/**`, `!packages/zod/**`.

These rules are ALWAYS ACTIVE for all test harness configuration files across root and package contexts.

### Rules

- **R-VIT-001** MUST: Developers MUST discover the ecosystem lock artifact and verify the exact resolved version of vitest/config before authoring or modifying configuration structures.
- **R-VIT-002** MUST: Test configurations must import configuration builder primitives directly from the designated configuration module rather than composing untyped configuration hashes.
- **R-VIT-003** SHOULD: Path resolution within configuration modules should leverage standard platform runtime modules to ensure consistent URI and path normalization across operating systems.

### Verify

```bash
# Discover the repository dependency manifest and lock artifact, verify the resolved dependency entry, and execute the project verification pipeline to validate configuration integrity.
find . -name "package.json" -o -name "pnpm-lock.yaml" -o -name "package-lock.json" -o -name "yarn.lock"
```

**Accept when:**
- All test configuration definitions export structures declared through the adopted configuration factory API.
- Repository lock verification confirms synchronization between the active environment and declared dependency ranges.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>