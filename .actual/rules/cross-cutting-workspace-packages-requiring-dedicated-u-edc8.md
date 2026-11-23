---
version: 2
name: cross-cutting-workspace-packages-requiring-dedicated-u-edc8
description: "Package Test Project Configuration Composition via vitest/config: Workspace Packages Requiring Dedicated Unit Test"
metadata:
  actual:
    adr_id: edc80f9a-032b-4c57-afa7-d0f5f09095cc
    status: accepted
    candidate_group_id: 682b8cfd-bb53-4c8c-8bb2-12185574b204
    evidence:
      source: deep
  scope:
    root: packages/zod
---

# Package Test Project Configuration Composition via vitest/config: Workspace Packages Requiring Dedicated Unit Test

Scope: applies to `packages/zod/**`.

These rules are ALWAYS ACTIVE for:
- Workspace packages requiring package-specific unit testing configurations within a multi-package repository.
- Test configurations that extend shared workspace baseline settings.

### Rules

- **R-TS-001** MUST: Workspace packages requiring dedicated unit test project definitions MUST define their test project by importing defineProject from vitest/config.

### Verify

- find . -maxdepth 3 -type f -exec grep -l "defineProject" {} +
- find . -maxdepth 3 -type f -exec grep -l "mergeConfig" {} +
- REPO_ROOT=$(git rev-parse --show-toplevel 2>/dev/null || pwd) && grep -rn "from [\"']vitest/config[\"']" "$REPO_ROOT"

**Accept when:**

- Package test configuration modules import defineProject and mergeConfig from vitest/config.
- Package test project definitions compose the shared root configuration with package-specific overrides via mergeConfig.
- Project test verification directives execute package test suites without configuration composition errors.

<enforcement>
Claude Code MUST NOT skip or defer verification.
- Verified by: Automated continuous integration pipeline executing test suites across all workspace projects.
- Verified by: Static analysis checks verifying defineProject and mergeConfig imports in package configuration files.
- Verified by: Peer review on pull requests modifying test configuration definitions.
- Violation handling: Pull requests introducing unmerged or duplicate package test configurations are rejected during code review.
- Violation handling: Continuous integration failures resulting from invalid project configuration composition block merging.
- Exception process: Packages requiring an incompatible test runner paradigm must submit an architectural exception documenting why configuration inheritance cannot be used.
- Exception process: Exceptions require approval from repository maintainers and must be documented within the package directory.
</enforcement>
