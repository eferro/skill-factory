---
name: capturing-project-knowledge
description: "Captures the business rules, tacit knowledge, and code conventions behind a change into durable, business-readable project knowledge (CLAUDE.md, flows, conventions). Use after a diff, commit, or PR to record the why that code alone cannot communicate, so knowledge compounds across features."
argument-hint: "[optional PR/MR URL #1] [PR/MR URL #2] ..."
---

STARTER_CHARACTER = 🧠

Before anything else, read `${CLAUDE_SKILL_DIR}/KNOWLEDGE.md`. It defines what project knowledge is, the types it can take, and where each type lives. Apply it when proposing where to write — the definition determines the location, not your assessment of it. Also read every existing conventions file the project keeps (by default `.claude/rules/conventions/`) to understand current coding conventions — read all of them, regardless of whether the change appears to contain code patterns. If the project has no such location yet, note that and continue.

## Gather context before extracting

You need two things before you can capture anything: the change, and the intent behind it.

**The change.** Review the change under discussion — the working-tree diff, a specific commit range, or a branch compared to its base (`git diff <base>...HEAD`, where `<base>` is the repository's default branch). Include the conversation history. If arguments were passed, they are PR/MR URLs: fetch each one's diff (for GitHub, `gh pr diff <url>`) and include it alongside the local change. Never fetch data for a URL that was not explicitly passed as an argument. If no arguments were passed, continue silently — never stop, ask, or suggest re-invoking with a URL.

**The intent.** Find the requirement that motivated the change — a tracked ticket (Jira, Linear, GitHub/GitLab issue) or a written specification. It is context, exactly like the diff, and the *why* questions cannot be correctly formulated without it. If a tracked requirement exists but is not in the conversation, stop and ask for it; wait before proceeding. Informal restatements of the requirement do not substitute for the real thing. If I confirm no such requirement exists, proceed with the diff and conversation history alone.

Do not extract rules, propose patterns, or ask the why until you have the change and either the intent or my explicit confirmation that none exists. If either is missing, stop and request it now.

## Extract

**Business rules and tacit knowledge** — the why behind decisions that code alone doesn't capture. Without the why, there is no entry: restating what the code already shows is duplication, not capture. If behavior introduced by the change lives behind a feature flag, capture the intended behavior as if the flag were already active and removed — never reference the flag or the feature it gates. Post-removal, any such qualifier is permanently wrong. These belong on the business-domain side of project knowledge — project-level, module-level, flows, or cross-module flows depending on scope.

**Code patterns** the change applies or that appear in surrounding code. Before proposing a pattern as a convention, verify how consistently it already appears across the module or related modules — a one-change pattern proposed as convention creates false conventions that confuse future decisions. If it appears only in the current change, ask whether it is a deliberate new convention or a one-off. A convention captures the deliberate choice to use the pattern and where to apply it — not the shape of the pattern itself.

## Ask the why, then propose

Assess whether what you found is meaningful. If the change, conversation, and intent reveal no new decisions, say there is nothing to capture and stop.

For each remaining finding, ask me the full why behind the decision using AskUserQuestion — no document fills in any part of it, not the ticket, not the PR description, not the commit message. Only I can tell you why. Don't assume — ask.

Capture only what isn't already in project knowledge. When the change, the code you read, or the conversation exposes stale or contradictory existing knowledge, write the corrected content and present it alongside your additions — contradictions are your responsibility even in files the change never touched. A contradiction means documented knowledge no longer reflects domain reality — not a formatting or style issue in a pre-existing entry. Do not surface stylistic improvements to still-correct knowledge; that erodes the guarantee that every change reflects a real domain error.

Show me only the proposed changes and wait for approval before writing. When writing, follow the content expectations in KNOWLEDGE.md for each type.

## Before showing the proposal

Review every business rule, invariant, and ubiquitous-language entry you wrote — regardless of how the existing file reads. No such entry may contain any code identifier, whether it describes behavior, defines a concept, or maps values. If one does, rewrite it in plain domain language. A business rule stated in code can no longer be validated by anyone outside engineering.
