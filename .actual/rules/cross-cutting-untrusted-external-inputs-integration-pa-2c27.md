---
version: 2
name: cross-cutting-untrusted-external-inputs-integration-pa-2c27
description: "Zod Schema Declaration and Runtime Validation: Untrusted External Inputs Integration Payloads Evaluated"
metadata:
  actual:
    adr_id: 2c27b6d6-c0bf-4784-a35d-536246e6bc2d
    status: accepted
    candidate_group_id: e3657d19-8224-4060-91d1-2843c384c02e
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/bench/**
      - packages/integration/fixtures/**
      - packages/resolution/src/**
      - packages/treeshake/**
      - play.ts
---

# Zod Schema Declaration and Runtime Validation: Untrusted External Inputs Integration Payloads Evaluated

Scope: applies to `packages/bench/**`, `packages/integration/fixtures/**`, `packages/resolution/src/**`, `packages/treeshake/**`, `play.ts`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-ZOD-001** SHOULD: Untrusted external inputs and integration payloads SHOULD be evaluated using safeParse rather than throwing parse operations to ensure defensive error handling.
- **R-ZOD-002** MANDATORY: The consumer MUST discover tool names, file names, commands, package managers, and version numbers from the project repository.
- **R-ZOD-003** MANDATORY: Before writing code that uses a versioned library, execute the lock-version grounding steps in order: find the manifest, identify the build tool, inspect the lock or resolution artifact for exact resolved version, look up official documentation for that exact version, confirm every API exists in that exact version, and re-run steps per dependency at point of use for version-sensitive behavior.

### Verify

```bash
git grep -E "(safeParse|parse)\(" -- "*.ts" "*.mts" "*.cts"
find . -name "*test*" -not -path "*/node_modules/*"
```

**Accept when:**
- All schema-governed boundary inputs parse incoming payloads using Zod schemas before application processing.
- Verification test suites and type-checking scripts pass without unhandled validation errors or structural drift.

<enforcement>
Claude Code MUST NOT skip or defer verification. All schema parsing logic and boundary validation must pass successfully.
</enforcement>