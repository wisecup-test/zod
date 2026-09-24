# Zod External Core Module Delegation: Variant Entry Points Export Core Definitions

These rules are ALWAYS ACTIVE for entry point modules exposing consumer-facing library surfaces across package variants and core module interface boundaries connecting external facades to internal definitions.

### Rules

- **R-ZOD-001** SHOULD: Variant entry points SHOULD re-export core definitions directly from the external module interface while applying only variant-specific configuration or subset filtering.

### Verify

```bash
# Discover and run the project static analysis suite to verify that all entry modules import shared definitions from the external core module.
# Discover and execute the package boundary and circular dependency verification scripts from repository manifests.
# Discover and run the integration test suite to validate API compatibility across all entry facade surfaces.
```

**Accept when:**
- All published entry surfaces successfully delegate core definitions to the external core module without local reimplementation.
- Static analysis and dependency boundary checks complete with zero unresolved imports or circular references.
- All unit and integration verification suites pass across all entry point variants.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>