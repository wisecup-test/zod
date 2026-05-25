# Standardize Schema Definition Patterns for Service API Boundaries: Service Boundaries Define

These rules are ALWAYS ACTIVE for all service API boundaries, including REST API endpoints, GraphQL resolvers, message queue consumers, RPC service methods, database model validation layers, and inter-service communication boundaries.

### Rules

- **R-SVC-BND-001** MUST: All service API boundaries MUST define explicit schemas using a declarative schema validation library (e.g., Zod, JSON Schema).

### Verify

```bash
# Check for schema definitions in service boundary files
grep -r "z\.object\|z\.string\|z\.number" --include="*.ts" --include="*.js" packages/*/src/**/schemas.ts packages/*/src/**/api

# Find schema validation tests
find . -name "*.test.ts" -path "*/tests/*" -exec grep -l "schema\|validation\|zod" {} \;

# Run schema validation tests with coverage threshold
npm test -- --testPathPattern="schema|validation" --coverage --coverageThreshold='{"global":{"branches":80}}'
```

**Accept when:**
- All service API boundary files contain explicit schema definitions using the standardized validation library
- Schema validation tests exist with at least 80% branch coverage for schema definitions
- CI pipeline includes automated checks that fail when service boundaries lack schema validation

<enforcement>
Claude Code MUST NOT skip or defer verification. All service API boundaries require explicit schema definitions before code review approval.
</enforcement>