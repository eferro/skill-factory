# Upstream Skills Registry

Every skill in `output_skills/` whose content comes from a third party. Each one
has a `credits.md` (or, for herdr, an attribution line in `SKILL.md` too) with
the full details: license and local changes.

## Synced skills

Imported from a third-party skills repository and trackable against it: diff the
upstream path from the recorded commit.

Mode: **verbatim** = imported as-is plus repo conventions (sync by re-copying);
**adapted** = rewritten or expanded (sync by reviewing upstream diffs manually).

| Local skill | Upstream repo | Upstream path | Commit | Imported | Mode | License |
|---|---|---|---|---|---|---|
| productivity/grilling | mattpocock/skills | skills/productivity/grilling | c55ee46 | 2026-09-25 | verbatim | MIT |
| productivity/grill-me | mattpocock/skills | skills/productivity/grill-me | c55ee46 | 2026-09-25 | verbatim | MIT |
| productivity/wait-what | mattpocock/skills | skills/productivity/wait-what | c55ee46 | 2026-09-25 | verbatim | MIT |
| productivity/handoff | mattpocock/skills | skills/productivity/handoff | unknown (pre-registry) | 2026-08-11 | adapted | MIT |
| design/domain-modeling | mattpocock/skills | skills/engineering/domain-modeling | c55ee46 | 2026-09-25 | verbatim | MIT |
| design/grill-with-docs | mattpocock/skills | skills/engineering/grill-with-docs | c55ee46 | 2026-09-25 | verbatim | MIT |
| design/prototype | mattpocock/skills | skills/engineering/prototype | c55ee46 | 2026-09-25 | verbatim | MIT |
| developer-tools/wizard | mattpocock/skills | skills/engineering/wizard | c55ee46 | 2026-09-25 | verbatim | MIT |
| developer-tools/herdr | ogulcancelik/herdr | SKILL.md (now skills/herdr/SKILL.md) | 0f161fa | 2026-07-29 | verbatim | Apache-2.0 |

### Checking for upstream changes

```bash
git clone https://github.com/<upstream repo> /tmp/upstream   # or git pull
git -C /tmp/upstream log --oneline <commit>..HEAD -- <upstream path>
git -C /tmp/upstream diff <commit>..HEAD -- <upstream path>
```

After syncing, update the commit column here and in the skill's `credits.md`.

## Derived skills

Written in this repo from a third-party article, process file, gist, or
methodology. There is no upstream skill to sync; see each `credits.md`.

| Local skill | Source | Created |
|---|---|---|
| strategy/llm-council | Ole Lehmann's skill (via Charlie J. Hills), on Karpathy's LLM Council | 2026-04-29 |
| practices/refactoring | LearnWithLlew/AgenticAi.Java.StarterProject process file | 2026-02-01 |
| ai/creating-process-files | LearnWithLlew/AgenticAi.Java.StarterProject processes | 2026-02-01 |
| design/event-modeling | dilgerma/spring-petclinic-kotlin `Claude.md` | 2026-02-01 |
| practices/capturing-project-knowledge | Emilio Carrión gist | 2026-07-14 |
| testing/nullables | James Shore, "Testing Without Mocks" | 2026-02-01 |
