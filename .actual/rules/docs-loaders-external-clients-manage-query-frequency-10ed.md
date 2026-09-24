# Internal Fetch Client with In-Memory Cache and Bearer Authentication: External Clients Manage Query Frequency Response

These rules are ALWAYS ACTIVE for internal data loader routines querying remote HTTP service endpoints and modules managing cached external API integration data.

### Rules

- **R-EXT-001** SHOULD: External API clients manage query frequency and response durability by maintaining explicit cache layers and timed revalidation policies.
- **R-EXT-002** MANDATORY: External client endpoints define explicit cache revalidation intervals matching route staleness requirements.
- **R-EXT-003** MANDATORY: Environment variable lookups for external authentication tokens are validated prior to initiating outbound HTTP requests.

### Verify

```bash
# Discover and run the repository test runner from the root manifest covering data loader modules
# Discover and run static analysis scripts from configuration artifacts across external client integrations
```

**Accept when:**
- Data loader modules retrieve external records and verify cached responses before initiating outbound network requests.
- Static analysis and test suites pass without reporting unhandled credential references or unvalidated external network calls.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>