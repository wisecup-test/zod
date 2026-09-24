# Adopt @inkeep/cxkit-react for Client-Side Documentation Search and Support: Developers Inspect Repository Lock Artifact Verify

These rules are ALWAYS ACTIVE for documentation user interface components implementing search dialogs, support bubbles, or interactive assistance widgets.

### Rules

- **R-INTR-001** MUST: Developers MUST inspect the repository lock artifact to verify the exact resolved version of @inkeep/cxkit-react and validate API compatibility against official documentation before implementation.

### Verify

```bash
# Discover the project verification script from the repository manifest and execute it to validate compilation and static type checking across documentation components.
# Discover and execute the repository linting suite to ensure proper client directive placement and hook lifecycle dependencies.
```

**Accept when:**
- Client documentation components successfully render interactive search and assistance interfaces powered by @inkeep/cxkit-react.
- Static analysis confirms all @inkeep/cxkit-react consumer modules declare the client boundary directive and handle lifecycle effects within useEffect.
- Configuration verification confirms that only public client environment variables are exposed to the browser runtime.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated static analysis, linting, and dependency audits are mandatory in continuous integration pipelines.
</enforcement>