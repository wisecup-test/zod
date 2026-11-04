---
version: 2
name: cross-cutting-external-input-boundaries-integration-pa-c9c3
description: "Zod Schema Declaration and Runtime Validation: External Input Boundaries Integration Payloads Validated"
metadata:
  actual:
    adr_id: c9c30a56-24b5-4470-b11c-6cdca48a95eb
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

# Zod Schema Declaration and Runtime Validation: External Input Boundaries Integration Payloads Validated

Scope: applies to `packages/bench/**`, `packages/integration/fixtures/**`, `packages/resolution/src/**`, `packages/treeshake/**`, `play.ts`.

These rules are ALWAYS ACTIVE for external data ingestion points, API integration payloads, and boundary contracts across application modules.

### Rules

- **R-ZOD-001** MUST: All external input boundaries, integration payloads, and validated domain models MUST declare structural shapes using Zod schemas.

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