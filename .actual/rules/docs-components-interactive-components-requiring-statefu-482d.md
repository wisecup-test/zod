# React Client Component Interaction Management via useState and useEffect Hooks: Interactive Components Requiring Stateful Interactions Lifecycle

These rules are ALWAYS ACTIVE for frontend UI components requiring user interaction, transient local state, or browser lifecycle events.

### Rules

- **R-STATE-001** MUST: Interactive UI components requiring stateful interactions or lifecycle side effects MUST declare the client rendering boundary and use React hooks exclusively for state and side-effect management.
- **R-STATE-002** MUST: Always return an explicit cleanup function from useEffect when subscribing to browser events, intervals, or asynchronous streams.
- **R-STATE-003** SHOULD: Encapsulate complex multi-step interaction logic or paired useState and useEffect routines into custom hooks to preserve component readability.
- **R-STATE-004** MUST: Execute lock-version grounding before writing code that uses a versioned library: find manifest, identify build tool, inspect repository lock or resolution artifact for exact resolved version, look up official documentation for that exact version, confirm every API/class/function exists in that version's documentation, and re-run per dependency at point of use for version-sensitive behavior.

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
Claude Code MUST NOT skip or defer verification. Verified by continuous integration pipelines and peer code review.
</enforcement>