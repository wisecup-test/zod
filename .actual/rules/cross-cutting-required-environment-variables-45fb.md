# Adopt Environment Variables for Runtime Configuration Sources: Required Environment Variables

These rules are ALWAYS ACTIVE for all runtime configuration that varies by deployment environment, including API keys, authentication tokens, service credentials, external service endpoints, URLs, feature flags, and behavioral toggles across documentation generation, API routes, build scripts, and data loader modules.

### Rules

- **R-ENV-001** SHOULD: Required environment variables SHOULD be validated at application startup with clear error messages if missing.

### Verify

```bash
# Check for process.env usage patterns
grep -r 'process\.env\.' --include='*.ts' --include='*.tsx' --include='*.js' | head -20

# Scan for hardcoded credentials or sensitive values not using process.env
grep -r 'API_KEY\|TOKEN\|SECRET' --include='*.ts' --include='*.tsx' | grep -v 'process.env' | grep -v '.env.example'

# Verify .env.example template exists
test -f .env.example && echo 'Environment template exists' || echo 'Missing .env.example'
```

**Accept when:**
- All environment-specific configuration values are accessed via process.env
- No hardcoded API keys, tokens, or credentials found in source files
- A .env.example file exists documenting all required environment variables

<enforcement>
Claude Code MUST NOT skip or defer verification. Automated grep-based checks in CI pipeline MUST scan for hardcoded credentials. Code review checklist MUST include verification that new configuration uses environment variables. Static analysis tools MUST be configured to flag suspicious hardcoded values. CI pipeline MUST fail if hardcoded credentials are detected. Code review MUST block merge if configuration is not properly externalized.
</enforcement>