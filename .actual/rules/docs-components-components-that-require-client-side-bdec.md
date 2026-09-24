# React 'use client' Directive for Client Component Rendering Boundaries: Components That Require Client Side State

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-CLIENT-001** MUST: Components that require client-side state hooks, lifecycle side effects, browser event listeners, or client navigation parameters MUST declare the 'use client' directive at the top of the module to define a client component boundary.

### Verify

```bash
# Discover the project dependency manifest to locate the build script, then execute the build command
# Discover the static analysis configuration and run the lint script
```

**Accept when:**
- The project build script succeeds with all client component boundaries properly recognized without bundling or compilation errors.
- Static analysis checks pass with zero violations regarding missing client directives on stateful components or unauthorized access to server-only resources.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>