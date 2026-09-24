# Core Module Kernel Architecture for Layered Schema Engine Distributions: Global State Schema Registries Instantiated Managed

These rules are ALWAYS ACTIVE for internal runtime modules, parsing utilities, schema registries, and distribution surface profiles involving transformations, validations, and standard schema integrations across library distribution variants.

### Rules

- **R-CORE-001** MUST: Global state and schema registries MUST be instantiated and managed within the core module, exposing access solely through core registry interfaces rather than distribution-local registries.

### Verify

```bash
# Discover the project script runner and execute the module dependency boundary linting suite to verify that no circular dependencies or reverse imports exist from core to distribution surfaces.
# Discover and run the project type-checking and unit test suites across all distribution variants to confirm uniform behavior against core schema utilities.
```

**Accept when:**
- The module boundary analysis confirms zero inward imports from the core module to outer distribution variants.
- All distribution test suites pass without registry conflicts or schema parsing discrepancies.

<enforcement>
Claude Code MUST NOT skip or defer verification. Continuous integration static analysis checks enforcing architectural import boundaries and automated test suites validating behavior across all distribution profiles against the core module are mandatory.
</enforcement>