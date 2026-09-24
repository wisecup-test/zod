# Zod Core Error Hierarchy and Parsing Utility Coordination: Internal Parsing Helpers Not Embed Hardcoded

These rules are ALWAYS ACTIVE for validation schema parse execution utilities, localized validation error formatting maps, and internal error class definitions and issue constructors.

### Rules

- **R-ZOD-001** MUST_NOT: Internal parsing helpers MUST NOT embed hardcoded locale-specific message templates within schema evaluation algorithms.

### Verify

```bash
# Discover and execute the project verification script from the repository manifest governing validation parsing and error mapping
# Discover and execute the repository type verification script to ensure all issue codes handled in error maps match central error definitions exhaustively
```

**Accept when:**
- The discovered test suite completes with all parsing utility and error map assertions passing without errors.
- Static type analysis confirms zero missing issue code branches across all registered locale formatters.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated continuous integration test and type verification pipelines, and peer code review.
</enforcement>