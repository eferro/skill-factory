# Credits

Adapted from the **`handoff`** skill by Matt Pocock:
https://github.com/mattpocock/skills/tree/main/skills/productivity/handoff

Source repository: https://github.com/mattpocock/skills (MIT License, © 2026 Matt Pocock)

The original is a short user-invoked prompt that compacts the current
conversation into a handoff document for a fresh agent, saved outside the
workspace.

## What changed in this adaptation

Expanded from an 8-line prompt into a structured skill, keeping the original's
invariants intact:

- **Explicit document structure**: goal, current state, next step, decisions and
  their reasons, dead ends, constraints, references, suggested skills — so the
  output is consistent across sessions rather than shaped by whatever the model
  happened to consider relevant.
- **Anti-examples for exclusion**: the original's no-duplication rule is kept and
  made concrete (no pasted diffs, no turn-by-turn narration, no restating what
  the codebase already says).
- **Verification honesty**: the handoff must distinguish what was verified from
  what was assumed, so the next session does not inherit unchecked claims as
  fact.
- **Redaction made actionable**: redact the secret's value but keep the pointer
  to where it lives, so the next session can still do the work.
- **Read-back check** before finishing, against this repo's progressive-disclosure
  conventions.
- Added `STARTER_CHARACTER` per this repo's convention.

Preserved unchanged: save to the OS temporary directory rather than the
workspace, the "suggested skills" section, the no-duplication rule with
references by path or URL, redaction of sensitive information, arguments treated
as the next session's focus, and `disable-model-invocation: true` (user-invoked
only).

The original's `agents/openai.yaml` was dropped — it is skills.sh metadata for
non-Claude agents, and its `allow_implicit_invocation: false` is already
expressed by `disable-model-invocation: true` in the frontmatter.
