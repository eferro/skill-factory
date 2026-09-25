# Credits

Imported from the **`domain-modeling`** skill by Matt Pocock:
https://github.com/mattpocock/skills/tree/main/skills/engineering/domain-modeling

Source repository: https://github.com/mattpocock/skills (MIT License, © 2026 Matt Pocock)

A model-invoked skill that actively builds a project's domain model while designing: challenges terms against a `CONTEXT.md` glossary, sharpens fuzzy language, stress-tests with scenarios, and records ADRs only when a decision is hard to reverse, surprising, and a real trade-off.

## Upstream

- Repository: https://github.com/mattpocock/skills
- Path: `skills/engineering/domain-modeling/`
- Commit: `c55ee46073ed923f86ce59a5eb3b6d895095d1b7` (2026-09-18)
- Imported: 2026-09-25
- Mode: verbatim import (keep the diff with upstream minimal)

To see upstream changes since import:
`git -C <clone> log --oneline c55ee46..origin/main -- skills/engineering/domain-modeling/`

## Local changes

- Added `STARTER_CHARACTER = 📖` per this repo's convention. Body otherwise verbatim.
- Placed under local category `design/` (upstream category is `engineering/`).

Supporting files copied verbatim: `ADR-FORMAT.md`, `CONTEXT-FORMAT.md`.

The original's `agents/openai.yaml` was dropped — it is skills.sh metadata for
non-Claude agents.
