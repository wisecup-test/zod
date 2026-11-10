---
version: 2
name: cross-cutting-implementations-not-import-full-monolith-5765
description: "Adoption of @zod/mini for Modular Schema Validation: Implementations Not Import Full Monolithic Schema"
metadata:
  actual:
    adr_id: 57656487-df2f-4aae-a873-bfbde4d1570c
    status: accepted
    candidate_group_id: 19ba1074-3608-4fc6-9490-5ff43e413b98
    evidence:
      source: deep
  scope:
    root: packages/integration
    paths:
      - fixtures/internal-types/**
---

# Adoption of @zod/mini for Modular Schema Validation: Implementations Not Import Full Monolithic Schema

Scope: applies to `packages/integration/fixtures/internal-types/**`.

These rules are ALWAYS ACTIVE for modules defining runtime schema validation contracts, data transfer object validation, type integrity boundaries, and internal types/integration testing fixtures.

### Rules

- **R-ZOD-001** MUST_NOT: Implementations MUST_NOT import full monolithic schema validation libraries when @zod/mini provides equivalent schema definitions.

### Verify

\`\`\`bash
# Discover and run the project test execution script to evaluate schema validation suite passes.
# Discover and run the project type check script to ensure static type inference aligns with runtime schemas.
# Discover and run the project module build verification script across all supported module targets.
\`\`\`

**Accept when:**
- All schema validation test fixtures execute without parsing errors under both ECMAScript and CommonJS module formats.
- Static type checking completes with zero diagnostic errors across all schema definitions and inferred types.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>