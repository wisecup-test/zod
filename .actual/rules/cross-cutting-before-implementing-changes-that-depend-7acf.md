---
version: 2
name: cross-cutting-before-implementing-changes-that-depend-7acf
description: "standard-schema Module Adoption: Before Implementing Changes That Depend External"
metadata:
  actual:
    adr_id: 7acfd961-d79e-4e54-944a-9dcac308f932
    status: accepted
    candidate_group_id: cde02561-665e-40aa-bc54-b52077956cb9
    evidence:
      source: deep
  scope:
    root: .
    paths:
      - packages/zod/src/v4/core/**
---

# standard-schema Module Adoption: Before Implementing Changes That Depend External

Scope: applies to `packages/zod/src/v4/core/**`.

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-STD-001** MUST: Before implementing changes that depend on external or shared specification packages, the consumer MUST discover the repository lock artifact and verify the exact resolved version and specification compliance.
- **R-STD-002** MANDATORY: When writing code that uses a versioned library, execute in order: (1) Find the dependency manifest in the repo. (2) Identify the build tool from the manifest. (3) Inspect the repository lock or resolution artifact to determine the exact resolved version. (4) Look up official documentation/changelog for that exact version. (5) Confirm every API, class, or function exists in that exact version's documentation before using it. (6) For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.

### Verify

```bash
# Discover the repository build and test script in the project manifest and execute the core test suite
BUILD_SCRIPT=$(npm pkg get scripts.test 2>/dev/null || echo "test")
eval "npm run $BUILD_SCRIPT"

# Discover and run linter and type-checker commands
LINT_SCRIPT=$(npm pkg get scripts.lint 2>/dev/null || echo "lint")
eval "npm run $LINT_SCRIPT"
```

**Accept when:**
- All core schema transformations and error definitions pass automated type-checking and unit test suites verifying conformity to the standard-schema module contracts.
- Dependency analysis confirms no cyclic dependencies or direct bypasses of the standard-schema module in core schema transformation modules.

<enforcement>
Claude Code MUST NOT skip or defer verification. All pull request builds fail if circular imports or standard-schema contract bypasses are introduced.
</enforcement>