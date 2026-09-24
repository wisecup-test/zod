# React 'use client' Directive for Client Component Rendering Boundaries: Client Components That Interact Runtime Environment

These rules are ALWAYS ACTIVE for all interactive UI components, components wrapping third-party interactive client libraries, and client components interacting with runtime environment configuration.

### Rules

- **R-CC-001** SHOULD: Client components that interact with runtime environment configuration SHOULD access only public client-exposed variables and MUST NOT access server-only secrets.

### Verify

```bash
# Discover the project dependency manifest to locate the build script, then execute the build command
# (e.g., npm run build, yarn build, pnpm build)
npm run build

# Discover the static analysis configuration and run the lint script (e.g., npm run lint)
npm run lint
```

**Accept when:**
- The project build script succeeds with all client component boundaries properly recognized without bundling or compilation errors.
- Static analysis checks pass with zero violations regarding missing client directives on stateful components or unauthorized access to server-only resources.

<enforcement>
Claude Code MUST NOT skip or defer verification. All client component boundary directives, hook usages, and runtime environment variable access must be verified through automated build and static analysis checks.
</enforcement>