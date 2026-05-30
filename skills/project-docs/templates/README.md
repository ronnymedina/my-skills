# <PROJECT_NAME>

<ONE_SENTENCE_DESCRIPTION>

<PARAGRAPH_EXPLAINING_WHAT_THE_PROJECT_DOES_AND_WHO_USES_IT>

## Requirements

- <RUNTIME> (e.g., Node.js >= 20, Python >= 3.11)
- <PACKAGE_MANAGER> (e.g., pnpm >= 9)
- <DATABASE> (e.g., PostgreSQL >= 15) — omit if no database
- <OPTIONAL_SERVICES> (e.g., Redis, Docker) — omit if not used

## Minimum Production Setup

Steps to run the project in production with the minimum required configuration.

1. Clone the repository.
2. Install dependencies:
   ```bash
   <INSTALL_COMMAND>
   ```
3. Copy `.env.example` to `.env` and fill in required variables (see [environments.md](docs/environments.md)).
4. Run database migrations (omit if no DB):
   ```bash
   <MIGRATION_COMMAND>
   ```
5. Build the project (omit if not applicable):
   ```bash
   <BUILD_COMMAND>
   ```
6. Start the application:
   ```bash
   <START_COMMAND>
   ```

The service will be available at `<URL_OR_PORT>`.

## Documentation

- [Development setup](docs/development.md) — local environment, dependencies, dev server.
- [Environment variables](docs/environments.md) — full reference of all env vars.
- [Commands](docs/commands.md) — every CLI command this project exposes.
- [Testing](docs/testing.md) — how to run unit and e2e tests.
- [Database](docs/database.md) — schema, models, relationships. (Omit link if no DB.)
