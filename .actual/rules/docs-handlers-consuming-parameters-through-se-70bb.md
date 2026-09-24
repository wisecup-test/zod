# next/server Service Boundary Parameter Extraction: Handlers Consuming Parameters Through Searchparams Get

These rules are ALWAYS ACTIVE for all HTTP route handlers, API endpoints, and client components reading or reflecting URL query parameters at navigation boundaries.

### Rules

- **R-ADR-001** MUST: Handlers consuming parameters through searchParams.get MUST explicitly account for null or missing return values by supplying fallback defaults or returning structured error responses at the service boundary.

### Verify

```bash
# Discover the project test execution script from the workspace dependency manifest and execute the test suite covering service route handlers.
# Discover the repository static analysis and type verification script and run it across all service boundary modules to confirm type conformance.
```

**Accept when:**
- All service boundary route handlers handle missing and malformed query parameters with fallback values or structured errors without uncaught exceptions.
- Project verification test suites and static type analysis execute with zero failures across all service boundary modules.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated continuous integration checks and mandatory peer code review.
</enforcement>