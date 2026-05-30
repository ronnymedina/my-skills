---
name: project-docs
description: Document a software project with a standard set of markdown files (README.md, docs/development.md, docs/environments.md, docs/commands.md, docs/testing.md, docs/database.md). Handles monorepos by documenting each child project. Use when the user asks to document a project, generate a README, update project documentation, review docs, audit documentation, document env vars, document commands, document the database schema, or do a docs self-review after finishing a feature.
---

# Project Docs

Maintains a consistent documentation set for software projects. Auto-detects mode (generation vs evaluation), monorepo layout, and which doc files apply.

## Documentation set

A fully documented project may contain:

- `README.md` (root)
- `docs/development.md`
- `docs/environments.md`
- `docs/commands.md`
- `docs/testing.md`
- `docs/database.md`

Each file is conditionally generated — see **Per-file skip rules** below. Templates live in `templates/`. Use them verbatim as starting points — do not invent new sections.

## Step 1: Monorepo detection

Run this BEFORE mode detection. Treat the project as a monorepo if ANY of these are true:

- **Workspace-managed**: `pnpm-workspace.yaml`, root `package.json` `workspaces` field, `nx.json`, `turbo.json`, or `lerna.json` exists.
- **Convention folders**: Any of `apps/`, `packages/`, `services/`, `libs/`, `projects/` exist at the root AND contain at least one subfolder with its own manifest (`package.json`, `pyproject.toml`, `requirements.txt`, `Cargo.toml`, `go.mod`, or `Dockerfile`).
- **Compose-orchestrated**: Root has `docker-compose.yml`, `docker-compose.yaml`, `compose.yml`, or `compose.yaml` AND there are 2 or more sibling subfolders (anywhere — at the root or under a convention folder) each containing a `Dockerfile`. This covers polyglot monorepos with no shared package manager.

If monorepo → follow **Monorepo flow**. Otherwise → follow **Single-project flow**.

## Step 2: Mode detection

For the project (or each child project in a monorepo):

1. If `docs/` does not exist OR contains zero `.md` files AND there is no `README.md` → **Generation mode**.
2. Otherwise → **Evaluation mode**.

The user can force a mode by saying "regenerate from scratch" (forces generation) or "only evaluate, don't write" (forces evaluation, read-only).

## Per-file skip rules

A doc file is generated ONLY if its trigger is present. In evaluation mode, do not flag the file as missing if its trigger isn't present.

| File | Generate only if… |
|------|-------------------|
| `README.md` | Always. |
| `docs/development.md` | Project has any of: `package.json`, `pyproject.toml`, `requirements.txt`, `Cargo.toml`, `go.mod`, `Gemfile`, `pom.xml`, `build.gradle`, `Dockerfile`. |
| `docs/environments.md` | Project has any `.env*` file (`.env.example`, `.env.sample`, `.env.template`) OR code reads env vars (`process.env.X`, `os.environ`, `os.getenv`, `std::env::var`, `System.getenv`). |
| `docs/commands.md` | Project has any of: `package.json` `scripts` field with entries, `Makefile`, `Taskfile.yml`, `justfile`, or executable scripts in `scripts/`/`bin/`. |
| `docs/testing.md` | Project has any test config: `vitest.config.*`, `jest.config.*`, `playwright.config.*`, `cypress.config.*`, `pytest.ini`, `pyproject.toml` `[tool.pytest]`, `tox.ini`, `cargo test` files in `tests/`, `go test` files (`*_test.go`). |
| `docs/database.md` | Project has any of: `prisma/schema.prisma`, `**/migrations/*.sql`, `**/migrations/*.py`, `**/models.py`, `**/*.entity.ts`, `drizzle.config.*`, `alembic.ini`. |

When a file is skipped, do NOT mention it in the README documentation index.

## Single-project flow

### Generation mode
1. Run **stack detection**.
2. Apply **Per-file skip rules** to decide which files to generate.
3. For each applicable file, copy the template from `templates/` and fill in fields.
4. Save files. Create `docs/` if missing.
5. Tell the user which files were created and which were skipped (with the reason).

### Evaluation mode
1. Run **stack detection**.
2. Read every existing doc file.
3. Compare each against the codebase using `checklists/self-review.md`.
4. Produce a single report (Missing / Stale / Inconsistent) grouped by file.
5. Do NOT edit files. Ask the user which items to apply, then make targeted edits only for approved items.

## Monorepo flow

Treat the root and each child project independently:

### Discover child projects

Use the FIRST applicable rule:

1. **Workspace manager declares paths** → use those (e.g., `pnpm-workspace.yaml` `packages:` glob, `package.json` `workspaces`, `nx.json` `projects`).
2. **Compose file declares services with `build:` directives** → each `build.context` (or shorthand build path) is a child project. Children may live at the root or anywhere — do not assume `apps/`.
3. **Convention folders** → child = any direct subfolder of `apps/`, `packages/`, `services/`, `libs/`, `projects/` that has its own manifest (`package.json`, `pyproject.toml`, `requirements.txt`, `Cargo.toml`, `go.mod`, or `Dockerfile`).
4. **Fallback** → any direct subfolder of the root that contains a `Dockerfile` (skip common non-project folders: `.git`, `node_modules`, `docs`, `scripts`, `infra`, `.github`).

A folder counts as a child only once even if multiple rules match it.

### For each child project
Run the **Single-project flow** scoped to that child's folder. Each child gets its own `README.md` and `docs/` directory inside its own folder. Per-file skip rules apply per-child — one child may have a database while another doesn't.

### For the monorepo root
The root only gets a `README.md`, using `templates/README-monorepo.md`. It must:
- Describe the monorepo purpose.
- Identify the orchestration mechanism: workspace manager (pnpm workspaces, Nx, Turborepo, Lerna), Docker Compose, both, or none.
- Provide the top-level bootstrap command(s) that actually exist (e.g., `pnpm install`, `docker compose up`, `make bootstrap`).
- Link to each child project's `README.md` with a one-line description per child.

The root does NOT get `docs/development.md`, `docs/environments.md`, etc. — those live in each child. Two exceptions:

- If a `Makefile`, `Taskfile`, or `justfile` at the root orchestrates child commands, also generate `docs/commands.md` at the root with those orchestration commands only.
- If `docker-compose.yml` at the root reads env vars (look for `${VAR}` interpolation or `env_file:`) that are not owned by any single child, also generate `docs/environments.md` at the root documenting those shared/compose-level vars only.

## Stack detection

Read these files (if present) to infer the stack. Do not assume — verify each:

- `package.json` → Node project. Check `packageManager` field and lockfiles (`pnpm-lock.yaml`, `yarn.lock`, `package-lock.json`, `bun.lockb`) to pick the package manager. Read `scripts` for commands.
- `requirements.txt`, `pyproject.toml`, `Pipfile` → Python project. Check for `poetry`, `uv`, `pip`.
- `Cargo.toml` → Rust.
- `go.mod` → Go.
- `Dockerfile`, `docker-compose.yml` → containerized; include Docker steps in production setup.
- `.env.example`, `.env.sample`, `.env.template` → source of truth for env vars.
- `prisma/schema.prisma` → Prisma + database. Read it for models.
- `**/migrations/*.sql`, `**/models.py`, `**/*.entity.ts` → database present.
- `vitest.config.*`, `jest.config.*`, `pytest.ini`, `playwright.config.*`, `cypress.config.*` → testing setup.

Only document what you can verify from the code or what the user confirms.

## Filling templates

When filling a template:

- Replace `<PLACEHOLDER>` tokens with real values.
- Delete entire sections that don't apply (don't leave "N/A" placeholders).
- For env vars, follow the exact format in `examples/environments-example.md`.
- For database models, follow the exact format in `examples/database-example.md` including the Mermaid `erDiagram`.
- Commands documented in `docs/commands.md` must come from `package.json` scripts, `Makefile` targets, or scripts the user confirms — never invented.

## Self-review trigger

When the user says "review the docs", "audit documentation", or "did I miss anything in the docs after this feature", run **Evaluation mode** end-to-end (for the root and every child if monorepo) and present a single consolidated report.

## What this skill does NOT do

- Does not write code comments or inline docstrings.
- Does not generate API reference docs (OpenAPI, JSDoc, etc.) — those belong to dedicated tools.
- Does not push changes to git or open PRs.
