# Adopt next/link for Client-Side Internal Navigation: Internal Navigation Elements Supply Static Dynamic

These rules are ALWAYS ACTIVE for all internal navigation elements, section anchors within documentation and content routes, and interactive UI components that navigate between application views or routes.

### Rules

- **R-NAV-001** SHOULD: Internal navigation elements supply static or dynamic destination paths to the href attribute of the Link component to enable background route prefetching.

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
Claude Code MUST NOT skip or defer verification. Automated static analysis checks and peer code reviews verify compliance, and violations will block pull requests or halt continuous integration workflows.
</enforcement>