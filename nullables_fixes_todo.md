# Nullables Skill: Issues and Improvements

This document identifies issues and potential improvements in the current Nullables skill implementation, compared against the source material (James Shore's article, example repos) and Anthropic's skill best practices.

---

## Critical Issues

### Description Field
- [ ] **Description uses first-person implied** - "Implements James Shore's Nullables" sounds like the skill itself implements it, not that it helps Claude implement it. Reword to: "Helps write tests without mocks using James Shore's Nullables pattern. Use when..."
- [ ] **Trigger words feel like a list** - The "or when user mentions..." clause reads like meta-documentation, not natural description. Integrate trigger words more naturally.

### Missing Core Concepts from Source Material
- [ ] **A-Frame Architecture not covered** - This is a foundational concept from the article that shapes how applications should be structured for testability. Currently omitted entirely.
- [ ] **Logic Sandwich pattern missing** - Critical pattern for structuring Application layer code: read → process → write. Not mentioned anywhere.
- [ ] **Traffic Cop pattern missing** - Observer pattern variant for event-driven apps. Essential for async/event-based code.
- [ ] **Sociable Tests not explained** - The article's core testing philosophy. Tests use real dependencies (sociable), only infrastructure is nulled.
- [ ] **Overlapping Sociable Tests missing** - Key concept: tests naturally overlap, catching breaking changes in dependency chains.
- [ ] **Narrow Integration Tests buried** - Should be more prominent in test-patterns.md. These verify wrappers work with real systems.
- [ ] **Parameterless Instantiation incomplete** - Only shown in infrastructure-wrappers.md, not in SKILL.md as a core principle.
- [ ] **Signature Shielding term missing** - test-patterns.md shows "Helper Functions" but doesn't use Shore's terminology "Signature Shielding".
- [ ] **Behavior Simulation incomplete** - Only mentioned briefly. Should explain `simulateX()` methods pattern for event-driven testing.

### Missing Anti-Patterns
- [ ] **Broad end-to-end tests** - Article explicitly warns against these; skill doesn't mention this anti-pattern.
- [ ] **Using mock libraries** - The whole point is to avoid these, but skill doesn't explicitly say "don't import sinon/jest mocks".
- [ ] **God Classes in Traffic Cop** - Common mistake when implementing Traffic Cop pattern.
- [ ] **Overly complex Embedded Stubs** - Article warns to test-drive stubs through wrapper's public interface.
- [ ] **Testing irrelevant implementation details** - Beyond just "interactions vs outcomes".

---

## Structure and Organization Issues

### SKILL.md
- [ ] **Inline EventEmitter vs OutputListener inconsistency** - SKILL.md line 74-95 shows inline `EventEmitter` implementation, but source repos use a dedicated `OutputListener` utility class. This creates inconsistency with references.
- [ ] **"When to Use" section could be decision tree** - Would be clearer as a flowchart or structured decision guide.
- [ ] **References section at end is flat list** - Could be organized by use case: "Building wrappers → infrastructure-wrappers.md", "Testing patterns → test-patterns.md", etc.

### Reference Files Organization
- [ ] **Missing TOC in reference files** - Per best-practices.md, files over 100 lines should have table of contents. Most references don't have one.
- [ ] **output-tracking.md shows custom OutputTracker** - But source repos have reusable `OutputListener` class. Skill should match source pattern.
- [ ] **configurable-responses.md missing `mapObject` use case** - The source shows `ConfigurableResponses.mapObject()` for HTTP endpoints. Skill mentions it but example is weak.

---

## Technical Issues

### Code Example Issues
- [ ] **Date in Clock example is 2024** - Line 33: `"2024-01-15T10:30:00Z"`. Per best-practices, avoid time-sensitive info. Use placeholder like `"2020-01-01T00:00:00Z"` or comment it's just an example.
- [ ] **StubbedDate implementation differs from source** - Source uses different internal structure. Current example works but could be closer to canonical.
- [ ] **Missing `ensure.signature` pattern from source** - Source repos validate arguments. Skill examples don't show this (though it's optional).
- [ ] **Error messages differ from source** - Source: `"No more responses configured in ${name}"`. Skill: `"No more configured responses"`.

### Pattern Completeness
- [ ] **ConfigurableResponses.create vs new** - Skill shows both `new` and factory method inconsistently. Source always uses factory.
- [ ] **OutputTracker.clear() return value** - Source returns cleared data on `clear()`. Skill version doesn't.
- [ ] **Missing OutputListener.create() factory** - Source has factory method, skill shows `new EventEmitter()` directly.

---

## Content Quality Issues

### Verbosity vs Conciseness
- [ ] **infrastructure-wrappers.md intro could be shorter** - "Infrastructure wrappers isolate external systems behind clean interfaces" is good, but following sentence is redundant.
- [ ] **test-patterns.md "Core Structure" section** - Arrange-Act-Assert is well-known. Could be even more concise.

### Missing Practical Guidance
- [ ] **When NOT to create a wrapper** - Article says "If the external system is simple enough to use directly in tests". Skill lacks concrete examples.
- [ ] **How to identify infrastructure boundaries** - What counts as "infrastructure"? File system? Database? HTTP? Clock? All yes, but skill doesn't explain the principle.
- [ ] **Migration strategy for existing code** - Article has "Descend the Ladder" and "Climb the Ladder" patterns. Completely missing.
- [ ] **"Paranoic Telemetry"** - Article's term for instrumenting code assuming external systems will fail. Not covered.

### Examples Gap
- [ ] **No TypeScript examples** - todo_nullables.md mentions this as future work. TypeScript users would benefit from type annotations.
- [ ] **No Python examples** - Many users work in Python. Pattern applies but syntax differs.
- [ ] **No Java examples in SKILL.md** - Only in embedded-stubs.md. Java users need to see the "thin wrapper" interface pattern upfront.

---

## Triggering and Discovery Issues

- [ ] **Description doesn't mention "infrastructure isolation"** - Common phrase users might say.
- [ ] **Missing "testable design" trigger** - Users asking about making code testable should find this skill.
- [ ] **Missing "dependency injection alternative"** - Article explicitly positions Nullables as alternative to DI frameworks.
- [ ] **"fake" not mentioned** - Users might say "fakes" instead of "stubs".

---

## Alignment with Source Material

### From James Shore Article (not in skill)
- [ ] **"Easily-Visible Behavior" pattern** - Prefer pure functions and immutable objects; provide getters/events for mutable state.
- [ ] **"Testable Libraries" pattern** - Wrap third-party code to match your application's needs.
- [ ] **"Collaborator-Based Isolation"** - Use dependencies to define test expectations, reducing brittleness.

### From Example Repos (not matched)
- [ ] **OutputListener class structure** - Repos have reusable utility; skill reinvents inline.
- [ ] **ensure.js/type.js pattern** - Source validates arguments. Skill doesn't mention this discipline.
- [ ] **File naming convention** - Source uses `_*_test.js` prefix. Could mention testing file conventions.

---

## Best Practices Checklist Gaps

Per `best-practices.md`, checking:

- [x] Description is specific and includes key terms
- [x] Description includes what the skill does and when to use it
- [x] SKILL.md body is under 500 lines (240 lines ✓)
- [x] Additional details are in separate files
- [ ] **No time-sensitive information** - 2024 date in example
- [x] Consistent terminology throughout (mostly)
- [x] Examples are concrete, not abstract
- [x] File references are one level deep
- [x] Progressive disclosure used appropriately
- [ ] **Workflows could have clearer steps** - No numbered workflow in SKILL.md itself
- [x] Scripts solve problems rather than punt (N/A - no scripts)
- [ ] **At least three evaluations created** - todo_nullables.md doesn't show actual eval scenarios
- [ ] **Tested with Haiku, Sonnet, and Opus** - Not mentioned/documented

---

## Terminology Consistency Issues

- [ ] **"Nullables" vs "Nullable"** - Used interchangeably. Pick one and stick to it.
- [ ] **"embedded stub" vs "Embedded Stub"** - Capitalization inconsistent.
- [ ] **"configurable responses" vs "Configurable Responses"** - Same issue.
- [ ] **"output tracking" vs "Output Tracking"** - Same issue.

---

## Minor Polish

- [ ] **SKILL.md line 137** - "Notice:" should be **Notice:** or removed (the bold already draws attention).
- [ ] **References section heading** - "Reference Files" is flat. Could be "Deep Dives" or "Detailed Patterns".
- [ ] **ASCII diagram in infrastructure-wrappers.md** - Good! But SKILL.md could also have a high-level visual.
- [ ] **test-patterns.md assertions section** - Shows `expect.any(Number)` which is Jest-specific. Skill should note this or use portable assertions.

---

## Summary: Top 10 High-Priority Fixes

1. [ ] Add A-Frame Architecture explanation (new reference file or section)
2. [ ] Add Logic Sandwich and Traffic Cop patterns
3. [ ] Explain "Sociable Tests" concept explicitly in SKILL.md
4. [ ] Fix inconsistency: use OutputListener utility pattern from source, not inline EventEmitter
5. [ ] Add missing anti-patterns (broad tests, mock libraries, God Classes)
6. [ ] Add TOC to reference files over 100 lines
7. [ ] Add migration patterns (Descend/Climb the Ladder)
8. [ ] Update date in example to avoid time-sensitivity
9. [ ] Add more trigger words to description (infrastructure isolation, testable design, DI alternative)
10. [ ] Create actual test evaluations to verify skill effectiveness

---

## Sources Referenced

| Resource | Issues Found From |
|----------|------------------|
| James Shore article | Missing concepts, anti-patterns, patterns |
| Simple example repo | OutputListener utility pattern |
| Complex example repo | ConfigurableResponses patterns, higher-level Nullables |
| best-practices.md | Time-sensitivity, TOC, evaluations, terminology |
| skills.md | Description format, trigger words |
| overview.md | Progressive disclosure principles |
| create_new_skill-process.md | Review checklist |
