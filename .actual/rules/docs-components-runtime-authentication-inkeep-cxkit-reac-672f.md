# Adopt @inkeep/cxkit-react for Client-Side Documentation Search and Support: Runtime Authentication Inkeep Cxkit React Consume

These rules are ALWAYS ACTIVE for documentation user interface components implementing search dialogs, support bubbles, or interactive assistance widgets using @inkeep/cxkit-react.

### Rules

- **R-INKEEP-001** MUST: Runtime authentication for @inkeep/cxkit-react MUST consume configuration exclusively through process.env.NEXT_PUBLIC_INKEEP_KEY.

### Verify

```bash
# Discover and execute project verification and linting scripts from the repository manifest
# Example standard checks:
npm run build
npm run lint
```

**Accept when:**
- Client documentation components successfully render interactive search and assistance interfaces powered by @inkeep/cxkit-react.
- Static analysis confirms all @inkeep/cxkit-react consumer modules declare the client boundary directive and handle lifecycle effects within useEffect.
- Configuration verification confirms that only public client environment variables are exposed to the browser runtime.

<enforcement>
Claude Code MUST NOT skip or defer verification. All violations of client boundary directives, unverified secrets, or unapproved search components will fail continuous integration and build checks.
</enforcement>