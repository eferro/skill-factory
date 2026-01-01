---
name: ai-patterns
description: Reference patterns for augmented coding with AI. Use when discussing AI coding patterns, anti-patterns, obstacles, context management, steering AI, or looking up Lexler's patterns collection.
---

# AI Patterns Reference

Patterns collection by Lexler (Lada Kesseler) and contributors for effective AI-augmented software development.

## Setup

First, pull latest:
```bash
cd /Users/ladak/workspace/knowledge/references-for-skills/ai-patterns-lexler/augmented-coding-patterns && git pull
```

## Content Location

All documents: `/Users/ladak/workspace/knowledge/references-for-skills/ai-patterns-lexler/augmented-coding-patterns/documents/`

## Structure

### Patterns (43)
Solutions to common AI coding problems.

Location: `documents/patterns/`

Key patterns by category:

**Context Management:**
- `context-management.md` - Core pattern for managing AI context
- `knowledge-document.md` - Structuring knowledge for AI
- `ground-rules.md` - Setting behavioral rules
- `focused-agent.md` - Keeping agents on task
- `semantic-zoom.md` - Controlling detail level

**Reliability:**
- `chain-of-small-steps.md` - Breaking down complex work
- `playgrounds.md` - Exploratory/throwaway code
- `offload-deterministic.md` - When to use scripts vs AI
- `hooks.md` - Forcing compliance via automation
- `reminders.md` - Reinforcing instructions

**Steering:**
- `active-partner.md` - AI pushback and honest dialogue
- `check-alignment.md` - Verifying AI understanding
- `reverse-direction.md` - Having AI lead
- `text-native.md` - ASCII diagrams, text-first

### Anti-patterns (9)
Common mistakes to avoid.

Location: `documents/anti-patterns/`

- `silent-misalignment.md` - AI appears to agree but doesn't
- `answer-injection.md` - Leading AI to wrong conclusions
- `tell-me-a-lie.md` - AI fabricating to please
- `distracted-agent.md` - Overloaded context
- `unvalidated-leaps.md` - Skipping verification steps

### Obstacles (14)
Inherent AI limitations to work around.

Location: `documents/obstacles/`

- `context-rot.md` - Instructions fade over conversation
- `limited-focus.md` - Can't attend to everything
- `hallucinations.md` - Fabricated information
- `compliance-bias.md` - Tendency to agree
- `non-determinism.md` - Inconsistent outputs

## Quick Reference

List all patterns:
```bash
ls /Users/ladak/workspace/knowledge/references-for-skills/ai-patterns-lexler/augmented-coding-patterns/documents/patterns/
```

Read a specific pattern:
```bash
cat /Users/ladak/workspace/knowledge/references-for-skills/ai-patterns-lexler/augmented-coding-patterns/documents/patterns/<pattern-name>.md
```

## Learning Path

See `documents/workshop_path.md` for structured progression through patterns.

## Online

View at: https://lexler.github.io/augmented-coding-patterns/
