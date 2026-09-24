# React 'use client' Directive for Client Component Rendering Boundaries: Interactive Client Component Boundaries Isolated Leaf

These rules are ALWAYS ACTIVE for all React component modules and UI files requiring browser runtime primitives, interactive state management, or client side effects within hybrid rendering architectures.

### Rules

- **R-CLIENT-001** SHOULD: Interactive client component boundaries SHOULD be isolated to leaf components to minimize client JavaScript bundle size and maximize server-rendered markup.
- **R-CLIENT-002** MANDATORY: Place the 'use client' directive as the initial statement of the component file, preceding all imports and declarations.
- **R-CLIENT-003** MANDATORY: Isolate client boundary declarations to focused leaf components to avoid converting surrounding server components into client components.
- **R-CLIENT-004** MANDATORY: Wrap third-party interactive libraries requiring browser execution within dedicated boundary components rather than elevating ancestor layouts.

### Verify

```bash
# Discover the project dependency manifest to locate the build script, then execute the build command to verify that all client component boundaries bundle without compilation errors.
# Discover the static analysis configuration and run the lint script to confirm compliance with client component directive constraints.
```

**Accept when:**
- The project build script succeeds with all client component boundaries properly recognized without bundling or compilation errors.
- Static analysis checks pass with zero violations regarding missing client directives on stateful components or unauthorized access to server-only resources.

<enforcement>
Claude Code MUST NOT skip or defer verification. Continuous integration builds fail upon detecting stateful hook usage in modules lacking the required boundary directive, and pull requests containing improper boundary placements or unauthorized resource access are blocked from merging.
</enforcement>