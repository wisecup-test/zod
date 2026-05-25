# Adopt Async/Await Pattern for Asynchronous Operations: Asynchronous Functions Declared

These rules are ALWAYS ACTIVE for all asynchronous code development in TypeScript/JavaScript files, including benchmark implementations, test files, API client implementations, service layer code, and database access operations.

### Rules

- **R-ASYNC-001** MUST: All asynchronous functions MUST be declared using the async keyword and return Promise types.

### Verify

```bash
# Count async function declarations in the codebase
grep -r 'async.*function\|async.*=>\|async (' --include='*.ts' --include='*.js' packages/ | wc -l

# Run ESLint with async/await enforcement rules
eslint --rule '@typescript-eslint/promise-function-async: error' packages/

# Verify test files use async patterns
npm test -- --grep 'async' --reporter json | jq '.tests[] | select(.title | contains("async"))'
```

**Accept when:**
- All new asynchronous functions use async/await syntax with proper type annotations
- ESLint checks pass with no violations of async/await rules in new code
- Code review checklist confirms try-catch error handling around await statements
- Benchmark tests show no performance regressions in async operation handling
- TypeScript compiler strict mode validates Promise return types without errors

<enforcement>
Claude Code MUST NOT skip or defer verification. All async/await patterns must be validated through ESLint and TypeScript compilation before acceptance.
</enforcement>