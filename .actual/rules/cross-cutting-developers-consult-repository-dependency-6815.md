# Adopt @rollup/plugin-typescript for Bundler TypeScript Compilation: Developers Consult Repository Dependency Manifest Lock

These rules are ALWAYS ACTIVE for build and bundle configurations compiling TypeScript source files across packages and shared modules.

### Rules

- **R-TS-001** MUST: Developers MUST consult the repository dependency manifest and lock artifact to resolve and verify the exact installed version of @rollup/plugin-typescript before modifying or extending bundling pipelines.

### Verify

```bash
# Discover and execute the repository build script from the project manifest
# Example: npm run build / yarn build / pnpm build
```

**Accept when:**
- The module bundling process compiles TypeScript sources without diagnostic errors or missing declaration artifacts.
- Emitted bundles preserve accurate module exports and pass all automated verification checks defined in the repository.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>