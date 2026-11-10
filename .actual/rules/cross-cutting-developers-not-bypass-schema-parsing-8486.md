---
version: 2
name: cross-cutting-developers-not-bypass-schema-parsing-8486
description: "Adoption of zod for Runtime Schema Validation and Parsing: Developers Not Bypass Schema Parsing Casting"
metadata:
  actual:
    adr_id: 84869ef4-f79b-48e7-abfe-301415848a8c
    status: accepted
    candidate_group_id: 3e4f306d-7388-4290-bc8e-3639ded660c1
    evidence:
      source: deep
  scope:
    root: packages/resolution
    paths:
      - src/**
---

# Adoption of zod for Runtime Schema Validation and Parsing: Developers Not Bypass Schema Parsing Casting

Scope: applies to `packages/resolution/src/**`.

These rules are ALWAYS ACTIVE for runtime input parsing and validation within module resolution entrypoints and data contracts interfacing with external inputs.

### Rules

- **R-ZOD-001** MUST_NOT: Developers MUST_NOT bypass schema parsing by casting unvalidated external input directly to expected internal types.

### Verify

```bash
# Discover the project verification script from the repository manifest and execute validation suites.
# Discover and run the project test execution command to verify schema parsing tests pass across all module entrypoints.
npm test
```

**Accept when:**
- All boundary inputs are validated via schema parsing without manual type casting.
- Verification suites pass with schema validation tests confirming rejection of invalid inputs and acceptance of valid inputs.

<enforcement>
Claude Code MUST NOT skip or defer verification. Continuous integration test execution, automated code review, and peer review enforce these rules, and pull requests bypassing schema validation are blocked.
</enforcement>