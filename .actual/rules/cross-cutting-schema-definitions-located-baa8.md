# Standardize Schema Definition Patterns for Service API Boundaries: Schema Definitions Located

These rules are ALWAYS ACTIVE for all REST API endpoints, GraphQL resolvers, message queue consumers, RPC service methods, database model validation layers, and inter-service communication boundaries.

### Rules

- **R-SCHEMA-001** SHOULD: Schema definitions SHOULD be co-located with service interface definitions to maintain cohesion.

### Verify

```bash
# Find schema definitions using Zod patterns
grep -r "z\.object\|z\.string\|z\.number" --include="*.ts" --include="*.js" packages/*/src/**/schemas.ts packages/*/src/**/api

# Find schema validation tests
find . -name "*.test.ts" -path "*/tests/*" -exec grep -l "schema\|validation\|zod" {} \;

# Run schema validation tests with coverage threshold
npm test -- --testPathPattern="schema|validation" --coverage --coverageThreshold='{"global":{"branches":80}}'
```

**Accept when:**
- All service API boundary files contain explicit schema definitions using the standardized validation library (Zod)
- Schema validation tests exist with at least 80% branch coverage for schema definitions
- CI pipeline includes automated checks that fail when service boundaries lack schema validation

<enforcement>
Claude Code MUST NOT skip or defer verification. Schema validation at service boundaries is mandatory for all in-scope API interfaces. Exceptions require explicit approval via the documented exception process (EXC-001 for performance-critical paths, EXC-002 for legacy service migration).
</enforcement>