# Adopt Environment Variables for Runtime Configuration Sources: Default Values Non

These rules are ALWAYS ACTIVE for all runtime configuration code, scripts, loaders, and any component that accesses deployment environment-specific settings such as API keys, service endpoints, and feature flags.

### Rules

- **R-ENV-001** SHOULD: Default values for non-sensitive configuration SHOULD be provided using fallback patterns (e.g., `process.env.VAR || 'default'`).

### Verify

```bash
# Check for process.env usage patterns
grep -r 'process\.env\.' --include='*.ts' --include='*.tsx' --include='*.js' | head -20

# Scan for hardcoded credentials not using process.env
grep -r 'API_KEY\|TOKEN\|SECRET' --include='*.ts' --include='*.tsx' | grep -v 'process.env' | grep -v '.env.example'

# Verify .env.example template exists
test -f .env.example && echo 'Environment template exists' || echo 'Missing .env.example'
```

**Accept when:**
- All environment-specific configuration values are accessed via `process.env`
- No hardcoded API keys, tokens, or credentials found in source files
- A `.env.example` file exists documenting all required environment variables
- Non-sensitive configuration uses fallback patterns with sensible defaults

<enforcement>
Claude Code MUST NOT skip or defer verification. All three verification commands must pass before accepting configuration code.
</enforcement>