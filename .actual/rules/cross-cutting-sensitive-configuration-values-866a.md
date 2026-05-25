# Adopt Environment Variables for Runtime Configuration Sources: Sensitive Configuration Values

These rules are ALWAYS ACTIVE for all files matching the configured scope.

### Rules

- **R-ENVVAR-001** MUST: Sensitive configuration values (API keys, tokens, credentials) MUST NOT be hardcoded in source files.

### Verify

```bash
# Check for process.env usage patterns
grep -r 'process\.env\.' --include='*.ts' --include='*.tsx' --include='*.js' | head -20

# Check for hardcoded sensitive patterns
grep -r 'API_KEY\|TOKEN\|SECRET' --include='*.ts' --include='*.tsx' | grep -v 'process.env' | grep -v '.env.example'

# Verify .env.example template exists
test -f .env.example && echo 'Environment template exists' || echo 'Missing .env.example'
```

**Accept when:**
- All environment-specific configuration values are accessed via process.env
- No hardcoded API keys, tokens, or credentials found in source files
- A .env.example file exists documenting all required environment variables

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated grep-based checks in CI pipeline scanning for hardcoded credentials are mandatory. Code review checklist MUST include verification that new configuration uses environment variables. Static analysis tools MUST be configured to flag suspicious hardcoded values. CI pipeline MUST fail if hardcoded credentials are detected in source files.
</enforcement>