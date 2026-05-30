# Testing

How to validate a skill before publishing.

## Test types

- **Manual invocation** — install the `.skill` locally, then issue prompts that should and should not trigger it.
- **Description triggering** — confirm Claude picks up the skill when expected and ignores it otherwise.

## Manual test loop

1. Package the skill:
   ```bash
   cd skills/<skill-name>
   zip -r /tmp/<skill-name>.skill .
   ```
2. Install in Claude Code / Cowork via **Save skill**.
3. In a new conversation, issue a prompt that matches the skill's description. Confirm Claude loads it.
4. Issue an unrelated prompt. Confirm the skill does NOT load (avoids false positives).
5. Walk through the skill's intended workflow end-to-end and confirm each step runs as written.

## Checklist before publishing

- [ ] `SKILL.md` has valid YAML frontmatter with `name` and `description`.
- [ ] Description includes at least 3 distinct trigger phrases the user would say.
- [ ] All files the SKILL.md references (templates, examples, scripts) actually exist.
- [ ] No hardcoded user-specific paths, names, or credentials.
- [ ] Tested in a real conversation, not just by reading the SKILL.md.

## Automated evals

This repo does not currently include automated skill evals. The `anthropic-skills:skill-creator` skill provides eval tooling — use it if you need regression coverage.
