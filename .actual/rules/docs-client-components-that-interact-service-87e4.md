# next/server Service Boundary Parameter Extraction: Client Components That Interact Service Endpoint

These rules are ALWAYS ACTIVE for all HTTP route handlers, API endpoints providing service boundaries, and client components reading or reflecting URL query parameters at navigation boundaries.

### Rules

- **R-NXT-001** SHOULD: Client components that interact with service endpoint query parameters align parameter key naming conventions with corresponding server boundary definitions.

### Verify

```bash
# Discover and execute the project test execution script from the workspace dependency manifest covering service route handlers
# Discover and run the repository static analysis and type verification script across all service boundary modules
```

**Accept when:**
- All service boundary route handlers handle missing and malformed query parameters with fallback values or structured errors without uncaught exceptions.
- Project verification test suites and static type analysis execute with zero failures across all service boundary modules.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verified by automated CI checks, test suites, static analysis verification scripts, and mandatory peer code review.
</enforcement>