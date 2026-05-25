# Adopt Environment Variables for Runtime Configuration Sources: Environment Variable Names

These rules are ALWAYS ACTIVE for all runtime configuration that varies by deployment environment, including API keys, authentication tokens, service credentials, external service endpoints, URLs, feature flags, and behavioral toggles across all TypeScript, JavaScript, and configuration files.

### Rules

- **R-ENV-001** MAY: Environment variable names MAY follow a consistent naming convention (e.g., UPPERCASE_WITH_UNDERSCORES).

### Verify

```bash
# Check for process.env usage patterns
grep -r 'process\.env\.' --include='*.ts' --include='*.tsx' --include='*.js' | head -20

# Scan for hardcoded credentials or sensitive values
grep -r 'API_KEY\|TOKEN\|SECRET' --include='*.ts' --include='*.tsx' | grep -v 'process.env' | grep -v '.env.example'

# Verify .env.example template exists
test -f .env.example && echo 'Environment template exists' || echo 'Missing .env.example'
```

**Accept when:**
- All environment-specific configuration values are accessed via process.env
- No hardcoded API keys, tokens, or credentials found in source files
- A .env.example file exists documenting all required environment variables

<enforcement>
Claude Code MUST NOT skip or defer verification. All three verification conditions must pass before accepting changes that introduce or modify environment-dependent configuration.
</enforcement>