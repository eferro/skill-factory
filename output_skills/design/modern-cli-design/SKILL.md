---
name: modern-cli-design
description: Principles for scalable, modern command-line tools - object-command architecture (noun-verb), LLM-optimized help, JSON output, concurrency patterns, credential management. Use when building CLIs, designing command structures, or implementing terminal applications.
---

STARTER_CHARACTER = 🔧⚡

# Modern CLI Design

Principles for building scalable, maintainable command-line tools based on proven patterns from Docker, Kubernetes, GitHub CLI, and WordPress CLI.

## Architecture

### Object-Command Model (Noun-Verb)

Structure commands as `<resource> <action>` rather than flags-based approaches.

**Structure**: `cli <object> <verb> [flags]`
- `wp plugin list`
- `gh issue create`
- `docker container stop`
- `kubectl pod delete`

**Benefits**:
- Predictable: users guess future commands from existing patterns
- Isolated code: each command is self-contained, like microservices
- Scalable: avoids flag proliferation and code duplication
- Reusable: global flags apply across all commands

**Anti-pattern**: Flag-heavy single commands that try to do multiple things
- ✗ `tool --action=list --resource=plugins`
- ✗ `tool --create-issue --type=bug`

### Unix Philosophy Integration

**Do one thing well, play well with others**:
- Accept input from stdin
- Write output to stdout
- Chain with pipes: `cli users list | jq '.[] | select(.active==true)'`
- Exit codes: 0 success, non-zero failure
- Respect environment variables

## LLM Optimization

LLMs discover and learn CLI tools by reading help output and examples. Optimize for machine consumption.

### Self-Documenting Help

**Extensive help text with examples**:
- Every command must have `--help`
- Include 3-5 concrete usage examples per command
- Show common patterns and edge cases
- Explain each flag's purpose and impact

**Why**: LLMs parse help to understand tool capabilities. Sparse help means LLMs won't use your tool correctly.

### Autocomplete Files

Provide shell completion files (bash, zsh, fish). These serve dual purposes:
- Human productivity
- Machine discovery of command surface

## Output Strategy

### JSON as First-Class Citizen

**Always provide JSON output option**: `--output json` or `--format json`

**Rationale**:
- PowerShell moves objects, not text - JSON is the interchange format
- Automation requires structured data
- LLMs consume JSON better than parsing text tables
- Interoperability with modern toolchains

**Anti-pattern**: Text-only output that requires brittle parsing with awk/sed

### Separate Human vs Machine Output

**Human output**:
- Tables with aligned columns
- Color coding for status
- Progress bars for long operations
- Rich formatting (use libraries like `bubble tea` in Go)

**Machine output** (`--output json`):
- Structured data: JSON, JSONL, CSV
- No formatting, no colors, no progress indicators
- Stable schema across versions
- Documented fields

**Never rely on external tools** (like `jq`) to format your output. Own the format strategy.

## Long-Running Operations

### Concurrency Patterns

For operations on large datasets or remote services:

**Chunk and parallelize**:
- Split work into independent units
- Process chunks concurrently (e.g., goroutines in Go)
- Utilize all CPU cores
- Show progress: `Processing 1000/5000 items (20%)`

**Rationale**: Users expect CLIs to be fast. Sequential processing of 10,000 items is unacceptable when you can parallelize.

### Resilience (rsync model)

For operations lasting minutes to hours:

**Essential features**:
- Checkpoint progress to disk
- Resume from interruption point
- Retry failed operations with exponential backoff
- Idempotent operations: safe to re-run

**Anti-pattern**: Starting from zero after a 2-hour process fails at 90%

### Responsive Remote Operations

When calling remote APIs:
- Non-blocking waits with timeout configuration
- Clear timeout error messages
- Allow user-configurable timeouts
- Show "waiting for response..." indicators

## State Management

**Prefer stateless**: CLIs should not maintain persistent state unless absolutely necessary.

**When state is required** (e.g., multi-hour operations):
- Use temporary embedded databases (SQLite)
- Persist to a "system of record" (remote service) as soon as possible
- Clean up temporary state on completion
- Document state file locations

## Security and Credentials

### Never Be a Password Manager

**Do not**:
- Store credentials in config files
- Hardcode secrets in binaries
- Accept passwords via command-line arguments (visible in `ps` output)

**Do**:
- Integrate with system credential stores (OS keychains)
- Support external credential providers
- Use short-lived tokens (e.g., AWS session tokens)
- Read sensitive input via stdin or secure prompts

**Reasonable pattern**: Temporary session tokens that auto-expire
- User authenticates once per session
- CLI stores token in memory or secure temp location
- Token expires after configurable time
- Reduces authentication friction without long-term credential storage

## Implementation Recommendations

### Language Choice

**Recommended**: Go or Rust
- Go: simple concurrency (goroutines), single binary, cross-platform
- Rust: memory safety, performance, zero-cost abstractions

**Why not C/C++**: Memory management complexity doesn't justify performance gains for most CLIs

### Go Ecosystem Tools

If using Go:
- **Cobra**: implements object-command model natively
- **Pflags**: robust flag parsing (better than stdlib)
- **Tablewriter**: formatted table output
- **Bubble Tea**: rich terminal UIs
- **Survey**: interactive prompts

### API-First Design

Modern CLIs primarily interact with remote services:
- Design for HTTP APIs, not local system calls
- Handle network failures gracefully
- Respect rate limits
- Cache responses when appropriate

## Output Format Control

**Flag naming**:
- `--output <format>` or `-o <format>`
- `--format <format>` or `-f <format>`

**Common formats**:
- `json`: structured data
- `yaml`: configuration-friendly
- `table`: human-readable default
- `csv`: spreadsheet-compatible
- `jsonl`: streaming line-delimited JSON

**Per-format considerations**:
- JSON: must be parseable by `jq`
- YAML: preserve key order
- Table: align columns, truncate long values
- CSV: proper escaping, header row

## Error Handling

**Structured error messages**:
- Context: what operation failed
- Reason: why it failed
- Action: what user should do

Example:
```
Error: Failed to create issue
Reason: API returned 403 Forbidden
Action: Check your authentication token with 'cli auth status'
```

**Anti-pattern**: Generic errors like "Operation failed" with no context

## Validation and Feedback

**Fail fast**:
- Validate inputs before expensive operations
- Check prerequisites (auth, network, dependencies)
- Confirm destructive operations: "Delete 50 items? (y/N)"

**Progress indicators**:
- Spinner for indeterminate operations
- Progress bar for known-duration tasks
- Status updates every 5-10 seconds for long operations

## Documentation Requirements

**Minimum documentation**:
- README with installation and quickstart
- `--help` for every command with examples
- `--version` showing version and build info
- Man pages (optional but professional)

**Help structure**:
```
USAGE:
  cli resource action [flags]

DESCRIPTION:
  Brief description of what this command does

EXAMPLES:
  cli resource action --flag value
  cli resource action --format json | jq '.field'

FLAGS:
  --flag    Description of flag
```

## Testing Strategy

**Test levels**:
- Unit: test command logic in isolation
- Integration: test against real services (with test accounts)
- Smoke: basic sanity checks on compiled binary

**Key test scenarios**:
- All commands with `--help` succeed
- JSON output is valid JSON
- Error cases return non-zero exit codes
- Long-running operations handle SIGINT gracefully

## Anti-Patterns to Avoid

**Don't**:
- Mix multiple actions in one command via flags
- Assume tools are installed (check and fail with helpful message)
- Use inconsistent terminology across commands
- Make destructive operations silent (always confirm or require `--force`)
- Ignore stdin/stdout conventions
- Block indefinitely without timeout
- Log to stdout (use stderr for logs, stdout for data)

## Consistency Principles

**Across your CLI**:
- Same flag names for same purposes (`--output`, not sometimes `--format`)
- Consistent resource naming (plural or singular, pick one)
- Predictable verb choices (create, list, get, update, delete)
- Uniform error message format
- Standardized JSON schema patterns

**Example consistency**:
```
cli users list --output json
cli plugins list --output json
cli issues list --output json
```

Not:
```
cli users show-all --format json
cli list-plugins -o json
cli issue-list --json
```
