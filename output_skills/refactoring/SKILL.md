---
name: refactoring
description: Refactoring process. Invoke immediately when user or document mentions refactoring, or proactively when code shows the first signs of becoming too complex or messy.
---

# Refactoring Production Code

STARTER_CHARACTER = 🟣

When starting, announce: "🟣 Using REFACTORING skill".

Work autonomously as much as possible. Start with the simplest thing or file and proceed to the more complex ones.

## Stages

1. Prep
2. Main Refactoring
3. Final Evaluation
4. Cleanup
5. Summary

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

### Refactoring Process
Follow this process for each refactoring:
1. Ensure all tests pass
2. Choose and perform the simplest possible refactoring (one at a time)
3. Ensure all tests pass after the change
4. Commit each successful refactor with the message format: "- r <refactoring>" (the message must include the "- r" prefix)
   Prefer small granular commits. If applying the same refactoring pattern to multiple locations, change one location at a time and commit each separately.
5. Provide a status update after each refactor

If a refactor fails three times or no further refactoring is found, pause and check with the user.

## 3. Final Evaluation

When you see no more obvious refactoring opportunities, say "🔍 Entering final evaluation".

Carefully look at existing code and think about the problem space:
- What is the purpose of the code? Express it as both fully and succinctly as possible, say "CODE PURPOSE: [your summary]"
- Does the actual code express that purpose in a way that is clear to see and understand for the reader?
- Look for opportunities to use domain language over implementation details in both explanations and names. Express what things ARE and why they exist, instead of how they're implemented.
- Think about applying this on different layers of abstraction: the whole file, methods, or parts of methods
- Look for methods where levels of abstraction are mixed: too much detail vs more abstract blocks that express the meaning. Can you see an opportunity to raise the level of abstraction in the more detailed sections?
- Think about the list of refactorings that you could implement to make the code better from that perspective
- If you identified improvements, follow the same refactoring process to implement them, be sure to commit and run tests as before, performing simplest refactoring first.

## 4. Cleanup

After all refactoring is complete, check for any backward-compatibility artifacts that were left behind to avoid breaking tests (aliases, re-exports, old function names kept alongside new ones).

If any exist:
- List them clearly
- Ask the user: "Should I update tests to use the new names and remove the compatibility aliases?"
- Only proceed with user approval
- Run tests after making changes to verify nothing broke

## 5. Summary

Provide a high-level summary of the refactoring:
- List each file that was touched
- Describe the key improvements made in each file

## Language-Specific

For Java: See [references/java.md](references/java.md)
