# json-schema-processors Internal Module Adoption for Schema Transformation: When Extracting Default Values Schema Definitions

These rules are ALWAYS ACTIVE for internal modules implementing schema-to-schema transformation within the core library, specifically processors and generators handling schema serialization and validation keyword mapping when extracting default values from schema definitions.

### Rules

- **R-JSON-001** MUST: When extracting default values from schema definitions, processors MUST create an isolated deep clone using serialization round-tripping before attaching default values to generated schema structures.

### Verify

```bash
# Discover and execute the project test runner script for core schema transformation
# Inspect the build configuration and run type-checking and linting verification tasks
npm test
npm run lint
npm run typecheck
```

**Accept when:**
- All unit tests covering schema transformation processors and generator pipelines execute successfully without regression.
- Cyclic schema references resolve to valid references without triggering call stack exceptions.
- Static type analysis and module linting checks pass with zero reported errors.

<enforcement>
Claude Code MUST NOT skip or defer verification. All changes affecting core schema transformation modules must be verified via automated tests and static analysis, and are subject to mandatory peer code review.
</enforcement>