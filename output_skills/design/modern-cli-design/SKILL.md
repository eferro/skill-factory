---
name: modern-cli-design
description: "Principles for building Unix-composable command-line tools in Go: stdout/stderr discipline, JSON and plain output modes, semantic exit codes, noun-verb commands, structured errors. Use when designing, building, or reviewing CLIs."
---

STARTER_CHARACTER = 🔧⚡

# Modern CLI Design

Specialized concerns (long-running operations, credentials, testing) live in `references/` — see the loading guidance at the end of this file.

---

## Core principle: stdout is for data, stderr is for everything else

stdout carries the product the user asked for — results, JSON, records. stderr carries everything else — progress, spinners, warnings, errors, debug, prompts.

A single spinner character on stdout breaks every downstream pipe. `mycli list | jq .` must never see a progress indicator on stdout.

Buffering matters. stdout is line-buffered on a TTY and block-buffered when piped (~2x faster than stderr due to fewer write syscalls). stderr is unbuffered — every write is a syscall, but error messages appear immediately even on crash.

Check TTY on stdout and stderr independently. A user running `mycli run 2>/dev/tty | jq .` has stdout piped and stderr on a terminal — spinners on stderr are correct in that case.

In Go, write data with `os.Stdout.Write` / `fmt.Fprintln(os.Stdout, ...)` and diagnostics with `fmt.Fprintln(os.Stderr, ...)`. Use `github.com/mattn/go-isatty` to detect TTY per file descriptor.

---

## Format flag hierarchy

Four output modes with different contracts:

- **Default (human)**: colors, tables, formatted text, progress on stderr. Not a contract — may change between versions.
- **`--plain`**: one record per line, no colors, flat rows with no borders. Stable across minor versions. Enables `mycli list --plain | grep error | wc -l`.
- **`--json`**: structured JSON on stdout. stdout contains ONLY valid JSON — zero spinners, zero colors, zero progress. Schema is versioned. `--json` implies non-interactive regardless of TTY.
- **`--format ndjson`**: newline-delimited JSON for streaming. Each line is one parseable object. Include a `type` field per record to multiplex events. Final line may be a summary record.

JSON envelope is consistent across every command:

```json
{"ok": true, "data": {...}}
{"ok": false, "error": {"code": "...", "message": "...", "fix": "...", "transient": false}}
```

The `transient` flag tells retry logic whether the failure may resolve on its own.

---

## Exit codes

Map to the most important failure modes for the tool. Document them in `--help`.

- `0` success
- `1` domain failure — expected failure mode (threshold not met, validation rejected, resource missing)
- `2` invalid usage — bad flags, missing required args, type errors on input
- `75` temporary failure — network timeout, 503, rate limit. Retry may help. Mirrors `transient: true` in JSON output.
- `78` config error — invalid or missing config file
- `130` SIGINT (128+2) — user pressed Ctrl-C
- `141` SIGPIPE (128+13) — pipe consumer closed early. Exit silently.
- `143` SIGTERM (128+15) — process was terminated

Non-zero exit codes always accompanied by a stderr explanation. Never use codes above 125 for application errors — those are reserved for signals (128 + signal number).

In Go, prefer `os.Exit(code)` from `main` only. Handlers return errors; the CLI adapter translates to exit codes.

---

## TTY detection and color

Decision priority (first match wins):

1. `--format json` / `--json` / `--format ndjson` — non-interactive, no color
2. `--no-color` flag — disable color
3. `NO_COLOR` env var non-empty — disable color. This is a de facto standard across the ecosystem.
4. `FORCE_COLOR` env var — enable color regardless of TTY
5. `TERM=dumb` — disable color and animations
6. `CI=true` — no interactive prompts
7. stdout is not a TTY — plain output, no spinners on stdout
8. Default — full interactive with colors

Spinners on stderr remain valid when stdout is piped.

---

## Output stability — stdout is a public API

Changes to the shape of machine-readable output (`--plain`, `--json`) are breaking changes to the CLI contract. Scripts and automation depend on them.

Additive is safe: new subcommands, new flags with preserving defaults, new optional JSON fields.

Breaking: removing or renaming flags, removing or renaming JSON fields, changing exit codes, changing default behavior.

Human-readable default output is not a contract — it can change freely.

When in doubt, add alongside — never modify. Deprecate with stderr warnings before removing.

---

## Noun-verb architecture

Structure commands as `cli <resource> <action>`: `mycli config set`, `mycli issue create`, `mycli cluster delete`. Global flags apply across subcommands. Predictability lets users guess future commands from existing patterns.

Anti-pattern: flag-heavy single commands like `tool --action=list --resource=plugins`. These fight the shell, prevent composition, and collapse as soon as two resources share a verb.

In Go, `github.com/spf13/cobra` implements this natively. Each command is a `*cobra.Command` with `Use`, `Short`, `Long`, `RunE`. Persistent flags on the root command apply everywhere.

Keep handlers pure: the business logic returns data, it does not print. The CLI adapter (typically in `cmd/mycli/`) parses args, calls the handler, picks the formatter, writes to the correct stream, sets the exit code. Handlers do not call `fmt.Println`, do not know about JSON vs text, do not call `os.Exit`.

This separation pays off concretely: handlers become testable without subprocess spawning, the same logic can back an HTTP server or MCP adapter, and format changes touch one file.

---

## Input design

Flags over positional arguments. One positional arg is fine (the "main thing"). Two is suspicious — prefer `--from` and `--to` over ordered positionals. Three or more positionals is never right.

`mycli copy myapp backup` is ambiguous. `mycli copy --from myapp --to backup` is self-documenting and order-independent.

Standard flags, with long form always available:

- `-h` / `--help` — show help, and only show help
- `--version` — print version to stdout
- `-q` / `--quiet` — suppress non-essential output
- `-v` / `--verbose` — more detail in human output
- `-d` / `--debug` — diagnostic output to stderr
- `-f` / `--force` — skip confirmation prompts
- `-n` / `--dry-run` — preview what would happen
- `--json` / `--plain` — machine-readable output modes
- `--no-color` / `--no-input` — disable color / disable all prompts
- `-o` / `--output` — output file
- `--fields` — select columns (critical for agent efficiency on large output)

Conventions:

- Accept `--flag=value` and `--flag value` equivalently
- `--` stops flag parsing: `mycli exec -- --flag-for-child`
- `-` means stdin or stdout: `cat data | mycli process -`
- If stdin is expected but connected to an interactive terminal, show help immediately — do not block waiting for input

Every prompt must be bypassable for scriptability:

- Confirmation → `--yes` or `--force`
- Selection → `--type=value`
- Text input → `--name=value`
- Passwords → `--password-file` or stdin

Secrets never via flag values. Flag values leak to `ps` output and shell history. Accept secrets through env vars, files, or stdin only.

Go: `github.com/spf13/pflag` (which Cobra uses) handles POSIX/GNU flag conventions including `--` and `=` syntax.

---

## Error design

Every error carries: a machine-readable code, a human message, a fix suggestion, and a transient flag.

In Go:

```go
type CLIError struct {
    Code      string // UPPER_SNAKE_CASE, e.g. "CONFIG_MISSING"
    Message   string // what went wrong, in human terms
    Fix       string // what the user should do
    Transient bool   // retrying might succeed
}
```

Human mode puts the most important information last — the eye lands at the end:

```
Error: CONFIG_MISSING — No config file found at ./mycli.yaml
Fix: Run `mycli init` to create a default config
```

JSON mode formats errors with the same structure:

```json
{"ok": false, "error": {"code": "CONFIG_MISSING", "message": "No config file found", "fix": "Run `mycli init`", "transient": false}}
```

Exit code 75 mirrors `transient: true` for non-JSON consumers that drive retries from exit codes.

Suggest corrections for typos where the set is small: `Did you mean 'deploy'?`. Group similar errors under one header — repeating 50 near-identical lines buries the signal. Write debug logs to a file by default, not to the terminal.

Anti-pattern: generic errors like `Operation failed` with no code, no reason, no action.

---

## Config precedence

Highest priority wins:

1. Flags — per-invocation override
2. Environment variables — `MYCLI_*` prefix, per-session
3. Project config — `./mycli.yaml`, `./.myclirc`, or embedded in `package.json`-equivalent
4. User config — `$XDG_CONFIG_HOME/mycli/` (fallback to `~/.config/mycli/`)
5. Built-in defaults

Follow the XDG Base Directory Specification for user config location. Env var naming: tool prefix, uppercase, underscore-separated (`MYCLI_THRESHOLD`, `MYCLI_API_URL`).

Never accept secrets via flags. Env vars, files, or stdin only.

Go: `github.com/spf13/viper` combined with Cobra implements this precedence. `github.com/adrg/xdg` provides XDG path helpers.

If the tool modifies configuration that belongs to another program, ask consent first.

---

## Composability patterns

Design for real-world pipes. A well-behaved CLI chains cleanly:

- Filter structured output: `mycli list --json | jq '.data[] | select(.status == "failed")'`
- Stream large datasets: `mycli run --format ndjson | while read -r line; do echo "$line" | jq '.file'; done`
- Feed stdin: `cat previous.json | mycli report -`
- Chain identifiers: `mycli create --json | jq -r '.data.id' | xargs mycli deploy --id`
- Parallel processing: `mycli list --json --fields id | jq -r '.data[].id' | xargs -P4 mycli process --id`
- CI exit-code-only: `mycli check --quiet || echo "Check failed"`
- Structured dry-run: `mycli apply --dry-run --json` outputs planned changes as data

Key patterns:

- `create` commands output the new identifier so the next command can consume it
- `list` commands support `--fields` for column selection — reduces output size, critical when an agent reads the response
- NDJSON avoids buffering the whole result in memory
- `--dry-run` paired with `--json` makes planned changes inspectable

---

## Anti-patterns

- Mixing data and diagnostics on stdout — breaks every pipe the user ever builds
- ANSI escape codes in piped output — check `isatty(stdout)` and `NO_COLOR`
- Interactive prompts with no flag bypass — agents and scripts cannot type 'y', and non-TTY without bypass hangs
- Printing nothing on success — silence is ambiguous; show brief confirmation, offer `-q` for scripts
- Designing for humans OR machines, not both — detect context, adapt automatically
- Output that does not guide the next action — every output is a signpost: success points to the next command, failure points to the fix
- Breaking existing CLI contracts — flag names, exit codes, JSON fields are promises
- Handlers that write directly to stdout/stderr or call `os.Exit` — let the adapter decide
- Non-zero exit without stderr explanation — scripts need both the code and the reason
- Verbose default output — a single run can easily produce hundreds of KB; support `--fields`, `--quiet`, `--json`
- Assuming required tools are installed — check and fail with a helpful message
- Inconsistent terminology across commands — same flag name for the same concept everywhere

---

## Verification checklist

After designing or reviewing a CLI:

- stdout has ONLY data; stderr has everything else
- Every command supports `--json` with the consistent envelope
- Exit codes are semantic and documented in `--help`
- Every prompt has a `--yes` / `--force` / flag bypass
- Errors include code, message, fix suggestion, and transient flag
- `--dry-run` available for mutating commands
- Progress and spinners go to stderr, never stdout
- `NO_COLOR`, `TERM=dumb`, and `--no-color` are all respected
- Piped output contains zero ANSI escape codes
- Success output includes next-action guidance
- Existing flags, exit codes, JSON fields never removed or renamed — only added
- JSON schema is versioned; additions safe, removals breaking
- Config follows flags > env > project > user > defaults
- Secrets accepted only via files / stdin / env, never flag values
- Startup under 500ms; something printed within 100ms of invocation
- Ctrl-C exits fast with bounded cleanup
- `--help` includes 2-3 realistic examples
- `--plain` output is grep-parseable (flat rows, no table borders)

---

## Load references on demand

Load the relevant file when the task matches.

- `references/long-running-operations.md` — concurrency and chunking, parallel processing patterns, rsync-style resume with checkpointing, signal handling (SIGINT / SIGTERM / SIGPIPE), crash-only design with atomic writes and stale lock recovery, state management with embedded SQLite. Load when the CLI runs for minutes to hours, streams large datasets, processes many items in parallel, or manages persistent state across invocations.
- `references/credentials-and-security.md` — OS keychain integration, short-lived session token patterns, secret input through stdin / files / env, authentication command design. Load when the CLI handles API tokens, logs users in, or otherwise touches secrets.
- `references/testing-cli.md` — subprocess integration tests that capture stdout / stderr / exit code, handler isolation with in-memory fakes, JSON contract tests that guard the schema, help text snapshots. Load when writing or reviewing tests for a CLI.
