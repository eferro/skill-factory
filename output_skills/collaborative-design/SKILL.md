---
name: collaborative-design
description: Designs software features collaboratively through scenarios, ASCII mockups, and iterative refinement. Use when designing features, tools, UIs, workflows, or any system before implementation.
---

STARTER_CHARACTER = 🎨

## Purpose

Stay in design mode. Resist jumping to implementation. Explore the problem space through concrete scenarios and visual mockups before committing to solutions.

## Process

```
Problem → Research → Scenarios → Mockups → Decisions → Validation
    ↑_______________________________________________|
              (iterate freely)
```

### 1. Clarify the Problem
- What are we building? Why?
- What does success look like?
- What constraints exist?

### 2. Research (if needed)
- Analyze existing patterns (logs, code, APIs)
- Check real-world examples
- Validate assumptions about formats, timing, etc.

### 3. Explore Through Scenarios
Walk through concrete user stories:
- "User opens the tool and sees..."
- "User types X, then Y happens..."
- "What if the user does Z?"

Ask about edge cases as they emerge.

### 4. Mockup Early
Use ASCII diagrams liberally:

**Flows:**
```
Input → Process → Output
          ↓
       Side effect
```

**UI/TUI:**
```
┌─────────────────────┐
│ Title               │
├─────────────────────┤
│ [x] Option A        │
│ [ ] Option B        │
│ > input: ____       │
└─────────────────────┘
```

**Data:**
```
config.toml:
[section]
key = "value"
```

### 5. Surface Options, Then Decide
Present 2-4 options with tradeoffs. Don't decide alone - discuss:
- "Option A does X, Option B does Y. Which direction?"
- Wait for input before proceeding

### 6. Validate Before Building
- POC for risky assumptions (API timing, format parsing)
- Test cases in plain English before code
- Document findings

### 7. Document Decisions
Track what was decided and why. Update docs as design evolves.

## Anti-patterns

- Jumping to code before exploring the design space
- Showing one solution instead of options
- Asking multiple questions at once (show the whole list, then ask each question one at a time)
- Making assumptions without checking (real data, real APIs)
- Skipping mockups for "obvious" UIs
- Deciding without discussing tradeoffs

## When to Exit Design Mode

- Problem is understood
- Key scenarios are walked through
- Major decisions are made and documented
- Test cases exist (in English)
- Risky assumptions are validated

Then: implementation.
