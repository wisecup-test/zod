# next/navigation Adoption for Application Routing and Parameter State: Before Implementing Updating Navigation Logic Developers

These rules are ALWAYS ACTIVE for all application modules, route pages, and interactive UI components that read query parameters or initiate route transitions.

### Rules

- **R-NAV-001** MUST: Before implementing or updating navigation logic, developers MUST inspect the workspace dependency manifest and package lock artifact to identify and verify the exact resolved version of the routing dependency against official documentation.

### Verify

```bash
# Inspect the project dependency manifest and lock artifact to verify that the routing module is registered as a required dependency.
# Execute repository linting and static analysis scripts to confirm no forbidden window location or history references exist in UI modules.
# Run the project automated test suite to ensure that route transitions and parameter retrieval behave as expected without runtime warnings.
```

**Accept when:**
- All routing and parameter interactions import exclusively from next/navigation.
- No direct window location or browser history manipulations exist within application components.
- Static analysis and automated component validation suites pass without routing-related errors.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>