# Adopt @inkeep/cxkit-react for Client-Side Documentation Search and Support: Client Side Initialization Interactive Lifecycle Handling

These rules are ALWAYS ACTIVE for documentation user interface components implementing search dialogs, support bubbles, or interactive assistance widgets.

### Rules

- **R-INKEEP-001** MUST: Client-side initialization and interactive lifecycle handling for @inkeep/cxkit-react integrations MUST be coordinated within useEffect hooks.

### Verify

```bash
# Discover and execute project verification and linting scripts from the repository manifest
# to validate compilation, static type checking, and proper client directive placement/hook lifecycle dependencies.
```

**Accept when:**
- Client documentation components successfully render interactive search and assistance interfaces powered by @inkeep/cxkit-react.
- Static analysis confirms all @inkeep/cxkit-react consumer modules declare the client boundary directive and handle lifecycle effects within useEffect.
- Configuration verification confirms that only public client environment variables are exposed to the browser runtime.

<enforcement>
Claude Code MUST NOT skip or defer verification. All pull requests introducing documentation UI components are verified by automated static analysis, linting checks, and peer code reviews.
</enforcement>