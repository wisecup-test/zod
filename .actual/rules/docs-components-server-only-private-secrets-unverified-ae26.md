# Adopt @inkeep/cxkit-react for Client-Side Documentation Search and Support: Server Only Private Secrets Unverified Environment

These rules are ALWAYS ACTIVE for documentation user interface components implementing search dialogs, support bubbles, or interactive assistance widgets.

### Rules

- **R-INKEEP-001** MUST_NOT: Server-only private secrets or unverified environment variables MUST NOT be passed to @inkeep/cxkit-react client components.

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
Claude Code MUST NOT skip or defer verification. Verified by automated static analysis, linting checks, and peer code reviews.
</enforcement>