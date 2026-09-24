# React Client Component Interaction Management via useState and useEffect Hooks: Consumers Verify Project Dependency Lock Artifact

These rules are ALWAYS ACTIVE for frontend UI components requiring user interaction, transient local state, or browser lifecycle events.

### Rules

- **R-REACT-001** MUST: Consumers MUST verify the project dependency lock artifact to determine the exact resolved version of React before implementing client interaction hooks.
- **R-REACT-002** MUST: Always return an explicit cleanup function from useEffect when subscribing to browser events, intervals, or asynchronous streams.
- **R-REACT-003** SHOULD: Encapsulate complex multi-step interaction logic or paired useState and useEffect routines into custom hooks to preserve component readability.

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
Claude Code MUST NOT skip or defer verification. Continuous integration pipelines and automated static analysis rules enforce these verification steps.
</enforcement>