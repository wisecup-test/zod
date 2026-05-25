# Adopt Environment Variables for Runtime Configuration Sources: Runtime Configuration Values

These rules are ALWAYS ACTIVE for all runtime configuration that varies by deployment environment, including API keys, authentication tokens, service credentials, external service endpoints, URLs, feature flags, and behavioral toggles across all TypeScript, JavaScript, and build script files.

### Rules

- **R-ENV-001** MUST: Runtime configuration values that vary by environment MUST be sourced from environment variables using `process.env`.
- **R-ENV-002** MUST: All runtime configuration that varies by deployment environment (development, staging, production) MUST NOT be hardcoded in source files.
- **R-ENV-003** MUST: API keys, authentication tokens, and service credentials MUST be accessed via environment variables, never hardcoded.
- **R-ENV-004** MUST: External service endpoints and URLs that vary by environment MUST be sourced from environment variables.
- **R-ENV-005** MUST: Feature flags and behavioral toggles that vary by environment MUST be sourced from environment variables.
- **R-ENV-006** SHOULD: A `.env.example` file SHOULD exist documenting all required and optional environment variables with descriptions.
- **R-ENV-007** SHOULD: A configuration module SHOULD validate and export typed configuration objects at startup.
- **R-ENV-008** MAY: Development-only configuration for local testing where security is not a concern MAY use hardcoded values (exception EXC-001).

### Verify

```bash
# Check for process.env usage patterns
grep -r 'process\.env\.' --include='*.ts' --include='*.tsx' --include='*.js' | head -20

# Check for hardcoded credentials or sensitive values
grep -r 'API_KEY\|TOKEN\|SECRET' --include='*.ts' --include='*.tsx' | grep -v 'process.env' | grep -v '.env.example'

# Verify .env.example exists
test -f .env.example && echo 'Environment template exists' || echo 'Missing .env.example'
```

**Accept when:**
- All environment-specific configuration values are accessed via `process.env`
- No hardcoded API keys, tokens, or credentials are found in source files
- A `.env.example` file exists documenting all required environment variables
- CI pipeline verification passes with no hardcoded credentials detected

<enforcement>
Claude Code MUST NOT skip or defer verification. All configuration sourcing MUST be validated against these rules before accepting changes.
</enforcement>