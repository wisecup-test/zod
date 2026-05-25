# Adopt Async/Await Pattern for Asynchronous Operations: Type Definitions Async

These rules are ALWAYS ACTIVE for all asynchronous code development in TypeScript/JavaScript files, including benchmark implementations, test files, API client implementations, service layer code, and database access operations.

### Rules

- **R-ASYNC-001** MUST: Type definitions for async functions MUST explicitly declare Promise return types with appropriate generic parameters.

### Verify

```bash
# Count async functions in the codebase
grep -r 'async.*function\|async.*=>\|async (' --include='*.ts' --include='*.js' packages/ | wc -l

# Run ESLint with async/await rules
eslint --rule '@typescript-eslint/promise-function-async: error' packages/

# Check test files for async patterns
npm test -- --grep 'async' --reporter json | jq '.tests[] | select(.title | contains("async"))'
```

**Accept when:**
- All new asynchronous functions use async/await syntax with proper type annotations
- ESLint checks pass with no violations of async/await rules in new code
- Code review checklist confirms try-catch error handling around await statements
- Benchmark tests show no performance regressions in async operation handling
- TypeScript compiler strict mode validates all Promise return types

<enforcement>
Claude Code MUST NOT skip or defer verification. All async function type definitions MUST be checked for explicit Promise return type declarations before code is accepted.
</enforcement>