# Adoption of zod/mini for Tree-Shakeable Schema Validation: Consumers Not Bypass Schema Parsing Unvalidated

These rules are ALWAYS ACTIVE for all workspace packages declaring schema definitions for input validation, payload verification, and runtime contract assertions, as well as performance-sensitive and bundle-constrained modules requiring modular validation pipelines.

### Rules

- **R-VAL-001** MUST_NOT: Consumers MUST_NOT bypass schema parsing on unvalidated external payloads prior to business domain processing.

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
Claude Code MUST NOT skip or defer verification. Verification is mandatory via automated static analysis, linting checks, and code reviews in continuous integration pipelines.
</enforcement>