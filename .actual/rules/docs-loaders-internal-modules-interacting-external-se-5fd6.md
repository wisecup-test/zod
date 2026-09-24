# Internal Fetch Client with In-Memory Cache and Bearer Authentication: Internal Modules Interacting External Services Encapsulate

These rules are ALWAYS ACTIVE for internal data loader routines querying remote HTTP service endpoints and modules managing cached external API integration data.

### Rules

- **R-EXT-001** MUST: Internal modules interacting with external services MUST encapsulate HTTP requests within dedicated client boundary functions rather than executing ad-hoc network queries.
- **R-EXT-002** MUST: All external client endpoints define explicit cache revalidation intervals matching route staleness requirements.
- **R-EXT-003** MUST: Ensure environment variable lookups for external authentication tokens are validated prior to initiating outbound HTTP requests.

### Verify

```bash
# Discover the repository test runner from the root manifest and execute the test suite covering data loader modules.
# Discover the repository static analysis script from configuration artifacts and run lint checks across external client integrations.
```

**Accept when:**
- Data loader modules retrieve external records and verify cached responses before initiating outbound network requests.
- Static analysis and test suites pass without reporting unhandled credential references or unvalidated external network calls.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>