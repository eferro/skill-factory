# Approval Tests Skill Improvement Plan

## Design Principles

**Focused Agent**: Narrow responsibility - teaching Claude to write approval tests.

**Progressive Disclosure**: Load knowledge only when needed:
- SKILL.md = universal concepts (loaded when skill triggers)
- Language hubs = language-specific overview + navigation
- Deep references = specialized topics (loaded on-demand)

**Separation of Concerns**: Languages differ - Python has SimpleLogger, Java has different utilities. Keep them separate.

---

## Target Structure

```
SKILL.md (universal: philosophy, workflow, when to use)
│
├── references/python.md (Python hub: quick start, imports, links deeper)
│   └── python/
│       ├── api.md (core verify functions)
│       ├── scrubbers.md (handling non-deterministic data)
│       ├── inline.md (inline approvals)
│       ├── logging.md (NEW: SimpleLogger, verify_logging)
│       └── advanced.md (NEW: multi-approval, config)
│
├── references/nodejs.md (Node.js hub)
│   └── nodejs/
│       ├── api.md
│       ├── scrubbers.md
│       └── inline.md
│
├── references/java.md (Java hub)
│   └── java/
│       ├── api.md
│       ├── scrubbers.md
│       └── inline.md
│
└── references/patterns/ (cross-language patterns)
    ├── combinations.md
    └── testing-patterns.md
```

---

## SKILL.md Changes

### Make Language-Agnostic
- [ ] Remove language-specific quick start code (move to language hubs)
- [ ] Keep: philosophy, core workflow, when to use, anti-patterns
- [ ] Replace "Language Detection" section with links to language hubs
- [ ] Update References section to point to language hubs

### Description Enhancement
- [ ] Add trigger words: "characterization testing", "testing combinations"
- Suggested: `Writes approval tests (snapshot/golden master testing) for Python, JavaScript/TypeScript, or Java. Use when verifying complex output, characterization testing legacy code, testing combinations, or working with .approved/.received files.`

---

## Create Language Hub Files

### Create: references/python.md
*Navigation hub with standalone value - not just links*

Content:
- [ ] Python quick start (verify, verify_as_json)
- [ ] Common imports block
- [ ] Python-specific gotchas (e.g., __str__ vs verify_as_json)
- [ ] Links to deeper references:
  - API details → python/api.md
  - Scrubbing → python/scrubbers.md
  - Inline approvals → python/inline.md
  - Logging verification → python/logging.md
  - Advanced patterns → python/advanced.md

### Create: references/nodejs.md
- [ ] Node.js/TypeScript quick start
- [ ] Common imports (approvals module)
- [ ] Jest/Mocha integration notes
- [ ] Links to deeper references

### Create: references/java.md
- [ ] Java quick start
- [ ] Common imports (org.approvaltests)
- [ ] JUnit 5 integration notes
- [ ] Links to deeper references

---

## New Python Reference Files

### Create: python/logging.md
*Load when: testing logs or tracing method calls*

- [ ] verify_simple_logger() context manager
- [ ] SimpleLogger.variable() for debugging
- [ ] SimpleLogger.use_markers() for method tracing
- [ ] verify_logging() for standard library logging
- [ ] Combining logs with results (3 approaches)

### Create: python/advanced.md
*Load when: multiple approvals, parametrized tests, configuration*

- [ ] NamerFactory.with_parameters() - multiple approvals per test
- [ ] gather_all_exceptions_and_throw - non-blocking verification
- [ ] settings().allow_multiple_verify_calls_for_this_method()
- [ ] Parametrized pytest tests integration
- [ ] approvaltests_config.json for subdirectories
- [ ] set_default_reporter() configuration

---

## Existing Reference Improvements

### python/scrubbers.md
- [ ] Add supported date formats table (15+ formats)
- [ ] Document DateScrubber.add_scrubber() for custom formats

### python/setup.md
- [ ] Move to python/setup.md (language-specific)
- [ ] Add approvaltests_config.json example
- [ ] Add conftest.py default reporter pattern

### patterns/testing-patterns.md
- [ ] Add "Multiple Approvals Per Test" pattern (brief, link to python/advanced.md)
- [ ] Add "Logs + Results" pattern (brief, link to python/logging.md)

---

## Items Removed (Too Niche)

These don't justify context cost:
- ~~MarkdownTable~~ - very specialized
- ~~CLI invocation~~ - rare cross-stack use case
- ~~verify_argument_parser~~ - too specific

---

## TODO: Port to Other Languages

After Python hub complete:

### Node.js Deep References
- [ ] nodejs/logging.md (if equivalent exists)
- [ ] nodejs/advanced.md

### Java Deep References
- [ ] java/logging.md (if equivalent exists)
- [ ] java/advanced.md

---

## Priority Order

### Phase 1: Restructure
- [ ] Create references/python.md (hub)
- [ ] Move language-specific content from SKILL.md to python.md
- [ ] Update SKILL.md to be language-agnostic

### Phase 2: New Python References
- [ ] Create python/logging.md
- [ ] Create python/advanced.md

### Phase 3: Improve Existing
- [ ] Enhance python/scrubbers.md with date formats table
- [ ] Update patterns/testing-patterns.md

### Phase 4: Other Languages
- [ ] Create references/nodejs.md (hub)
- [ ] Create references/java.md (hub)
- [ ] Review/update their deep references

---

## Validation Checklist

- [ ] SKILL.md is language-agnostic (universal concepts only)
- [ ] Language hubs have standalone value (not just links)
- [ ] Deep references have single responsibility
- [ ] No content duplication across files
- [ ] Each file is concise (assumes Claude is smart)
- [ ] SKILL.md stays under 500 lines
