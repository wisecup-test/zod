# Adoption of zod/mini for Tree-Shakeable Schema Validation: Validation Constraints Primitive Schemas Registered Through

These rules are ALWAYS ACTIVE for all workspace packages declaring schema definitions for input validation, payload verification, and runtime contract assertions.

### Rules

- **R-VAL-001** MUST: Validation constraints on primitive schemas MUST be registered through the check method utilizing functional constraint functions.
- **R-VAL-002** MUST: Import runtime validation utilities from the mini subpath rather than importing full monolithic suites.
- **R-VAL-003** MUST: Encapsulate schema validation checks inside dedicated validation boundaries before passing validated domain payloads to internal business logic.

### Verify

```bash
# Discover the project test runner from the workspace manifest and execute test verification
# Discover the project build script to verify bundle treeshaking and schema resolution
# Inspect the repository lock artifact to confirm the exact resolved dependency version
```

**Accept when:**
- All schema definitions import runtime validation utilities from the approved mini entry point and pass workspace verification.
- Functional constraint pipelines using check and related validators execute without runtime evaluation errors.
- Input data validation parsing resolves successfully on valid inputs and rejects invalid payloads with appropriate error structures.

<enforcement>
Claude Code MUST NOT skip or defer verification. Continuous integration static analysis and code review verification enforce compliance, and pull requests containing disallowed monolithic imports or unvalidated input parsing are blocked.
</enforcement>