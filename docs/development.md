# Development Setup

How to author and modify skills locally.

## Prerequisites

- A text editor.
- `zip` CLI (built-in on macOS and Linux).
- Claude Code or Cowork mode for testing the skill end-to-end.

## Repository layout

```
skills/
└── <skill-name>/
    ├── SKILL.md          # Required. Frontmatter + instructions for Claude.
    ├── templates/        # Optional. Reusable starting-point files.
    ├── examples/         # Optional. Reference outputs.
    └── checklists/       # Optional. Step lists Claude follows.
```

## Authoring a new skill

1. Create a folder under `skills/` named with the skill identifier (kebab-case).
2. Add a `SKILL.md` with YAML frontmatter at the top:
   ```markdown
   ---
   name: <skill-name>
   description: <one paragraph with explicit trigger phrases>
   ---
   ```
3. Write the body as short, imperative instructions — what Claude must do, in what order.
4. Put bulky content (templates, examples, long reference data) in sibling folders so the SKILL.md stays light. Reference them by relative path.

## Modifying an existing skill

1. Edit files inside `skills/<skill-name>/`.
2. Repackage with the steps in [README.md](../README.md#minimum-production-setup).
3. Re-install in Claude Code / Cowork to pick up the changes.

## Conventions

- **Frontmatter description**: include the literal trigger phrases a user would say. Vague descriptions = the skill never activates.
- **One purpose per skill**. If a skill does two unrelated things, split it.
- **Never invent commands or tools** in instructions — only reference things that exist or that the user confirms.
