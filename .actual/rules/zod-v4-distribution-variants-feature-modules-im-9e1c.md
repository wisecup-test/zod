# Core Module Kernel Architecture for Layered Schema Engine Distributions: Distribution Variants Feature Modules Import Shared

These rules are ALWAYS ACTIVE for all internal runtime modules, parsing utilities, schema registries, distribution surface profiles, transformations, validations, and standard schema integrations across library distribution variants.

### Rules

- **R-DIST-001** MUST: All distribution variants and feature modules MUST import shared schema validation primitives, execution utilities, and registry instances exclusively from the centralized core module.

### Verify

```bash
# Discover project script runner and run module dependency boundary linting suite
# Discover and run project type-checking and unit test suites across all distribution variants
```

**Accept when:**
- The module boundary analysis confirms zero inward imports from the core module to outer distribution variants.
- All distribution test suites pass without registry conflicts or schema parsing discrepancies.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory.
</enforcement>