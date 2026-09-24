# Adopt @inkeep/cxkit-react for Client-Side Documentation Search and Support: Interactive Search Documentation Assistance Components Use

These rules are ALWAYS ACTIVE for documentation user interface components implementing search dialogs, support bubbles, or interactive assistance widgets.

### Rules

- **R-DOC-001** MUST: Interactive search and documentation assistance components MUST use @inkeep/cxkit-react for client-side search and chat widgets.

### Verify

```bash
# Discover and run project verification and linting suite via repository manifest
# (e.g., npm run test, npm run lint, or equivalent package manager commands)
```

**Accept when:**
- Client documentation components successfully render interactive search and assistance interfaces powered by @inkeep/cxkit-react.
- Static analysis confirms all @inkeep/cxkit-react consumer modules declare the client boundary directive and handle lifecycle effects within useEffect.
- Configuration verification confirms that only public client environment variables are exposed to the browser runtime.

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated static analysis, peer code reviews, and dependency auditing script checks enforce these requirements.
</enforcement>