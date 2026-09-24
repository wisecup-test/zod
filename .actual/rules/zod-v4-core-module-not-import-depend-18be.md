# Core Module Kernel Architecture for Layered Schema Engine Distributions: Core Module Not Import Depend Upon

These rules are ALWAYS ACTIVE for all internal runtime modules, parsing utilities, schema registries, and distribution surface profiles.

### Rules

- **R-CORE-001** MUST_NOT: The core module MUST NOT import from or depend upon outer distribution variants or specialized interface surfaces.

### Verify

```bash
# Discover the project script runner and execute the module dependency boundary linting suite to verify that no circular dependencies or reverse imports exist from core to distribution surfaces.
# Discover and run the project type-checking and unit test suites across all distribution variants to confirm uniform behavior against core schema utilities.
```

**Accept when:**
- The module boundary analysis confirms zero inward imports from the core module to outer distribution variants.
- All distribution test suites pass without registry conflicts or schema parsing discrepancies.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>