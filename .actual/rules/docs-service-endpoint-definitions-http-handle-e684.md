# next/server Service Boundary Parameter Extraction: Service Endpoint Definitions Http Handlers Standardize

These rules are ALWAYS ACTIVE for all HTTP route handlers, API endpoints providing service boundaries, and client components reading or reflecting URL query parameters at navigation boundaries.

### Rules

- **R-ADR-001** MUST: Service endpoint definitions in HTTP handlers MUST standardize query parameter ingestion through next/server boundary interfaces using searchParams.get extraction.

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