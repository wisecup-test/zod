---
version: 2
name: cross-cutting-configurations-requiring-explicit-typing-784e
description: "Adoption of vitest/config Module for Standardized Test Harness Configuration: Configurations Requiring Explicit Typing Leverage Viteuserconfig"
metadata:
  actual:
    adr_id: 784ebfa1-749e-4f08-ae37-c052d15d9ccb
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

# Adoption of vitest/config Module for Standardized Test Harness Configuration: Configurations Requiring Explicit Typing Leverage Viteuserconfig

Scope: applies to the whole repository; excludes `!packages/bench/**`, `!packages/docs/**`, `!packages/integration/**`, `!packages/mini/**`, `!packages/resolution/**`, `!packages/treeshake/**`, `!packages/tsc/**`, `!packages/zod/**`.

These rules are ALWAYS ACTIVE for all test harness configuration files across root and package contexts.

### Rules

- **R-VIT-001** SHOULD: Configurations requiring explicit typing leverage the ViteUserConfig type interface provided by the configuration module.
- **R-VIT-002** MANDATORY: Consumers must execute lock-version grounding, inspecting repository lock or resolution artifacts to determine exact resolved versions before using version-sensitive library APIs.

### Verify

```bash
# Discover dependency manifest and lock artifact, verify resolved dependency entry
# Run the project verification pipeline to validate test configuration integrity
npm test -- --run
```

**Accept when:**
- All test configuration definitions export structures declared through the adopted configuration factory API.
- Repository lock verification confirms synchronization between the active environment and declared dependency ranges.

<enforcement>
Claude Code MUST NOT skip or defer verification. All test configurations must use the standardized configuration factory API and adhere to lock-file grounding requirements.
</enforcement>