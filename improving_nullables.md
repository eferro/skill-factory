# Improving Nullables Skill

Analysis based on Anthropic's skill authoring best practices.

## Summary

The nullables skill is well-structured with good progressive disclosure. Main SKILL.md is 272 lines (well under 500 limit) with 8 reference files. The content is comprehensive and technically sound.

## Issues

### 2. No STARTER_CHARACTER

Other skills (tdd, refactoring) use visual indicators like 🔴🌱🌀 or 🟣. This skill lacks one, making it inconsistent with the skill family.

### 3. Missing Workflow/Steps Section

The TDD skill has clear phases: "Test Planning → Implementation Phase → Final Evaluation". Nullables is more reference-style without a clear "how to build your first Nullable" workflow.

Users would benefit from:
```
## Building a Nullable (Quick Start)
1. Identify the infrastructure dependency
2. Create wrapper class with `create()` and `createNull()` factory methods
3. Add OutputListener for tracking
4. Write the embedded stub
5. Test the wrapper
```

### 4. JavaScript-Only Examples in Main File

All SKILL.md examples are JavaScript. Java appears only in embedded-stubs.md reference. No Python examples anywhere.

Given Python's popularity for testing, this is a gap.

### 5. Redundant Reference Links

References are listed twice:
- "Three Supporting Patterns" section (lines 165-215) with brief examples
- "Reference Files" section (lines 257-271) as a flat list

This creates confusion about which path to follow.

### 6. A-Frame Architecture Fragmented

A-Frame is explained in:
- SKILL.md (lines 23-52) - core concept
- logic-sandwich.md - detailed examples
- event-driven.md - Traffic Cop variation

The relationship between these isn't clear. User might read SKILL.md and not realize they need logic-sandwich.md for depth.

### 7. Anti-Patterns Section Too Brief

Current anti-patterns (lines 217-255) are useful but brief. Missing common pitfalls:
- Over-wrapping (wrapping things that don't need it)
- Stub scope creep (stub becomes as complex as real thing)
- Forgetting to test the wrapper itself
- Nulling at wrong abstraction level

### 8. Some Reference Files Are Long

| File | Lines | Notes |
|------|-------|-------|
| test-patterns.md | 331 | Could split "Testing Time" and "Testing Events" |
| embedded-stubs.md | 317 | Dense, many patterns |
| infrastructure-wrappers.md | 295 | Comprehensive but long |

These approach the "consider splitting" threshold.

### 9. Missing "When NOT to Use" for Supporting Patterns

Main Nullables section has clear "Do NOT use when" but the three supporting patterns (Output Tracking, Configurable Responses, Embedded Stubs) lack this guidance.

### 10. Jest-Specific Pattern in test-patterns.md

Line 322-330 mentions `expect.any(Number)` is Jest-specific. Good awareness, but the workaround shown is verbose. Could provide cleaner alternatives.

## Improvement Suggestions

### High Priority

1. **Enhance description** with trigger words (mocks, test doubles, infrastructure)
2. **Add quick-start workflow** section showing steps to build first Nullable
3. **Consolidate reference linking** - remove redundant "Reference Files" section, keep inline links in context

### Medium Priority

4. **Add STARTER_CHARACTER** for consistency (e.g., 🧪 or ⚡)
5. **Add Python examples** in main file or dedicated reference
6. **Expand anti-patterns** into a reference file with more comprehensive coverage
7. **Clarify A-Frame navigation** - better signposting between SKILL.md, logic-sandwich.md, and event-driven.md

### Lower Priority

8. **Consider splitting longest reference files** if they grow further
9. **Add "When NOT to use" to supporting patterns**
10. **Provide cleaner patterns for dynamic field assertion** across test frameworks

## Structural Recommendation

```
Current:
SKILL.md (272 lines)
├── references/
│   ├── infrastructure-wrappers.md (295 lines)
│   ├── output-tracking.md (215 lines)
│   ├── configurable-responses.md (258 lines)
│   ├── embedded-stubs.md (317 lines)
│   ├── test-patterns.md (331 lines)
│   ├── logic-sandwich.md (110 lines)
│   ├── event-driven.md (112 lines)
│   └── migration.md (158 lines)

Suggested restructure:
SKILL.md
├── references/
│   ├── architecture/
│   │   ├── a-frame.md (merge logic-sandwich + event-driven concepts)
│   │   └── logic-sandwich.md (examples only)
│   ├── building/
│   │   ├── infrastructure-wrappers.md
│   │   ├── output-tracking.md
│   │   ├── configurable-responses.md
│   │   └── embedded-stubs.md
│   ├── testing/
│   │   ├── test-patterns.md
│   │   └── time-and-events.md (split from test-patterns)
│   └── migration.md
```

This makes the reference hierarchy clearer and keeps related content together.
