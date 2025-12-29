# Create New Skill

STARTER_CHARACTER = 🎯

## Description

Create a Claude Code skill that works effectively. Skills teach Claude domain-specific expertise that triggers automatically when relevant.

## Steps

### 1. Learn Skill Patterns
Read the official documentation in `docs/knowledge/anthropic-skill-docs/`:
- `overview.md` - Core concepts and architecture
- `skills.md` - Implementation patterns
- `best-practices.md` - Guidelines and pitfalls

### 2. Clarify the Goal
Ask the user:
- What specific task should Claude be able to do?
- When should this skill trigger? (What phrases would a user say?)
- What does Claude NOT already know that this skill needs to provide?
- Do you have examples that should be included as reference material?

### 3. Research (if needed)
If the domain is unfamiliar:
- Gather domain knowledge first
- Identify patterns, terminology, and common workflows

### 4. Design Structure

**Skill anatomy:**
```
skill-name/
├── SKILL.md (required)
├── scripts/      - Executable code for deterministic operations
├── references/   - Detailed docs, examples, loaded as needed
└── assets/       - Templates, images used in output
```

Decide scope:
- **Single file**: Simple guidance, under 500 lines
- **Multi-file**: Complex domain with reference materials or scripts

**Do NOT include:** README.md, CHANGELOG.md, INSTALLATION_GUIDE.md, or other auxiliary documentation.

### 5. Write SKILL.md

**Frontmatter:**
```yaml
---
name: doing-the-thing
description: [What it does]. Use when [trigger phrases user would say].
---
```
- Name: lowercase, hyphens, gerund form preferred
- Description: Third person, specific, includes trigger words. This is the primary triggering mechanism.

**Body:**
- Concise instructions. Assume Claude is smart.
- Use principles + anti-examples, not good examples to copy (avoids collapsing solution space)
- Anti-example: "Avoid vague names like `helper`, `utils`" is better than listing good names

### 6. Add Supporting Files (if multi-file)

**References:** Detailed docs, loaded only when needed. Keep SKILL.md lean.

**Examples in references:** When including examples, add framing:
> "These illustrate the principle. Consider what fits your context."

**Scripts:** For operations that need deterministic reliability.

Keep references one level deep from SKILL.md.

### 7. Review Against Best Practices
Re-read `docs/knowledge/anthropic-skill-docs/best-practices.md` and `skills.md` (troubleshooting section). Compare to what you created:
- Does the description include clear trigger words?
- Is the body concise? Remove anything Claude already knows.
- Are references one level deep?
- Any anti-patterns present?

Suggest improvements before proceeding.

### 8. Test
- Ask Claude to do a task that should trigger the skill
- Verify: Does it trigger? Does Claude follow instructions correctly?
- Try edge cases

### 9. Iterate
- Skill doesn't trigger → improve description with better trigger words
- Claude misses steps → make instructions more prominent
- Too verbose → remove what Claude already knows

## Output
Save completed skill to: `output_skills/[skill-name]/SKILL.md`
