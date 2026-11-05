---
version: 2
name: cross-cutting-consumers-inspect-repository-lock-artifa-0ca2
description: "Core Module Architecture for Validation Engine and Global Registry Management: Consumers Inspect Repository Lock Artifact Verify"
metadata:
  actual:
    adr_id: 0ca2cf97-b2f9-4133-a116-58755d9f1455
    status: accepted
    candidate_group_id: d439e3f0-eafd-4b71-a843-e881f89e04eb
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/v4/**
---

# Core Module Architecture for Validation Engine and Global Registry Management: Consumers Inspect Repository Lock Artifact Verify

Scope: applies to `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for all code, modules, checks, errors, and global registry access within the project.

### Rules

- **R-CORE-001** MUST: Consumers MUST inspect the repository lock artifact to verify the exact resolved version of any external library dependency before authoring or integrating module-level consumers.

### Verify

```bash
# Discover and run the project static analysis and linting command to verify module boundary compliance.
# Discover and execute the project test runner across core module test suites.
# Discover and execute the circular dependency checker script defined in the project configuration.
```

**Accept when:**
- All core module test suites complete with zero errors.
- Static dependency validation passes without detecting disallowed inward imports into the core module layer.
- Schema registry resolution tests verify deterministic cache lookups across compatibility facades.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated dependency graph validation and static lint checks executed in continuous integration pipelines enforce compliance.
</enforcement>