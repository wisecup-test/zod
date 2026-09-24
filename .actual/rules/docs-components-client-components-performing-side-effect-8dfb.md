# React Client Component Interaction Management via useState and useEffect Hooks: Client Components Performing Side Effects Asynchronous

These rules are ALWAYS ACTIVE for frontend UI components requiring user interaction, transient local state, or browser lifecycle events.

### Rules

- **R-CLIENT-001** MUST: Client components performing side effects, asynchronous browser operations, or event listener subscriptions MUST encapsulate them within the useEffect hook with explicit dependency arrays.

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
Claude Code MUST NOT skip or defer verification. Verification is mandatory.
</enforcement>