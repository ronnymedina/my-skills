# skills

A collection of Claude Code / Cowork skills authored by Ronny.

Each skill is a self-contained folder under `skills/` with a `SKILL.md` describing when and how Claude should use it. Skills are packaged as `.skill` files (zip archives) for installation in Claude Code or Cowork.

## Requirements

- Claude Code or Cowork mode (to install and run skills).
- `zip` CLI (for packaging skill folders into `.skill` files).
- Markdown editor of choice.

## Minimum Production Setup

To "use" a skill from this repo:

1. Clone the repository.
2. Package the skill you want to install:
   ```bash
   cd skills/<skill-name>
   zip -r ../../<skill-name>.skill .
   ```
3. Open the resulting `<skill-name>.skill` file in Claude Code / Cowork and click **Save skill**.
4. Invoke the skill by triggering its description (see each skill's `SKILL.md`).

## Documentation

- [Development setup](docs/development.md) — how to author and modify skills locally.
- [Testing](docs/testing.md) — how to validate a skill before publishing.
# my-skills
