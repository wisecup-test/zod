# Adopt next/link for Client-Side Internal Navigation: Components Not Use Unmanaged Anchor Elements

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-NAV-001** MUST_NOT: Components MUST NOT use unmanaged anchor elements for local intra-application paths.

### Verify

```bash
# Discover and run the project static analysis and linting scripts to verify compliance with internal link import rules.
# Discover and execute automated test suites to validate route link rendering and target attributes.
# Discover and run the project build script to ensure all linked routes resolve successfully.
```

**Accept when:**
- All internal intra-site links render via the framework Link component without unmanaged anchor tags for local paths.
- Project static analysis and build verification scripts execute without navigation-related errors.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>