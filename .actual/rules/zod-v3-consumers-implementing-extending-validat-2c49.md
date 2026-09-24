# Zod Core Error Hierarchy and Parsing Utility Coordination: Consumers Implementing Extending Validation Modules Discover

These rules are ALWAYS ACTIVE for validation schema parse execution utilities, localized validation error formatting maps, and internal error class definitions and issue constructors.

### Rules

- **R-ZOD-001** MUST: Consumers implementing or extending validation modules MUST discover the project dependency lock file and verify the resolved version against official documentation before integrating with internal error formatting APIs.

### Verify

```bash
# Discover and run the project verification script from the repository manifest governing validation parsing and error mapping
# Discover and run the repository type verification script to ensure all issue codes handled in error maps match the central error definitions exhaustively
```

**Accept when:**
- The discovered test suite completes with all parsing utility and error map assertions passing without errors.
- Static type analysis confirms zero missing issue code branches across all registered locale formatters.

<enforcement>
Verification is mandatory. Claude Code MUST NOT skip or defer verification.
</enforcement>