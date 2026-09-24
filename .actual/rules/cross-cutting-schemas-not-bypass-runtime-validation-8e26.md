# Valibot Modular Schema Validation Adoption: Schemas Not Bypass Runtime Validation When

These rules are ALWAYS ACTIVE for runtime input parsing, structured schema definition, and payload validation across application modules and performance-sensitive, bundle-constrained packages.

### Rules

- **R-VAL-001** MUST_NOT: Schemas MUST NOT bypass runtime validation when parsing untrusted external inputs across public API boundaries.

### Verify

```bash
# Discover the project test runner from the dependency manifest and execute the test suite
# Discover and run the project build script to confirm tree-shaking and bundle generation succeed
```

**Accept when:**
- All schema validation tests pass across packages importing the validation library.
- Production bundle analysis confirms that only imported validation primitives are included in target distribution artifacts.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>