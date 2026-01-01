# Nullables Skill Improvement Suggestions

Analysis based on:
- Skill creation best practices from `docs/knowledge/anthropic-skill-docs/`
- James Shore's original article and example repositories
- The existing `nullable_todo.md` suggestions

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

## Language Focus is JavaScript - Consider Noting Applicability

**Current:** All examples are JavaScript.

**Problem:** When Claude is working in Python, TypeScript, or Java, it should still apply this pattern.

**Note:** The embedded-stubs.md already has a Java example (Thin Wrapper Pattern).

- [ ] Add a brief note: "Examples use JavaScript. The pattern applies to any language - see embedded-stubs.md for Java example"
- [ ] Or: Add Python example in a reference file

