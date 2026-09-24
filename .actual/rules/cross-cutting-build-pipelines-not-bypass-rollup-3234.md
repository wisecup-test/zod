# Adopt @rollup/plugin-typescript for Bundler TypeScript Compilation: Build Pipelines Not Bypass Rollup Plugin

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-TS-001** MUST_NOT: Build pipelines MUST_NOT bypass @rollup/plugin-typescript with uncoordinated secondary transpilers or ad-hoc compile scripts for packages governed by this standard.

### Verify

```bash
# Discover the repository build script from the project manifest and execute the bundle build target to verify clean TypeScript compilation.
# Discover the test verification script from the project manifest and execute the test suite to validate that emitted bundle artifacts pass all functional checks.
```

**Accept when:**
- The module bundling process compiles TypeScript sources without diagnostic errors or missing declaration artifacts.
- Emitted bundles preserve accurate module exports and pass all automated verification checks defined in the repository.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>