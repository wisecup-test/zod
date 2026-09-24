# Zod External Core Module Delegation: Zod Package Entry Points Route Their

These rules are ALWAYS ACTIVE for all Zod package entry points and core module boundaries.

### Rules

- **R-ZOD-001** MUST: All Zod package entry points MUST route their core public API definitions and runtime constructs through the centralized external core module rather than maintaining independent core implementations.

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