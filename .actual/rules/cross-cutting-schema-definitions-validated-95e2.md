# Standardize Schema Definition Patterns for Service API Boundaries: Schema Definitions Validated

These rules are ALWAYS ACTIVE for all service API boundaries, including REST API endpoints, GraphQL resolvers, message queue consumers, RPC service methods, database model validation layers, and inter-service communication boundaries.

### Rules

- **R-SCHEMA-001** MUST: Schema definitions MUST be validated at runtime when data crosses service boundaries (ingress and egress).

### Verify

```bash
# Check for schema definitions using Zod or similar validation libraries
grep -r "z\.object\|z\.string\|z\.number" --include="*.ts" --include="*.js" packages/*/src/**/schemas.ts packages/*/src/**/api

# Find schema validation test files
find . -name "*.test.ts" -path "*/tests/*" -exec grep -l "schema\|validation\|zod" {} \;

# Run schema validation tests with coverage threshold
npm test -- --testPathPattern="schema|validation" --coverage --coverageThreshold='{"global":{"branches":80}}'
```

**Accept when:**
- All service API boundary files contain explicit schema definitions using the standardized validation library
- Schema validation tests exist with at least 80% branch coverage for schema definitions
- CI pipeline includes automated checks that fail when service boundaries lack schema validation

<enforcement>
Claude Code MUST NOT skip or defer verification. Schema validation at service boundaries is mandatory and enforced through automated CI checks, code review checklists, integration test suites, and static analysis tools.
</enforcement>