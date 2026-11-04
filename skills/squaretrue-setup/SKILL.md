---
name: squaretrue-setup
description: Opt a project into the Squaretrue workflow by writing a short "Squaretrue" section into its agent instruction file. Use only when the user asks to set up Squaretrue; never offer it unprompted.
---

# Squaretrue setup

Run only on request. Never offer setup in a project that has not opted in.

## 1. Discover, don't ask

Inspect the repository for:

- The agent instruction file the host reads (for Claude Code: `CLAUDE.md`). If several exist, use the one this host reads and name it in the setup text. If none exists, setup will create the host's standard file.
- An existing `Squaretrue` section. If present, show it and ask what to change instead of adding a second one.
- Stack, build and test commands, and existing documentation. These are discovered during each task, not recorded in setup.

## 2. Ask only what the repository cannot answer

Ask in one message:

1. **Documentation mode**
   - `existing-only` (default): update documentation that already exists; create no new files; disclose missing coverage in the delivery report.
   - `full`: maintain the README + `docs/` structure, creating files when there is content; the only mode that aims to pass the five-year return test.
   - `report-only`: documentation notes in the delivery report only; no durable documentation.

   Recommend `full` if the project is an application meant to outlive an experiment, but do not choose it for the user.
2. **Action policy:** restrictions and preferences for actions such as committing, pushing, and opening pull requests. Example: "commit locally; ask before pushing to feature branches; never push to the main branch."
3. **Handoff location:** default `HANDOFF.md`.

## 3. Show the exact text, then write it

Show the user exactly what will be written, and where, before writing it:

```markdown
## Squaretrue

This project uses the Squaretrue workflow.

- Documentation: <existing-only | full | report-only>
- Action policy: <restrictions and preferences>
- Handoff location: <HANDOFF.md>
```

Add `- Packs: <links>` only if the user names project guidance packs.

Write only after the user approves. Then state:

- The action policy records restrictions and preferences; it grants no permission. Actions that need authorization still need it from the user and the host, and approving this text approves none of them.
- Standing permissions belong in the host's permission settings, not in this section.

## Never

- Create empty documentation files, templates, or hooks.
- Write permissions or credentials into the section.
