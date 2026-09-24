# React 'use client' Directive for Client Component Rendering Boundaries: Before Implementing Updating Components Client Component

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-REACT-001** MUST: Before implementing or updating components using the client component rendering model, developers MUST discover the project dependency manifest and lock artifact to inspect and verify the exact resolved version of the rendering framework and UI libraries.
- **R-REACT-002** MUST: Place the 'use client' directive as the initial statement of the component file, preceding all imports and declarations.
- **R-REACT-003** MUST: Isolate client boundary declarations to focused leaf components to avoid converting surrounding server components into client components.
- **R-REACT-004** MUST: Wrap third-party interactive libraries requiring browser execution within dedicated boundary components rather than elevating ancestor layouts.

### Verify

```bash
# Discover the project dependency manifest to locate the build script, then execute the build command to verify that all client component boundaries bundle without compilation errors.
# Discover the static analysis configuration and run the lint script to confirm compliance with client component directive constraints.
```

**Accept when:**
- The project build script succeeds with all client component boundaries properly recognized without bundling or compilation errors.
- Static analysis checks pass with zero violations regarding missing client directives on stateful components or unauthorized access to server-only resources.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>