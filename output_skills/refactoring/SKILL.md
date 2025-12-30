---
name: refactoring
description: Refactoring process. Invoke immediately when user or document mentions refactoring, or proactively when code gets too complex or messy.
---

# Refactoring Production Code

STARTER_CHARACTER = 🟣

When starting, announce: "🟣 Using REFACTORING skill".

Work autonomously as much as possible. Start with the simplest thing or file and proceed to the more complex ones.

## Stages

1. Prep
2. Main Refactoring
3. Final Evaluation
4. Summary

## Test Code Policy

Do not change test code during refactoring, except:
- Renames that follow production code renames (imports, function calls)
- Import path updates if something moved

Never change test assertions, test data, or test logic.

## 1. Prep

- Determine scope: use specified files, or identify related files (imports, shared functionality), or ask user
- Add files in scope to todo list
- Find or create ./test.sh, verify all tests pass
- Remove comments from files in scope (commit per file)

## 2. Main Refactoring

### Code Style

Write self-explanatory, readable code.

- Use functional helper methods for clarity
- Remove dead code
- Extract paragraphs into methods
- Use better variable names
- Remove unused imports
- Remove unhelpful local variables
- Look for opportunities to simplify
- Use domain language - name things for what they ARE, not how they're implemented
- Keep consistent abstraction levels within methods

### Refactoring Process

For each refactor:
1. Ensure all tests pass
2. Choose and perform the simplest possible refactoring (one at a time)
3. Ensure all tests pass after the change
4. Commit each successful refactor with the message format: "- r <refactoring>" (the message must include the "- r" prefix)
   Prefer small granular commits. If applying the same refactoring pattern to multiple locations, change one location at a time and commit each separately.
5. Provide a status update after each refactor

If a refactor fails three times or no further refactoring is found, pause and check with the user.

## 3. Final Evaluation

When you see no more obvious refactoring opportunities, say "🔍 Entering final evaluation".

Re-read Code Style guidelines. Look at the code again. If you see improvements, apply them using the same refactoring process.

## 4. Summary

Provide a high-level summary of the refactoring:
- List each file that was touched
- Describe the key improvements made in each file

## Language-Specific

For Java: See [references/java.md](references/java.md)
