---
name: writing-statuslines
description: Writes Claude Code status line scripts. Use when creating, customizing, or debugging statusline configurations.
---

STARTER_CHARACTER = 📊

## Setup

Update the reference docs to get the latest from Anthropic:
```bash
python ~/.claude/skills/writing-statuslines/scripts/update-docs.py
```

## What Status Lines Are

A shell command whose stdout renders as a bar at the bottom of Claude Code, in its own row above the footer badges. With a custom status line configured, most footer keyboard hints (`esc to interrupt`, `? for shortcuts`) are no longer shown.

`/statusline <natural language>` generates a script in `~/.claude/` and updates settings; `/statusline delete` removes it.

## Configuration

Add to `~/.claude/settings.json` (user-level) or `.claude/settings.json` (project-level):

```json
{
  "statusLine": {
    "type": "command",
    "command": "~/.claude/statusline.sh",
    "padding": 2,
    "refreshInterval": 5
  }
}
```

- `command` runs in a shell: a script path or an inline command (e.g. a `jq -r` one-liner).
- `padding` (optional, default `0`): extra horizontal spacing added to the built-in spacing — relative indentation, not distance from the terminal edge.
- `refreshInterval` (optional, seconds, min `1`): also re-run on a timer. Set it for clocks or when background subagents change state while the session is idle; leave unset to run only on events.
- `hideVimModeIndicator` (optional): `true` hides the built-in `-- INSERT --` when the script renders `vim.mode` itself.

## How It Works

- Claude Code passes session JSON via stdin; the script prints to stdout
- **Every line of stdout is a row** — multi-line status lines are supported
- ANSI colors supported; OSC 8 escape sequences make text clickable (iTerm2, Kitty, WezTerm; not Terminal.app)
- Terminal size is in `COLUMNS` / `LINES` env vars — `tput cols` cannot see the terminal because output is captured
- Script must be executable (`chmod +x`); only stdout is used
- Runs under workspace trust, like hooks: blank until the folder is trusted

### When it runs

Once at session start/resume, then on: new assistant message, `/compact` finishing, permission mode change, vim mode toggle, `command` change, `refreshInterval` tick, a `rate_limits.*.resets_at` passing, a warm `prompt_cache.expires_at` passing.

Updates are **debounced at 300ms**: rapid changes batch into one run after they stop. A new trigger **cancels an in-flight script**, so a slow script may never finish.

## Key Fields

Full schema, field table, and which fields may be absent or `null`: see "Available data" in the reference.

- `model.display_name` — short model name ("Opus", "Sonnet")
- `workspace.current_dir` / `workspace.project_dir` — may differ when working in subdirectories; `workspace.repo.{host,owner,name}` from `origin`; `workspace.git_worktree` in linked worktrees
- `context_window.used_percentage` / `remaining_percentage` — pre-calculated from input tokens only; may be `null` early
- `context_window.current_usage` — raw token counts from the last API call; `null` before the first call and right after `/compact`
- `cost.total_cost_usd` — estimated at list price, resets on `/clear`
- `rate_limits.five_hour` / `seven_day` — `used_percentage`, `resets_at` (Pro/Max only; each window may be absent)
- `prompt_cache.warm`, `prompt_cache.hit_ratio` — cache state for the main conversation
- `effort.level`, `thinking.enabled`, `fast_mode`, `vim.mode`, `agent.name`
- `pr.number` / `pr.url` / `pr.review_state` — open PR (or GitLab MR, `pr.kind: "mr"`) for the branch
- `session_id` — stable per session; use it to key cache files
- `session_name`, `worktree.*` — present only when set

Optional objects (`vim`, `agent`, `pr`, `worktree`, `rate_limits`, `prompt_cache`, `effort`, `workspace.repo`…) are missing, not `null`, when they don't apply. Always use fallbacks: `jq -r '.rate_limits.five_hour.used_percentage // empty'`.

## Constraints

- Keep it scannable: glanceable in under a second, short enough not to truncate on narrow terminals (notifications share the row)
- Exit cleanly and quickly — non-zero exit or empty output blanks the status line
- Cache expensive operations (git, network) in a file keyed by `session_id`; never by `$$`/PID, which changes every run

## Anti-Patterns

- Cramming too much info — pick 3-4 data points per line
- Not consuming stdin (script must read it even if it doesn't use all fields)
- Expensive uncached operations (git commands, API calls) on every invocation
- Cache files keyed by PID, or shared across sessions
- Reading fields without null/absent fallbacks
- Using `tput cols` for width instead of `COLUMNS`
- `echo -e` for OSC 8 links — use `printf '%b'`
- Forgetting `chmod +x`
- Writing to stderr instead of stdout

## Subagent Rows

`subagentStatusLine` (same shape as `statusLine`) customizes each subagent row in the agent panel. It receives a `tasks` array plus `columns` on stdin, and prints one JSON line per row to override: `{"id": "<task id>", "content": "<row body>"}`. Omit an id to keep the default; empty `content` hides the row. Details in the reference.

## Testing

Test scripts manually with mock JSON:
```bash
echo '{"model":{"display_name":"Opus"},"workspace":{"current_dir":"/test"},"cost":{"total_cost_usd":0.05},"context_window":{"used_percentage":42.5},"session_id":"test-session"}' | COLUMNS=80 ./statusline.sh
```

Not appearing? Check `chmod +x`, stdout vs stderr, workspace trust, `disableAllHooks` / `allowManagedHooksOnly`, and run `claude --debug` for the exit code and stderr of the first invocation.

## Reference

- [references/anthropic-statusline.md](references/anthropic-statusline.md) - Complete reference: full JSON schema, prompt cache fields, examples (context bar, git with colors, cost, multi-line, clickable links, rate limits, caching, Windows) in bash, python, and node, and troubleshooting
