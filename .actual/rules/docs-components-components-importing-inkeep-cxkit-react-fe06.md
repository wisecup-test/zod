# Adopt @inkeep/cxkit-react for Client-Side Documentation Search and Support: Components Importing Inkeep Cxkit React Declare

These rules are ALWAYS ACTIVE for documentation user interface components implementing search dialogs, support bubbles, or interactive assistance widgets importing @inkeep/cxkit-react.

### Rules

- **R-INTR-001** MUST: All components importing @inkeep/cxkit-react MUST declare the use client directive at the top of the module boundary.

### Verify

```bash
# Discover and execute project verification and linting scripts from the repository manifest
```

**Accept when:**
- Client documentation components successfully render interactive search and assistance interfaces powered by @inkeep/cxkit-react.
- Static analysis confirms all @inkeep/cxkit-react consumer modules declare the client boundary directive and handle lifecycle effects within useEffect.
- Configuration verification confirms that only public client environment variables are exposed to the browser runtime.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>