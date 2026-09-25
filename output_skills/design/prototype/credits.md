# Credits

Imported from the **`prototype`** skill by Matt Pocock:
https://github.com/mattpocock/skills/tree/main/skills/engineering/prototype

Source repository: https://github.com/mattpocock/skills (MIT License, © 2026 Matt Pocock)

A model-invoked skill that builds throwaway prototypes to answer a design question, branching into a logic/state-model demo (single HTML file, see `LOGIC.md`) or radically different UI variations on one route (see `UI.md`).

## Upstream

- Repository: https://github.com/mattpocock/skills
- Path: `skills/engineering/prototype/`
- Commit: `c55ee46073ed923f86ce59a5eb3b6d895095d1b7` (2026-09-18)
- Imported: 2026-09-25
- Mode: verbatim import (keep the diff with upstream minimal)

To see upstream changes since import:
`git -C <clone> log --oneline c55ee46..origin/main -- skills/engineering/prototype/`

## Local changes

- Added `STARTER_CHARACTER = 🧪` per this repo's convention. Body otherwise verbatim.
- Placed under local category `design/` (upstream category is `engineering/`).

Supporting files copied verbatim: `LOGIC.md`, `UI.md`.

The original's `agents/openai.yaml` was dropped — it is skills.sh metadata for
non-Claude agents.
