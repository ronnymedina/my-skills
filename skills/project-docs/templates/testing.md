# Testing

How to run tests and what each test suite covers.

## Test types

- **Unit tests** — <SCOPE_AND_LOCATION>
- **Integration tests** — <SCOPE_AND_LOCATION>
- **E2E tests** — <SCOPE_AND_LOCATION>

## Configuration

- **Test runner**: <RUNNER> (e.g., Vitest, Jest, pytest, Playwright)
- **Config file**: `<CONFIG_FILE>`
- **Required env**: tests use `.env.test` (variables documented in [environments.md](environments.md))
- **Test database**: <HOW_TEST_DB_IS_PROVISIONED> *(omit if no DB)*

## Running tests

### All tests
```bash
<TEST_ALL_COMMAND>
```

### Unit tests only
```bash
<UNIT_COMMAND>
```

### E2E tests only
```bash
<E2E_COMMAND>
```

### Watch mode
```bash
<WATCH_COMMAND>
```

### Coverage
```bash
<COVERAGE_COMMAND>
```

## Writing tests

- Test files live in `<LOCATION>` and follow the `<PATTERN>` naming convention (e.g., `*.test.ts`, `test_*.py`).
- <ANY_PROJECT_SPECIFIC_CONVENTIONS>
