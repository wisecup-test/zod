# Adopt next/link for Client-Side Internal Navigation: Consumers Inspect Repository Dependency Resolution Artifact

These rules are ALWAYS ACTIVE for all internal navigation elements, section anchors, documentation, content routes, and interactive UI components within the application.

### Rules

- **R-NAV-001** MUST: Consumers MUST inspect the repository dependency resolution artifact to determine the exact locked version of the routing dependency before implementing navigation features.

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