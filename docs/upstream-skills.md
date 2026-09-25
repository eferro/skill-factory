# Upstream Skills Registry

Skills in `output_skills/` that come from third-party repositories. Each one has
a `credits.md` with the full details (license, local changes). Use this table to
check upstream for changes: diff the upstream path from the recorded commit.

Mode: **verbatim** = imported as-is plus repo conventions (sync by re-copying);
**adapted** = rewritten or expanded (sync by reviewing upstream diffs manually).

| Local skill | Upstream repo | Upstream path | Commit | Imported | Mode |
|---|---|---|---|---|---|
| productivity/handoff | mattpocock/skills | skills/productivity/handoff | unknown (pre-registry) | 2026-09 | adapted |
| productivity/grilling | mattpocock/skills | skills/productivity/grilling | c55ee46 | 2026-09-25 | verbatim |
| productivity/grill-me | mattpocock/skills | skills/productivity/grill-me | c55ee46 | 2026-09-25 | verbatim |
| productivity/wait-what | mattpocock/skills | skills/productivity/wait-what | c55ee46 | 2026-09-25 | verbatim |
| design/domain-modeling | mattpocock/skills | skills/engineering/domain-modeling | c55ee46 | 2026-09-25 | verbatim |
| design/grill-with-docs | mattpocock/skills | skills/engineering/grill-with-docs | c55ee46 | 2026-09-25 | verbatim |
| design/prototype | mattpocock/skills | skills/engineering/prototype | c55ee46 | 2026-09-25 | verbatim |
| developer-tools/wizard | mattpocock/skills | skills/engineering/wizard | c55ee46 | 2026-09-25 | verbatim |

## Checking for upstream changes

```bash
git clone https://github.com/mattpocock/skills /tmp/mp-skills   # or git pull
git -C /tmp/mp-skills log --oneline <commit>..HEAD -- <upstream path>
git -C /tmp/mp-skills diff <commit>..HEAD -- <upstream path>
```

After syncing, update the commit column here and in the skill's `credits.md`.
