---
version: 2
name: cross-cutting-static-application-types-derived-directl-ea7e
description: "Zod Schema Declaration and Runtime Validation: Static Application Types Derived Directly Zod"
metadata:
  actual:
    adr_id: ea7ed3ae-cba6-4068-a596-1f71fb15488b
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

# Zod Schema Declaration and Runtime Validation: Static Application Types Derived Directly Zod

Scope: applies to `packages/bench/**`, `packages/integration/fixtures/**`, `packages/resolution/src/**`, `packages/treeshake/**`, `play.ts`.

These rules are ALWAYS ACTIVE for external data ingestion points, API integration payloads, boundary contracts across application modules, and data model validation logic requiring synchronization between runtime assertions and static typing.

### Rules

- **R-ZOD-001** SHOULD: Static application types SHOULD be derived directly from Zod schema definitions through schema type inference to prevent drift between runtime validation rules and compile-time types.

### Verify

```bash
git grep -E "(safeParse|parse)\\(" -- "*.ts" "*.mts" "*.cts"
find . -name "*test*" -not -path "*/node_modules/*"
```

**Accept when:**
- All schema-governed boundary inputs parse incoming payloads using Zod schemas before application processing.
- Verification test suites and type-checking scripts pass without unhandled validation errors or structural drift.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated test suites exercising schema parsing logic and boundary validation, as well as static analysis and architectural review of data entry points and external integration layers.
</enforcement>