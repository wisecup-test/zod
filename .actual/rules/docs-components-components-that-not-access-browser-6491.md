# React 'use client' Directive for Client Component Rendering Boundaries: Components That Not Access Browser Runtime

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-REACT-001** MUST_NOT: Components that do not access browser runtime APIs, state hooks such as useState, or effect hooks such as useEffect MUST NOT declare the 'use client' directive.

### Verify

```bash
# Discover the project dependency manifest to locate the build script, then execute the build command to verify client component boundaries.
# (Example: pnpm build / npm run build)
# Discover the static analysis configuration and run the lint script to confirm compliance.
# (Example: pnpm lint / npm run lint)
```

**Accept when:**
- The project build script succeeds with all client component boundaries properly recognized without bundling or compilation errors.
- Static analysis checks pass with zero violations regarding missing client directives on stateful components or unauthorized access to server-only resources.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated continuous integration build checks, static analysis linting rules, and peer code reviews verify client component bundling, compilation, and boundary placement.
</enforcement>