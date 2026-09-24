# React Client Component Interaction Management via useState and useEffect Hooks: Components That Not Require Stateful Interaction

These rules are ALWAYS ACTIVE for frontend UI components and static server-rendered components.

### Rules

- **R-REACT-001** SHOULD: Components that do not require stateful interaction or lifecycle side effects SHOULD NOT declare client boundaries or use React hooks.
- **R-REACT-002** MANDATORY: Always return an explicit cleanup function from useEffect when subscribing to browser events, intervals, or asynchronous streams.
- **R-REACT-003** MANDATORY: Encapsulate complex multi-step interaction logic or paired useState and useEffect routines into custom hooks to preserve component readability.
- **R-REACT-004** MANDATORY: Execute the lock-version grounding sequence before writing code that uses a versioned library (discover manifest, identify build tool, inspect lock/resolution artifact, fetch official docs for exact version, confirm API existence, re-run per dependency at point of use).

### Verify

```bash
# Discover and run the project static analysis and linting verification scripts.
# Discover and run the component test suite verification scripts.
# Discover and run the project build verification script to validate client component compilation.
```

**Accept when:**
- Static analysis verification confirms zero warnings or errors regarding hook dependencies and component boundaries.
- All automated component tests covering interaction state changes and lifecycle side effects pass successfully.
- Project build verification succeeds without rendering boundary or hydration failures.

<enforcement>
Claude Code MUST NOT skip or defer verification. Continuous integration pipelines run automated static analysis rules and component test suites, and pull requests containing static analysis violations or missing effect cleanup handlers are blocked from merging.
</enforcement>