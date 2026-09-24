# Adoption of zod/mini for Tree-Shakeable Schema Validation: Consumers Isolate Reusable Constraint Checks Across

These rules are ALWAYS ACTIVE for all workspace packages declaring schema definitions for input validation, payload verification, and runtime contract assertions, as well as performance-sensitive and bundle-constrained modules requiring modular validation pipelines.

### Rules

- **R-ZOD-001** SHOULD: Consumers SHOULD isolate reusable constraint checks across schema boundaries to maximize dead code elimination.

### Verify

```bash
# Discover the project test runner from the workspace manifest and execute test verification
# Discover the project build script to verify bundle treeshaking and schema resolution
# Inspect the repository lock artifact to confirm the exact resolved dependency version
```

**Accept when:**
- All schema definitions import runtime validation utilities from zod/mini and pass workspace verification.
- Functional constraint pipelines using check, minLength, maxLength, and related validators execute without runtime evaluation errors.
- Input data validation parsing resolves successfully on valid inputs and rejects invalid payloads with appropriate error structures.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>