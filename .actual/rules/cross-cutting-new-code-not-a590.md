# Adopt Async/Await Pattern for Asynchronous Operations: New Code Not

These rules are ALWAYS ACTIVE for all new asynchronous code in TypeScript/JavaScript files, including benchmark implementations, test files, API client implementations, service layer code, and database access operations.

### Rules

- **R-ASYNC-001** SHOULD NOT: New code SHOULD NOT use callback-based patterns or raw Promise constructors unless interfacing with legacy APIs.

### Verify

```bash
# Count async/await usage in codebase
grep -r 'async.*function\|async.*=>\|async (' --include='*.ts' --include='*.js' packages/ | wc -l

# Run ESLint with async/await enforcement rules
eslint --rule '@typescript-eslint/promise-function-async: error' packages/

# Check test files for async patterns
npm test -- --grep 'async' --reporter json | jq '.tests[] | select(.title | contains("async"))'
```

**Accept when:**
- All new asynchronous functions use async/await syntax with proper type annotations
- ESLint checks pass with no violations of async/await rules in new code
- Code review checklist confirms try-catch error handling around await statements
- Benchmark tests show no performance regressions in async operation handling
- Exceptions (legacy API integration, documented performance issues) are approved by tech lead and logged with reference to EX-001 or EX-002

<enforcement>
Claude Code MUST NOT skip or defer verification. ESLint checks MUST pass in CI pipeline. Code review MUST confirm async/await patterns before merge. Violations block pull requests until corrected.
</enforcement>