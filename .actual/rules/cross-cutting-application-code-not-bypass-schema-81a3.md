---
version: 2
name: cross-cutting-application-code-not-bypass-schema-81a3
description: "Zod Schema Declaration and Runtime Validation: Application Code Not Bypass Schema Validation"
metadata:
  actual:
    adr_id: 81a396b9-e378-4342-a4a0-02022a554528
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

# Zod Schema Declaration and Runtime Validation: Application Code Not Bypass Schema Validation

Scope: applies to `packages/bench/**`, `packages/integration/fixtures/**`, `packages/resolution/src/**`, `packages/treeshake/**`, `play.ts`.

These rules are ALWAYS ACTIVE for external data ingestion points, API integration payloads, and boundary contracts across application modules.

### Rules

- **R-ZOD-001** MUST_NOT: Application code MUST_NOT bypass schema validation by asserting raw untrusted data directly to internal types without running schema parsing.

### Verify

```bash
git grep -E "(safeParse|parse)\\(" -- "*.ts" "*.mts" "*.cts"
find . -name "*test*" -not -path "*/node_modules/*"
```

**Accept when:**
- All schema-governed boundary inputs parse incoming payloads using Zod schemas before application processing.
- Verification test suites and type-checking scripts pass without unhandled validation errors or structural drift.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>