---
version: 2
name: cross-cutting-developers-inspect-authoritative-reposit-a745
description: "Adoption of zod for Runtime Schema Validation and Parsing: Developers Inspect Authoritative Repository Lock Artifact"
metadata:
  actual:
    adr_id: a74549e1-c52b-4c65-a5f6-de1fc802bc64
    status: accepted
    candidate_group_id: 3e4f306d-7388-4290-bc8e-3639ded660c1
    evidence:
      source: deep
  scope:
    root: packages/resolution
    paths:
      - src/**
---

# Adoption of zod for Runtime Schema Validation and Parsing: Developers Inspect Authoritative Repository Lock Artifact

Scope: applies to `packages/resolution/src/**`.

These rules are ALWAYS ACTIVE for runtime input parsing, validation within module resolution entrypoints, and data contracts interfacing with external inputs across module formats.

### Rules

- **R-ZOD-001** MUST: Developers MUST inspect the authoritative repository lock artifact to determine the exact resolved dependency version before writing code that consumes the validation library.
- **R-ZOD-002** MANDATORY: Execute the lock-version grounding sequence (find manifest, identify build tool, inspect repository lock artifact for exact resolved version, look up official documentation for that exact version, confirm APIs exist, re-run per dependency at point of use) before using a versioned library.
- **R-ZOD-003** MANDATORY: Construct reusable schema objects for shared boundary primitives to prevent redundant declarations.
- **R-ZOD-004** MANDATORY: Infer static types directly from schema definitions to maintain synchronization between compile-time and runtime models.

### Verify

```bash
# Discover the project verification script from the repository manifest and execute validation suites:
# (Example discovery & execution workflow derived from repository manifest)
if [ -f package.json ]; then
  npm test
elif [ -f pnpm-lock.yaml ]; then
  pnpm test
elif [ -f yarn.lock ]; then
  yarn test
fi
```

**Accept when:**
- All boundary inputs are validated via schema parsing without manual type casting.
- Verification suites pass with schema validation tests confirming rejection of invalid inputs and acceptance of valid inputs.

<enforcement>
Claude Code MUST NOT skip or defer verification. Violation handling: Pull requests bypassing schema validation on external inputs are blocked from merging, and code review flags any unvalidated boundary type assertions for refactoring.
</enforcement>