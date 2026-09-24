# Adopt next/link for Client-Side Internal Navigation: Navigation Links Combined Transition Hover Styling

These rules are ALWAYS ACTIVE for all internal navigation elements and section anchors within documentation and content routes, and interactive UI components that navigate between application views or routes.

### Rules

- **R-NAV-001** MAY: Navigation links MAY be combined with transition or hover styling classes to indicate interactive state.

### Verify

```bash
# Discover and run project static analysis, linting, test suites, and build scripts
# Example typical workflow commands:
npm run lint
npm run test
npm run build
```

**Accept when:**
- All internal intra-site links render via the framework Link component without unmanaged anchor tags for local paths.
- Project static analysis and build verification scripts execute without navigation-related errors.

<enforcement>
Claude Code MUST NOT skip or defer verification. Verification is mandatory via automated static analysis checks, peer code review, and CI pipelines.
</enforcement>