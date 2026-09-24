# Adoption of zod/mini for Tree-Shakeable Schema Validation: Schemas Provide Custom Locale Messages Within

These rules are ALWAYS ACTIVE for all workspace packages declaring schema definitions for input validation, payload verification, and runtime contract assertions.

### Rules

- **R-ZOD-001** MAY: Schemas MAY provide custom locale messages within individual constraint functions to satisfy localized error requirements.
- **R-ZOD-002** MANDATORY: When constructing complex object schemas, import object and individual validator functions directly from the mini subpath rather than importing full monolithic suites.
- **R-ZOD-003** MANDATORY: Encapsulate schema validation checks inside dedicated validation boundaries before passing validated domain payloads to internal business logic.
- **R-ZOD-004** MANDATORY (LOCK-VERSION GROUNDING): Before writing code that uses a versioned library, execute in order: (1) Find dependency manifest in the repo. (2) Identify build tool from manifest. (3) Inspect repository lock or resolution artifact to determine exact resolved version. (4) Look up official documentation, changelog, or public API reference for that exact version. (5) Confirm every API, class, or function you will call exists in that exact version's documentation before using it. (6) For version-sensitive behavior, re-run steps 3-5 per dependency at point of use.

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
Claude Code MUST NOT skip or defer verification. Automated static analysis and linting checks in continuous integration pipelines verify compliance, and pull requests containing disallowed monolithic imports or unvalidated input parsing are blocked until corrected.
</enforcement>