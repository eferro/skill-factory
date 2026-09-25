# Credits

Imported from the **`grill-with-docs`** skill by Matt Pocock:
https://github.com/mattpocock/skills/tree/main/skills/engineering/grill-with-docs

Source repository: https://github.com/mattpocock/skills (MIT License, © 2026 Matt Pocock)

A user-invoked shortcut (`disable-model-invocation: true`) that calls the `grilling` and `domain-modeling` skills together, so the interview writes `CONTEXT.md` and ADRs as decisions crystallise. Requires both to be installed (`productivity/grilling`, `design/domain-modeling`).

## Upstream

- Repository: https://github.com/mattpocock/skills
- Path: `skills/engineering/grill-with-docs/`
- Commit: `c55ee46073ed923f86ce59a5eb3b6d895095d1b7` (2026-09-18)
- Imported: 2026-09-25
- Mode: verbatim import (keep the diff with upstream minimal)

To see upstream changes since import:
`git -C <clone> log --oneline c55ee46..origin/main -- skills/engineering/grill-with-docs/`

## Local changes

- None. `SKILL.md` is verbatim.
- Placed under local category `design/` (upstream category is `engineering/`).

The original's `agents/openai.yaml` was dropped — it is skills.sh metadata for
non-Claude agents.
