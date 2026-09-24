# Zod External Core Module Delegation: Entry Points Expose Convenience Aliases Targeted

These rules are ALWAYS ACTIVE for all entry point modules, variant entry facades, and external core module boundaries.

### Rules

- **R-ZOD-001** MAY: Entry points MAY expose convenience aliases or targeted subsets of core exports to optimize bundle footprint for specialized consumer constraints.

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
Claude Code MUST NOT skip or defer verification. Automated continuous integration pipeline failures block merges for direct reimplementations of core functions in entry facades, and mandatory architectural review is required for any bypasses.
</enforcement>