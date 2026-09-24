# Zod Core Error Hierarchy and Parsing Utility Coordination: Validation Failures Emitted During Parse Operations

These rules are ALWAYS ACTIVE for validation schema parse execution utilities, localized validation error formatting maps, and internal error class definitions.

### Rules

- **R-ZOD-001** MUST: All validation failures emitted during parse operations MUST conform to the structured issue schema established by the central error class hierarchy.

### Verify

```bash
# Discover and execute the project verification script from the repository manifest for validation parsing and error mapping
# Execute the repository type verification script to ensure all issue codes handled in error maps match the central error definitions exhaustively
```

**Accept when:**
- The discovered test suite completes with all parsing utility and error map assertions passing without errors.
- Static type analysis confirms zero missing issue code branches across all registered locale formatters.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated continuous integration test and type verification pipelines as well as peer code review.
</enforcement>