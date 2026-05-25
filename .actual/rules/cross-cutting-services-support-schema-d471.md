# Standardize Schema Definition Patterns for Service API Boundaries: Services Support Schema

These rules are ALWAYS ACTIVE for all REST API endpoints, GraphQL resolvers, message queue consumers, RPC service methods, database model validation layers, and inter-service communication boundaries.

### Rules

- **R-SCHEMA-001** SHOULD: Services SHOULD support schema interoperability formats (e.g., JSON Schema conversion) for cross-platform compatibility.

### Verify

```bash
# Scan for schema definitions using standardized validation library
grep -r "z\.object\|z\.string\|z\.number" --include="*.ts" --include="*.js" packages/*/src/**/schemas.ts packages/*/src/**/api

# Find schema validation test files
find . -name "*.test.ts" -path "*/tests/*" -exec grep -l "schema\|validation\|zod" {} \;

# Run schema validation tests with coverage threshold
npm test -- --testPathPattern="schema|validation" --coverage --coverageThreshold='{"global":{"branches":80}}'
```

**Accept when:**
- All service API boundary files contain explicit schema definitions using the standardized validation library (Zod)
- Schema validation tests exist with at least 80% branch coverage for schema definitions
- CI pipeline includes automated checks that fail when service boundaries lack schema validation
- Schema definitions are kept in sync with actual service behavior as verified by integration tests

<enforcement>
Claude Code MUST NOT skip or defer verification. All new service boundaries require schema validation or documented exception approval before merge.
</enforcement>