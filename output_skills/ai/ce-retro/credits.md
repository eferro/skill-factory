# Credits

Imported from the **`ce-retro`** skill of Every's Compound Engineering plugin:
https://github.com/EveryInc/compound-engineering-plugin/tree/main/skills/ce-retro

Source repository: https://github.com/EveryInc/compound-engineering-plugin (MIT License, © 2025 Every)

Looks back over agent sessions in a repo (current session by default, or a named
scope across harnesses), finds what in the repo's environment keeps costing
agents effort or leading them into mistakes, and lands only the fixes the
evidence justifies, after user approval. Keeps a local decision ledger.

## Status

**On trial** (since 2026-11-14). Imported to try it out and derive improvements
for our own version. Keep notes of what works and what does not before adapting.

## Upstream

- Repository: https://github.com/EveryInc/compound-engineering-plugin
- Path: `skills/ce-retro/`
- Commit: `d6d00627bb70e933664d5641b41502d4121a1252` (2026-11-11)
- Imported: 2026-11-14
- Mode: verbatim import (keep the diff with upstream minimal)

To see upstream changes since import:
`git -C <clone> log --oneline d6d0062..origin/main -- skills/ce-retro/`

## Local changes

- Added `STARTER_CHARACTER = 🔁🪞` per this repo's convention. Everything else verbatim.
- Placed under local category `ai/`.
- Added `disable-model-invocation: true` to the frontmatter while on trial: the
  skill only runs when invoked explicitly with `/ce-retro`, never auto-triggered
  (its description mentions "postmortem", which could match incident work).

## Security review (2026-11-14)

Code is defensive: no network calls, no eval, deletes only its own temp files,
refuses symlinks, creates 0700 dirs, never pushes. Risks come from its authority:

- **Config changes derived from untrusted transcripts.** After approval it edits
  instruction files and harness settings (hooks, MCP servers, permissions, env).
  Do not bulk-approve a group containing hooks/MCP/permission changes; review item by item.
- **Self-declared authority.** Invoking it "authorizes" edits and commits without
  asking each time; commits land on the current branch (main in trunk-based repos).
- **Cross-project privacy.** Session discovery opens the first lines of every
  recent session file in `~/.claude/projects` (all projects). Extracts (up to
  800 chars per turn, 200 per error, no secret redaction) go to
  `/tmp/compound-engineering-<uid>/ce-retro/` and are never cleaned up.
  Remove that directory after each run.
- **Ledger inside the repo** at `.context/compound-engineering/ce-retro/`.
  Mitigated by a global gitignore entry for `.context/` (`~/.config/git/ignore`).
- **Missing sibling skills** (see below): routed items end as "approved but not applied".

Trial guidance: start with the current session only, in a non-sensitive repo,
before asking for wider scopes.

## Known dependencies on the upstream plugin

The skill refers to sibling skills from the same plugin that are **not** in this repo:

- `ce-noslop`: used for writing the approval account and report (falls back to plain writing if missing).
- `ce-compound`, `ce-setup`, `ce-plan`: targets for routing approved items that are not environment edits.

Without them, routed items cannot be handed off. Candidate area for adaptation.

The ledger is stored at `<main checkout>/.context/compound-engineering/ce-retro/`
(see `scripts/retro-state.py`).
