# Credits

Imported from the **`grilling`** skill by Matt Pocock:
https://github.com/mattpocock/skills/tree/main/skills/productivity/grilling

Source repository: https://github.com/mattpocock/skills (MIT License, © 2026 Matt Pocock)

A model-invoked skill that interviews the user relentlessly about a plan, decision, or idea, working a design tree in rounds (the frontier of currently answerable decisions, each with a recommended answer), delegating fact-finding to sub-agents.

## Upstream

- Repository: https://github.com/mattpocock/skills
- Path: `skills/productivity/grilling/`
- Commit: `c55ee46073ed923f86ce59a5eb3b6d895095d1b7` (2026-09-18)
- Imported: 2026-09-25
- Mode: verbatim import (keep the diff with upstream minimal)

To see upstream changes since import:
`git -C <clone> log --oneline c55ee46..origin/main -- skills/productivity/grilling/`

## Local changes

- Added `STARTER_CHARACTER = 🔥` per this repo's convention. Body otherwise verbatim.

The original's `agents/openai.yaml` was dropped — it is skills.sh metadata for
non-Claude agents.
