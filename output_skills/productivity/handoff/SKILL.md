---
name: handoff
description: "Compacts the current conversation into a handoff document so a fresh agent can pick up the work with full context."
argument-hint: "What will the next session be used for?"
disable-model-invocation: true
---

# Handoff

STARTER_CHARACTER = 🤝

Write a handoff document summarising the current conversation so a fresh agent can continue the work.

Save it to the temporary directory of the user's OS — not the current workspace. Report the path back to the user.

If the user passed arguments, treat them as a description of what the next session will focus on, and tailor the document to that focus: keep what the next session needs, drop what it does not.

## What earns a place in the document

The value of a handoff is the context that exists nowhere else. Prioritise accordingly:

- **Goal** — what the work is trying to achieve, and for whom.
- **Current state** — what is done and verified, what is in progress, what is untouched. Be explicit about what was *not* verified; an unverified claim inherited as fact is how the next session goes wrong.
- **Next step** — the single concrete action to take first, not a wish list.
- **Decisions and their reasons** — choices already made, and why. Without the why, the next agent relitigates them.
- **Dead ends** — approaches already tried and rejected, and what went wrong. This is often the highest-value section and the one most easily lost.
- **Constraints** — deadlines, compatibility requirements, things the user asked not to touch, environment quirks discovered the hard way.
- **References** — paths, URLs, ticket IDs, branch names, and the exact commands used to build, run, or test.
- **Suggested skills** — skills the next agent should invoke, and for which part of the work.

## What to leave out

Do not duplicate content already captured in other artifacts — specs, plans, ADRs, issues, commits, diffs. Reference them by path or URL instead. A handoff that restates a plan file goes stale the moment that file changes.

Anti-examples, each of which makes the document worse:

- Pasting a diff that `git diff` would produce on demand.
- Narrating the conversation turn by turn instead of stating where it landed.
- Restating what the codebase already says: file inventories, function signatures, directory trees.
- Recording tool calls made rather than conclusions reached.
- Hedged status such as "mostly working" — say what passes, what fails, and what was never run.
- Generic advice any competent agent already applies.

## Sensitive information

Redact API keys, tokens, passwords, connection strings, and personally identifiable information. Redact the value, keep the reference: name the variable or the secret store the next session should read it from, so the work stays actionable.

## Before finishing

Read the document back as if you had no memory of this conversation. Anything you could not act on is missing context; anything you could have looked up yourself is noise. Fix both, then hand over the path.
