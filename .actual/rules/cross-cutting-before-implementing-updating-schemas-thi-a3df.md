---
version: 2
name: cross-cutting-before-implementing-updating-schemas-thi-a3df
description: "Zod Schema Declaration and Runtime Validation: Before Implementing Updating Schemas This Library"
metadata:
  actual:
    adr_id: a3dfaa71-990c-421b-85dc-82232e09dfb4
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

# Zod Schema Declaration and Runtime Validation: Before Implementing Updating Schemas This Library

Scope: applies to `packages/bench/**`, `packages/integration/fixtures/**`, `packages/resolution/src/**`, `packages/treeshake/**`, `play.ts`.

These rules are ALWAYS ACTIVE for external data ingestion points, API integration payloads, and boundary contracts across application modules.

### Rules

- **R-ZOD-001** MUST: Before implementing or updating schemas using this library, the consumer MUST inspect the repository lock artifact to determine the exact resolved dependency version and verify API compatibility against version-specific documentation.
- **R-ZOD-002** MUST: Define shared reusable schema primitives in dedicated module boundaries to prevent redundant schema definitions.
- **R-ZOD-003** PREFER: Prefer defensive parsing methods at public ingestion endpoints to capture structured issue reports without triggering uncaught exceptions.
- **R-ZOD-004** MUST: Enforce schema type inference as the single source of truth across all domain type definitions.

### Verify

```bash
git grep -E "(safeParse|parse)\(" -- "*.ts" "*.mts" "*.cts"
find . -name "*test*" -not -path "*/node_modules/*"
```

**Accept when:**
- All schema-governed boundary inputs parse incoming payloads using Zod schemas before application processing.
- Verification test suites and type-checking scripts pass without unhandled validation errors or structural drift.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>