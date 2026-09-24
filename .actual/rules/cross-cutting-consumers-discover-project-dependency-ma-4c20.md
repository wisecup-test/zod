# Valibot Modular Schema Validation Adoption: Consumers Discover Project Dependency Manifest Lock

These rules are ALWAYS ACTIVE for runtime input parsing, structured schema definition, and payload validation across application modules.

### Rules

- **R-VAL-001** MUST: Consumers MUST discover the project dependency manifest and lock artifact to determine the authoritative installed version of the validation library prior to implementing or consuming schema primitives.

### Verify

```bash
# Discover the project test runner from the dependency manifest and execute the test suite to verify schema validation compliance.
# Discover and run the project build script to confirm that tree-shaking and bundle generation succeed without unresolved validation imports.
```

**Accept when:**
- All schema validation tests pass across packages importing the validation library.
- Production bundle analysis confirms that only imported validation primitives are included in target distribution artifacts.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>