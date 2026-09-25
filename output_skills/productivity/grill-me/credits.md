# Credits

Imported from the **`grill-me`** skill by Matt Pocock:
https://github.com/mattpocock/skills/tree/main/skills/productivity/grill-me

Source repository: https://github.com/mattpocock/skills (MIT License, © 2026 Matt Pocock)

A user-invoked shortcut (`disable-model-invocation: true`) that simply calls the `grilling` skill. Requires `grilling` to be installed too.

## Upstream

- Repository: https://github.com/mattpocock/skills
- Path: `skills/productivity/grill-me/`
- Commit: `c55ee46073ed923f86ce59a5eb3b6d895095d1b7` (2026-09-18)
- Imported: 2026-09-25
- Mode: verbatim import (keep the diff with upstream minimal)

To see upstream changes since import:
`git -C <clone> log --oneline c55ee46..origin/main -- skills/productivity/grill-me/`

## Local changes

- None. `SKILL.md` is verbatim (a one-line user-invoked alias that calls the `grilling` skill).

The original's `agents/openai.yaml` was dropped — it is skills.sh metadata for
non-Claude agents.
