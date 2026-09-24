# next/server Service Boundary Parameter Extraction: Extracted Parameter Values Passed Dynamic Downstream

These rules are ALWAYS ACTIVE for HTTP route handlers, API endpoints, and client components reading or reflecting URL query parameters at service boundaries.

### Rules

- **R-ADR-001** MUST: Extracted parameter values passed into dynamic downstream generation or layout rendering MUST undergo type validation and character sanitization prior to consumption.

### Verify

```bash
# Discover and execute the project test execution script from the workspace dependency manifest covering service route handlers.
# Discover and run the repository static analysis and type verification script across all service boundary modules.
```

**Accept when:**
- All service boundary route handlers handle missing and malformed query parameters with fallback values or structured errors without uncaught exceptions.
- Project verification test suites and static type analysis execute with zero failures across all service boundary modules.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated continuous integration checks and peer code reviews enforce compliance.
</enforcement>