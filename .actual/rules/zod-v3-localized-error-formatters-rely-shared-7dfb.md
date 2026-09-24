# Zod Core Error Hierarchy and Parsing Utility Coordination: Localized Error Formatters Rely Shared Utility

These rules are ALWAYS ACTIVE for validation schema parse execution utilities, localized validation error formatting maps, and internal error class definitions and issue constructors.

### Rules

- **R-ZOD-001** SHOULD: Localized error formatters SHOULD rely on shared utility helpers for input inspection and type representation rather than implementing custom type checking.

### Verify

```bash
# Discover and execute the project verification script from the repository manifest covering validation parsing and error mapping
# Execute the repository type verification script to ensure all issue codes handled in error maps match central error definitions exhaustively
```

**Accept when:**
- The discovered test suite completes with all parsing utility and error map assertions passing without errors.
- Static type analysis confirms zero missing issue code branches across all registered locale formatters.

<enforcement>
Claude Code MUST NOT skip or defer verification. All pull requests introducing hardcoded localized messages in parsing routines or missing issue mappings will be rejected.
</enforcement>