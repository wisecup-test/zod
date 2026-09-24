# Internal Fetch Client with In-Memory Cache and Bearer Authentication: Client Error Handling Routines Report External

These rules are ALWAYS ACTIVE for internal data loader routines querying remote HTTP service endpoints and modules managing cached external API integration data.

### Rules

- **R-EXT-001** MUST: Client error handling routines MUST report external API failure events to standard error channels without leaking secret credentials or runtime environment details.

### Verify

```bash
# Discover the repository test runner from the root manifest and execute the test suite covering data loader modules.
# Discover the repository static analysis script from configuration artifacts and run lint checks across external client integrations.
```

**Accept when:**
- Data loader modules retrieve external records and verify cached responses before initiating outbound network requests.
- Static analysis and test suites pass without reporting unhandled credential references or unvalidated external network calls.

<enforcement>
Claude Code MUST NOT skip or defer verification. Continuous integration jobs fail when unhandled external network calls or missing environment checks are detected.
</enforcement>