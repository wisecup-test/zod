# next/server Service Boundary Parameter Extraction: Service Boundary Definitions Centralize Expected Query

These rules are ALWAYS ACTIVE for HTTP route handlers, API endpoints, and client-facing interfaces processing incoming requests and reading or reflecting URL query parameters at service boundaries.

### Rules

- **R-SB-001** SHOULD: Service boundary definitions SHOULD centralize expected query parameter keys as named constants to maintain predictable interface contracts across routes.

### Verify

```bash
# Discover the project test execution script from the workspace dependency manifest and execute the test suite covering service route handlers.
# Discover the repository static analysis and type verification script and run it across all service boundary modules to confirm type conformance.
```

**Accept when:**
- All service boundary route handlers handle missing and malformed query parameters with fallback values or structured errors without uncaught exceptions.
- Project verification test suites and static type analysis execute with zero failures across all service boundary modules.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated continuous integration checks executing test suites and static analysis verification scripts, and mandatory peer code review.
</enforcement>