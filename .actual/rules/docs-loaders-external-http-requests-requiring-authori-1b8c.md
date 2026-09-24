# Internal Fetch Client with In-Memory Cache and Bearer Authentication: External Http Requests Requiring Authorization Inject

These rules are ALWAYS ACTIVE for internal data loader routines querying remote HTTP service endpoints and modules managing cached external API integration data.

### Rules

- **R-EXT-001** MUST: External HTTP requests requiring authorization MUST inject credentials from environment configuration via standard bearer authentication headers.

### Verify

```bash
# Discover and execute repository test runner covering data loader modules
# Discover and run static analysis/lint checks across external client integrations
```

**Accept when:**
- Data loader modules retrieve external records and verify cached responses before initiating outbound network requests.
- Static analysis and test suites pass without reporting unhandled credential references or unvalidated external network calls.

<enforcement>
Claude Code MUST NOT skip or defer verification.
</enforcement>