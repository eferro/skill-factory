# Credits

Imported from the **`wizard`** skill by Matt Pocock:
https://github.com/mattpocock/skills/tree/main/skills/engineering/wizard

Source repository: https://github.com/mattpocock/skills (MIT License, © 2026 Matt Pocock)

A model-invoked skill that generates an interactive bash wizard (from `template.sh`) walking a human through manual steps only they can perform: provisioning, credentials, CI secrets, third-party dashboards, one-off migrations.

## Upstream

- Repository: https://github.com/mattpocock/skills
- Path: `skills/engineering/wizard/`
- Commit: `c55ee46073ed923f86ce59a5eb3b6d895095d1b7` (2026-09-18)
- Imported: 2026-09-25
- Mode: verbatim import (keep the diff with upstream minimal)

To see upstream changes since import:
`git -C <clone> log --oneline c55ee46..origin/main -- skills/engineering/wizard/`

## Local changes

- Added `STARTER_CHARACTER = 🧙` per this repo's convention. Body otherwise verbatim.
- Placed under local category `developer-tools/` (upstream category is `engineering/`).

Supporting files copied verbatim: `template.sh`.

The original's `agents/openai.yaml` was dropped — it is skills.sh metadata for
non-Claude agents.
