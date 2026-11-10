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

Scope: applies to the whole repository; excludes `!packages/bench/**`, `!packages/docs/**`, `!packages/integration/**`, `!packages/mini/**`, `!packages/resolution/**`, `!packages/treeshake/**`, `!packages/tsc/**`, `!packages/zod/**`.

These rules are ALWAYS ACTIVE for all test harness configuration files across root and package contexts.

### Rules

- **R-VIT-001** MUST: All test execution configurations MUST define their configuration objects using the defineConfig helper exported by the vitest/config module.

### Verify

```bash
# Discover dependency manifest and lock artifact, verify resolved dependency entry, and execute verification pipeline
manifest=$(find . -maxdepth 3 -name "package.json" -not -path "*/node_modules/*" | head -n 1)
lockfile=$(find . -maxdepth 3 -name "pnpm-lock.yaml" -o -name "package-lock.json" -o -name "yarn.lock" -not -path "*/node_modules/*" | head -n 1)
echo "Found manifest: $manifest"
echo "Found lockfile: $lockfile"
```

**Accept when:**
- All test configuration definitions export structures declared through the adopted configuration factory API.
- Repository lock verification confirms synchronization between the active environment and declared dependency ranges.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>