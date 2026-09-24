# React Client Component Interaction Management via useState and useEffect Hooks: Client Components Managing Transient Interaction State

These rules are ALWAYS ACTIVE for frontend UI components requiring user interaction, transient local state, or browser lifecycle events.

### Rules

- **R-REACT-001** MUST: Client components managing transient interaction state MUST utilize the useState hook rather than external mutable variables or imperative DOM properties.

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
Claude Code MUST NOT skip or defer verification. Verification by automated static analysis rules, component test suites, and peer code review is mandatory.
</enforcement>