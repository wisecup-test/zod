# Adopt next/link for Client-Side Internal Navigation: Components Requiring Internal Route Navigation Document

These rules are ALWAYS ACTIVE for all internal navigation elements and section anchors within documentation and content routes, and interactive UI components that navigate between application views or routes.

### Rules

- **R-NAV-001** MUST: Components requiring internal route navigation or document anchor links MUST use the Link component provided by next/link rather than standard unmanaged hyperlink elements.

### Verify

```bash
# Discover and run project static analysis/linting scripts to verify compliance with internal link import rules
# Discover and execute automated test suites to validate route link rendering and target attributes
# Discover and run the project build script to ensure all linked routes resolve successfully
```

**Accept when:**
- All internal intra-site links render via the framework Link component without unmanaged anchor tags for local paths.
- Project static analysis and build verification scripts execute without navigation-related errors.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated static analysis and peer code review enforce compliance; pull requests containing unmanaged anchors for internal routes will be blocked.
</enforcement>