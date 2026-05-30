# <MONOREPO_NAME>

<ONE_PARAGRAPH_DESCRIBING_THE_MONOREPO>

## Orchestration

- **Type**: <pnpm workspaces | Nx | Turborepo | Lerna | Yarn workspaces | npm workspaces | Docker Compose | Makefile-driven | none>
- **Layout**: <describe where children live — e.g., "each app is a top-level folder with its own Dockerfile" or "under apps/ and packages/">

## Bootstrap

Run the project locally:

```bash
<BOOTSTRAP_COMMAND>
```

For workspace-managed monorepos this is typically `pnpm install`. For compose-orchestrated monorepos it's typically `docker compose up -d` (after copying `.env.example` to `.env`). List only commands that actually exist in this repo.

<OPTIONAL_ADDITIONAL_BOOTSTRAP_STEPS>

## Projects

- **[<child-name>](<path>/README.md)** — <ONE_LINE_DESCRIPTION>
- **[<child-name>](<path>/README.md)** — <ONE_LINE_DESCRIPTION>
- **[<child-name>](<path>/README.md)** — <ONE_LINE_DESCRIPTION>

*(Group under `### apps/`, `### packages/`, etc., only if children are organized that way. Otherwise keep a flat list.)*

## Root-level docs

- [Commands](docs/commands.md) — orchestration commands (Makefile / Taskfile / compose helpers). *Omit link if not generated.*
- [Environment variables](docs/environments.md) — shared compose-level env vars. *Omit link if not generated.*

---

Each child project owns its own README and `docs/` folder. Open a project link above for setup, environment variables, commands, testing, and database details specific to that project.
