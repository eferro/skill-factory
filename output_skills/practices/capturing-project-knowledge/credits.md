# Credits

Adapted from the **`compound`** skill by Emilio Carrión:
https://gist.github.com/EmilioCarrion/efdfa5487963651bf65fc491f30fbeb4

The original captures business rules, tacit knowledge, and code patterns into
project knowledge (a hierarchy of CLAUDE.md files, flows, and conventions).

## What changed in this adaptation

Generalized to work across projects and toolchains, keeping the original's
invariants intact:

- **Branch-agnostic**: the base branch is the repository's default branch
  (`git diff <base>...HEAD`) rather than a hardcoded `master`.
- **Tool-agnostic intent**: the motivating requirement can be any tracked ticket
  (Jira, Linear, GitHub/GitLab issue) or a written spec — not Jira specifically.
- **Optional PR/MR URLs**: arguments accept GitHub or GitLab pull/merge request
  URLs, with `gh pr diff` given as the GitHub example rather than the only path.
- **Adaptable layout**: the knowledge structure in KNOWLEDGE.md is the default,
  and the skill defers to a project's existing organization when one exists.
- Renamed from `compound` to `capturing-project-knowledge` for discovery clarity.

Preserved unchanged: read-knowledge-first, require the why before capturing,
no-duplication rule, ask-the-why via the user, feature-flag handling, convention
consistency check, correction of stale/contradictory knowledge, and the ban on
code identifiers in business rules, invariants, and ubiquitous language.
