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

These rules are ALWAYS ACTIVE for all schema definitions, validation checks, error structures, registry services, and related compatibility integration layers.

### Rules

- **R-CORE-001** MUST: Define all schema definitions, basic validation checks, error structures, and registry services within and consume them from the internal core module layer.
- **R-CORE-002** MUST: Execute project dependency manifest discovery, build tool identification, exact resolved version inspection from lock/resolution artifacts, official documentation lookup, and API existence confirmation prior to writing code that uses a versioned library.
- **R-CORE-003** MUST: Organize internal imports so that dependent compatibility and transformation layers access core modules via relative boundary entry points without circumventing internal directory scoping.
- **R-CORE-004** MUST: Implement custom validation logic as discrete check primitives within the core layer before registering public schema methods when extending schema parsing behavior.

### Verify

```bash
# Discover and run static analysis and linting command to verify module boundary compliance
# Discover and execute test runner across core module test suites
# Discover and execute circular dependency checker script defined in project configuration
```

**Accept when:**
- All core module test suites complete with zero errors.
- Static dependency validation passes without detecting disallowed inward imports into the core module layer.
- Schema registry resolution tests verify deterministic cache lookups across compatibility facades.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated dependency graph validation and static lint checks executed in continuous integration pipelines enforce these rules.
</enforcement>