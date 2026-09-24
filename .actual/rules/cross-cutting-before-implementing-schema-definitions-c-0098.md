# Adoption of zod/mini for Tree-Shakeable Schema Validation: Before Implementing Schema Definitions Consumers Discover

These rules are ALWAYS ACTIVE for all workspace packages declaring schema definitions for input validation, payload verification, and runtime contract assertions, as well as performance-sensitive and bundle-constrained modules requiring modular validation pipelines.

### Rules

- **R-ZOD-001** MUST: Before implementing schema definitions, consumers MUST discover the project package manifest and lock artifact to inspect and bind to the exact resolved library version.
- **R-ZOD-002** MUST: Import object and individual validator functions directly from the mini subpath rather than importing full monolithic suites when constructing complex object schemas.
- **R-ZOD-003** MUST: Encapsulate schema validation checks inside dedicated validation boundaries before passing validated domain payloads to internal business logic.

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
Claude Code MUST NOT skip or defer verification. Automated static analysis and code review verification enforce import paths and schema composition patterns; violations block pull requests.
</enforcement>