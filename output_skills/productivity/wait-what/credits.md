# Credits

Imported from the **`wait-what`** skill by Matt Pocock:
https://github.com/mattpocock/skills/tree/main/skills/productivity/wait-what

Source repository: https://github.com/mattpocock/skills (MIT License, © 2026 Matt Pocock)

A user-invoked prompt (`disable-model-invocation: true`) to fire when the last message did not land: the agent re-pitches it with context, in ASD-STE100 Simplified Technical English, using the ubiquitous language from `CONTEXT.md` (or `CONTEXT-MAP.md`).

## Upstream

- Repository: https://github.com/mattpocock/skills
- Path: `skills/productivity/wait-what/`
- Commit: `c55ee46073ed923f86ce59a5eb3b6d895095d1b7` (2026-09-18)
- Imported: 2026-09-25
- Mode: verbatim import (keep the diff with upstream minimal)

To see upstream changes since import:
`git -C <clone> log --oneline c55ee46..origin/main -- skills/productivity/wait-what/`

## Local changes

- None. `SKILL.md` is verbatim (a one-paragraph user-invoked prompt).

The original's `agents/openai.yaml` was dropped — it is skills.sh metadata for
non-Claude agents.
