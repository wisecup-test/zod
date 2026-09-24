# Zod Core Error Hierarchy and Parsing Utility Coordination: Parse Execution Routines Decouple Issue Collection

These rules are ALWAYS ACTIVE for validation schema parse execution utilities, localized validation error formatting maps, and internal error class definitions and issue constructors.

### Rules

- **R-ZOD-001** MUST: Parse execution routines MUST decouple issue collection from message string construction by delegating error description generation to localized error mapping functions.

### Verify

```bash
# Discover the project verification script from the repository manifest and execute the test suite governing validation parsing and error mapping.
# Execute the repository type verification script to ensure all issue codes handled in error maps match the central error definitions exhaustively.
```

**Accept when:**
- The discovered test suite completes with all parsing utility and error map assertions passing without errors.
- Static type analysis confirms zero missing issue code branches across all registered locale formatters.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory via automated continuous integration tests, type verification pipelines, and peer code review.
</enforcement>