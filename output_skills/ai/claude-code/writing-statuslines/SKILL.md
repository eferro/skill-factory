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

Custom scripts that display contextual information at the bottom of Claude Code's interface. Updated when conversation messages change, at most every 300ms.

## Configuration

Add to `~/.claude/settings.json` (user-level) or `.claude/settings.json` (project-level):

```json
{
  "statusLine": {
    "type": "command",
    "command": "~/.claude/statusline.sh",
    "padding": 0
  }
}
```

`padding` is optional. Set to 0 to let the status line reach the terminal edge.

## How It Works

- Claude Code passes session context as JSON via stdin to the script
- First line of stdout becomes the status line text
- ANSI color codes supported
- Script must be executable (`chmod +x`)
- Only stdout is used (not stderr)

## JSON Input Schema

The script receives this via stdin:

```json
{
  "hook_event_name": "Status",
  "session_id": "abc123...",
  "transcript_path": "/path/to/transcript.json",
  "cwd": "/current/working/directory",
  "model": {
    "id": "claude-opus-4-1",
    "display_name": "Opus"
  },
  "workspace": {
    "current_dir": "/current/working/directory",
    "project_dir": "/original/project/directory"
  },
  "version": "1.0.80",
  "output_style": {
    "name": "default"
  },
  "cost": {
    "total_cost_usd": 0.01234,
    "total_duration_ms": 45000,
    "total_api_duration_ms": 2300,
    "total_lines_added": 156,
    "total_lines_removed": 23
  },
  "context_window": {
    "total_input_tokens": 15234,
    "total_output_tokens": 4521,
    "context_window_size": 200000,
    "used_percentage": 42.5,
    "remaining_percentage": 57.5,
    "current_usage": {
      "input_tokens": 8500,
      "output_tokens": 1200,
      "cache_creation_input_tokens": 5000,
      "cache_read_input_tokens": 2000
    }
  }
}
```

`context_window.current_usage` may be `null` if no messages have been sent yet.

## Key Fields

- `model.display_name` — short model name ("Opus", "Sonnet")
- `workspace.current_dir` / `workspace.project_dir` — may differ when working in subdirectories
- `cost.total_cost_usd` — cumulative session cost
- `context_window.used_percentage` / `remaining_percentage` — pre-calculated, ready to display
- `context_window.current_usage` — raw token counts from the last API call

## Constraints

- Output exactly one line
- Runs every 300ms at most — expensive operations must be cached
- Keep it scannable: glanceable in under a second
- Script must exit cleanly and quickly

## Anti-Patterns

- Cramming too much info — pick 3-4 data points max
- Not consuming stdin (script must read it even if it doesn't use all fields)
- Expensive uncached operations (git commands, API calls) on every invocation
- Multiple output lines (only first line is used)
- Forgetting `chmod +x`
- Writing to stderr instead of stdout

## Testing

Test scripts manually with mock JSON:
```bash
echo '{"model":{"display_name":"Sonnet"},"workspace":{"current_dir":"/test"},"cost":{"total_cost_usd":0.05},"context_window":{"used_percentage":42.5}}' | ./statusline.sh
```

## Reference

- [references/anthropic-statusline.md](references/anthropic-statusline.md) - Complete reference with examples in bash, python, and node
