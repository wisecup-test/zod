# Adopt @rollup/plugin-typescript for Bundler TypeScript Compilation: Build Configurations Processing Typescript Modules Use

These rules are ALWAYS ACTIVE for build and bundle configurations compiling TypeScript source files across packages and shared modules.

### Rules

- **R-BLD-001** MUST: Build configurations processing TypeScript modules MUST use @rollup/plugin-typescript to execute source compilation and emit bundled module artifacts.

### Verify

```bash
# Discover the project configuration files to ensure the TypeScript plugin is ordered correctly with companion resolution and commonjs plugins in the pipeline array.
# Discover the repository build script from the project manifest and execute the bundle build target to verify clean TypeScript compilation.
# Discover the test verification script from the project manifest and execute the test suite to validate that emitted bundle artifacts pass all functional checks.
```

**Accept when:**
- The module bundling process compiles TypeScript sources without diagnostic errors or missing declaration artifacts.
- Emitted bundles preserve accurate module exports and pass all automated verification checks defined in the repository.

<enforcement>
Claude Code MUST NOT skip or defer verification. Continuous integration build checks and peer code review validate successful artifact bundling.
</enforcement>