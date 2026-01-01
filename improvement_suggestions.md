# Nullables Skill Improvement Suggestions

Analysis based on:
- Skill creation best practices from `docs/knowledge/anthropic-skill-docs/`
- James Shore's original article and example repositories
- The existing `nullable_todo.md` suggestions

---

## Reference Navigation Could Be Clearer

**Current:** The "Reference Files" section lists files with descriptions.

**For Claude:** When encountering edge cases (event-driven code, migration from mocks), Claude needs to know which reference to consult.

- [ ] Consider grouping references by use case: "For event-driven code, see event-driven.md" rather than listing all files equally

---

## Missing Key Terminology from Shore's Pattern Language

Shore's article defines specific terms that the skill sometimes uses different names for:

| Shore's Term | Current Skill | Status |
|--------------|--------------|--------|
| Narrow Tests | (implied) | Missing explicit mention |
| State-Based Tests | Mentioned in anti-patterns | Could be more prominent |
| Overlapping Sociable Tests | test-patterns.md | Consider adding to SKILL.md |
| Signature Shielding | test-patterns.md | Good, keep there |
| Zero-Impact Instantiation | "Constructor does work" anti-pattern | Same concept, different name |
| Parameterless Instantiation | infrastructure-wrappers.md | Good |
| Narrow Integration Tests | test-patterns.md | Good |
| Behavior Simulation | event-driven.md as `simulateX()` | Good |

- [ ] Consider adding a terminology box linking to Shore's pattern language
- [ ] Or: Add brief definitions for "narrow tests" and "state-based tests" since these are foundational

---

## Examples Follow "Good Example" Pattern - Consider Anti-Examples

Best practices: *"Use principles + anti-examples, not good examples to copy (avoids collapsing solution space)"*

**Current:** The skill uses good examples heavily.

**Observation:** The anti-patterns section already does this well. But the main examples could benefit from brief "don't do this" contrasts inline.

- [ ] The existing BAD/GOOD patterns in anti-patterns are good
- [ ] Consider adding brief anti-examples to the Core Pattern section showing what NOT to do in `createNull()`

---

## Language Focus is JavaScript - Consider Noting Applicability

**Current:** All examples are JavaScript.

**Problem:** When Claude is working in Python, TypeScript, or Java, it should still apply this pattern.

**Note:** The embedded-stubs.md already has a Java example (Thin Wrapper Pattern).

- [ ] Add a brief note: "Examples use JavaScript. The pattern applies to any language - see embedded-stubs.md for Java example"
- [ ] Or: Add Python example in a reference file

---

## Structural Recommendation: Proposed Reordering

Current order front-loads architecture (A-Frame) before the actionable pattern.

Suggested flow:
```
1. Core Insight (2 lines) - "production code with an off switch"
2. When to Use / When NOT to Use
3. Core Pattern: Two Factory Methods
4. Testing with Nullables (brief example)
5. Three Supporting Patterns (brief with links)
6. A-Frame Architecture (condensed, or moved to reference)
7. Anti-Patterns
8. Reference Navigation
```

---

## Summary: Priority Order

**Medium (polish):**
- [ ] Add tradeoffs discussion (so Claude knows when NOT to suggest Nullables)

**Low (nice to have):**
- [ ] Note cross-language applicability
