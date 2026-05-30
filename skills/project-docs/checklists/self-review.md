# Self-Review Checklist

Run this checklist in **evaluation mode**. For each file, compare doc content against the codebase.

## README.md

- [ ] Description matches what the project actually does (cross-check with `package.json` `description` field, main module docstring, or top-level comments).
- [ ] Requirements list includes every runtime declared in `package.json` `engines`, `pyproject.toml` `requires-python`, or `Dockerfile` base image.
- [ ] Minimum production setup commands actually exist (check `package.json` `scripts` or `Makefile`).
- [ ] Documentation index links to every file that exists under `docs/`. Flag broken links.

## docs/development.md

- [ ] All listed install/setup commands exist as scripts.
- [ ] Dev server command matches `package.json` `scripts.dev` (or equivalent).
- [ ] If `docker-compose.yml` exists, the doc mentions it.
- [ ] If `.env.example` exists, the doc instructs copying it.

## docs/environments.md

- [ ] Every variable in `.env.example` (or `.env.sample`) appears in the doc.
- [ ] No variable in the doc is missing from `.env.example` (stale entry).
- [ ] Each variable has: Default, Required, and where applicable Valores/Ejemplo/Rango.
- [ ] Variables read in code (search for `process.env.X`, `os.environ["X"]`, `os.getenv("X")`, `env.X`) all appear in the doc.
- [ ] Required-vs-optional matches reality: variables with no default in code should be Required: `true`.

## docs/commands.md

- [ ] Every script in `package.json` `scripts` is documented OR explicitly intentionally omitted (internal pre/post hooks).
- [ ] Every documented command actually exists as a script or is a valid CLI call.
- [ ] No outdated commands (referencing removed scripts).

## docs/testing.md

- [ ] Test runner matches the config file present in the repo (e.g., `vitest.config.ts` → Vitest).
- [ ] All documented test commands exist.
- [ ] If `.env.test` is referenced, it exists or is documented as needing to be created.

## docs/database.md

- [ ] Every model in `schema.prisma` (or `models.py`, entity files) appears.
- [ ] Every model in the doc still exists in the schema.
- [ ] Field lists match: flag missing fields, removed fields, type changes, nullability changes.
- [ ] Enums match what's defined in the schema.
- [ ] Mermaid diagram includes all models documented above it.

## Cross-file consistency

- [ ] Same env var name spelled identically in `environments.md`, `development.md`, `README.md`.
- [ ] Commands referenced in `README.md` and `development.md` match the canonical version in `commands.md`.
- [ ] Project name consistent across all files.

## Report format

Group findings as:

```
### README.md
- Missing: <item>
- Stale: <item>
- Inconsistent: <item> (vs. <other file>)

### docs/environments.md
- Missing: REDIS_URL (read in src/cache.ts but not documented)
- Stale: OLD_API_KEY (documented but not in .env.example or code)
```

End with: "Want me to apply any of these? Reply with the file names or 'all'."
