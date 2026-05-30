# Development Setup

How to run the project locally for development.

## Prerequisites

- <RUNTIME_AND_VERSION>
- <PACKAGE_MANAGER>
- <LOCAL_SERVICES> (e.g., PostgreSQL running locally or via Docker)

## First-time setup

1. Clone the repo and enter the directory.
2. Install dependencies:
   ```bash
   <INSTALL_COMMAND>
   ```
3. Copy environment file:
   ```bash
   cp .env.example .env
   ```
   Fill in the variables marked **Required** in [environments.md](environments.md).
4. Start local services (if using Docker):
   ```bash
   docker compose up -d
   ```
5. Run database migrations (omit if no DB):
   ```bash
   <MIGRATION_COMMAND>
   ```
6. Seed the database (omit if no seed script):
   ```bash
   <SEED_COMMAND>
   ```

## Running the dev server

```bash
<DEV_COMMAND>
```

The dev server runs at `<DEV_URL>` with hot reload enabled.

## Common dev tasks

See [commands.md](commands.md) for the full command reference.

## Troubleshooting

- **<COMMON_ISSUE>**: <SOLUTION>
