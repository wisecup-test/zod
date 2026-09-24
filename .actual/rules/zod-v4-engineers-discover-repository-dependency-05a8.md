# Core Module Kernel Architecture for Layered Schema Engine Distributions: Engineers Discover Repository Dependency Manifest Lock

These rules are ALWAYS ACTIVE for all internal runtime modules, parsing utilities, schema registries, and distribution surface profiles involving schema validations and standard schema integrations across library distribution variants.

### Rules

- **R-CORE-001** MUST: Engineers MUST discover the repository dependency manifest and lock artifact to verify the exact resolved version of all external specification libraries before implementing core module integrations.
- **R-CORE-002** MUST: Structure internal core exports through a dedicated entry interface to establish a well-defined boundary for surface variants.
- **R-CORE-003** MUST: Ensure registry singletons instantiated in the core module maintain strict reference identity across dynamic imports and distribution boundaries.

### Verify

```bash
# Discover the project script runner and execute dependency boundary linting and test suites across variants
```

**Accept when:**
- The module boundary analysis confirms zero inward imports from the core module to outer distribution variants.
- All distribution test suites pass without registry conflicts or schema parsing discrepancies.

<enforcement>
Claude Code MUST NOT skip or defer verification. Compliance with architectural dependency boundaries and lock-version grounding is strictly enforced by automated CI static analysis and architectural linting.
</enforcement>