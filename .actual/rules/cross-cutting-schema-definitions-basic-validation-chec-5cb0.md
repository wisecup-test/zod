---
version: 2
name: cross-cutting-schema-definitions-basic-validation-chec-5cb0
description: "Core Module Architecture for Validation Engine and Global Registry Management: Schema Definitions Basic Validation Checks Error"
metadata:
  actual:
    adr_id: 5cb066dd-1903-4568-8233-a7da6b218f53
    status: accepted
    candidate_group_id: d439e3f0-eafd-4b71-a843-e881f89e04eb
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/v4/**
---

# Core Module Architecture for Validation Engine and Global Registry Management: Schema Definitions Basic Validation Checks Error

Scope: applies to `packages/zod/src/v4/**`.

These rules are ALWAYS ACTIVE for all schema definitions, validation checks, error representations, global registry services, transformation processors, and compatibility adapters within the project.

### Rules

- **R-CORE-001** MUST: Define all schema definitions, basic validation checks, error structures, and registry services within and consume them from the internal core module layer.
- **R-CORE-002** MANDATORY: Execute lock-version grounding before writing code that uses a versioned library (find dependency manifest, identify build tool, inspect lock/resolution artifact, look up official documentation for that exact version, confirm API existence, and re-run per dependency at point of use).
- **R-CORE-003** MANDATORY: Organize internal imports so that dependent compatibility and transformation layers access core modules via relative boundary entry points without circumventing internal directory scoping.
- **R-CORE-004** MANDATORY: Implement custom validation logic as discrete check primitives within the core layer before registering public schema methods when extending schema parsing behavior.

### Verify

```bash
# Discover and run static analysis and linting command for module boundary compliance
# Discover and execute test runner across core module test suites
# Discover and execute circular dependency checker script defined in project configuration
```

**Accept when:**
- All core module test suites complete with zero errors.
- Static dependency validation passes without detecting disallowed inward imports into the core module layer.
- Schema registry resolution tests verify deterministic cache lookups across compatibility facades.

<enforcement>
Claude Code MUST NOT skip or defer verification. All pull requests introducing backward dependencies into core modules or circumventing the global registry are automatically blocked.
</enforcement>