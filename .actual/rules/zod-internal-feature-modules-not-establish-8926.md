# Zod External Core Module Delegation: Internal Feature Modules Not Establish Direct

These rules are ALWAYS ACTIVE for all code affecting entry point facades, internal feature modules, and external core module delegation boundaries within the Zod package variants.

### Rules

- **R-ZOD-001** SHOULD_NOT: Internal feature modules SHOULD_NOT establish direct circular dependencies back to entry point facades that re-export the external module.

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