# Adopt @rollup/plugin-typescript for Bundler TypeScript Compilation: Configurations Invoking Rollup Plugin Typescript Position

These rules are ALWAYS ACTIVE for build and bundle configurations compiling TypeScript source files across packages and shared modules.

### Rules

- **R-TS-001** MUST: Configurations invoking @rollup/plugin-typescript MUST position the plugin appropriately relative to module resolution plugins to ensure TypeScript source files are resolved before transpilation.

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