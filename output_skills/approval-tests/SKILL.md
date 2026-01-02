---
name: approval-tests
description: Write approval tests (snapshot testing) for Python, JavaScript/TypeScript, or Java. Use when verifying complex output, testing with golden masters, or working with .approved/.received files.
---

# Approval Tests

## Philosophy

"A picture's worth 1000 assertions."

Approval tests verify complex output by comparing against a saved "golden master" file instead of writing individual assertions. You capture the output once, review it, approve it, and future runs compare against that approved snapshot.

**Use approval tests when:**
- Output is complex (JSON, XML, formatted text, multiple fields)
- You're characterizing legacy code behavior
- Testing combinations of inputs
- Assertions would be tedious or brittle

**Use assertions when:**
- Testing simple values
- Testing specific edge cases
- Output is non-deterministic and can't be scrubbed

## Core Workflow

```
1. Write test with verify(result)
2. Run test → FAILS (no .approved file yet)
3. Creates: TestName.approved.txt (empty) + TestName.received.txt (actual output)
4. Review .received file - is this correct?
5. YES → rename/copy .received to .approved
6. Run test again → PASSES
7. Commit .approved file to version control
```

**File naming convention:**
```
{TestClass}.{test_method}.approved.txt   ← commit this
{TestClass}.{test_method}.received.txt   ← gitignore this
```

**Critical rules:**
- `.approved` files ARE your test expectations - commit them
- `.received` files are temporary - add `*.received.*` to .gitignore
- Never edit `.approved` files by hand - always generate via test

## Quick Start

**Python:**
```python
from approvaltests import verify

def test_report():
    result = generate_report()
    verify(result)
```

**JavaScript/TypeScript:**
```javascript
const approvals = require('approvals');

it('generates report', function() {
    const result = generateReport();
    approvals.verify(__dirname, 'test_report', result);
});
```

**Java:**
```java
import org.approvaltests.Approvals;

@Test
void testReport() {
    String result = generateReport();
    Approvals.verify(result);
}
```

**First run:** Test fails, `.received` file created. Review it, approve it, rerun.

## When Approval Tests Shine

**Complex objects** - Instead of asserting 20 fields:
```python
# Bad: tedious, brittle
assert user.name == "Alice"
assert user.email == "alice@example.com"
assert user.created_at == ...
# ... 17 more assertions

# Good: verify the whole thing
verify_as_json(user)
```

**Characterization tests** - Capture legacy behavior before refactoring:
```python
def test_legacy_billing():
    result = legacy_billing_system.calculate(test_data)
    verify(result)  # Captures current behavior as baseline
```

**Combinatorial testing** - Test all input combinations:
```python
verify_all_combinations(
    process_order,
    sizes=["S", "M", "L"],
    colors=["red", "blue"],
    shipping=["standard", "express"]
)
```

## Common Patterns

### verify() - Basic string/object verification
```python
verify(result)                    # String output
verify(str(complex_object))       # Object as string
```

### verify_as_json() - Objects as formatted JSON
```python
verify_as_json(user)              # Pretty-printed JSON
verify_as_json(list_of_users)     # Works with collections
```

### verify_all() - Collections with labels
```python
verify_all("Users", users, lambda u: f"{u.name}: {u.email}")
```

### Scrubbing non-deterministic data
Timestamps, GUIDs, and random values break approval tests. Use scrubbers:
```python
from approvaltests import verify, Options
from approvaltests.scrubbers import scrub_all_dates

verify(result, options=Options().with_scrubber(scrub_all_dates))
```

See language-specific reference for scrubber details.

## Language Detection

Determine language from project context:
- `pyproject.toml`, `setup.py`, `requirements.txt` → Python
- `package.json` → JavaScript/TypeScript
- `pom.xml`, `build.gradle` → Java

Then read the appropriate reference for accurate API details.

## References

**Language-specific API and setup:**
- Python: [references/python/api.md](references/python/api.md) | [setup](references/python/setup.md)
- Node.js: [references/nodejs/api.md](references/nodejs/api.md) | [setup](references/nodejs/setup.md)
- Java: [references/java/api.md](references/java/api.md) | [setup](references/java/setup.md)

**Advanced patterns:**
- Inline approvals: [python](references/python/inline.md) | [nodejs](references/nodejs/inline.md) | [java](references/java/inline.md)
- Scrubbers: [python](references/python/scrubbers.md) | [nodejs](references/nodejs/scrubbers.md) | [java](references/java/scrubbers.md)
- Combinations: [references/patterns/combinations.md](references/patterns/combinations.md)

## Anti-Patterns

**Don't write assertions for complex objects:**
```python
# Bad
assert json.loads(result)["users"][0]["name"] == "Alice"
assert json.loads(result)["users"][0]["email"] == "alice@example.com"

# Good
verify_as_json(result)
```

**Don't commit .received files** - They're temporary test artifacts.

**Don't forget scrubbers for timestamps/GUIDs:**
```python
# Bad - will fail randomly
verify(f"Created at: {datetime.now()}")

# Good - scrub the date
verify(result, options=Options().with_scrubber(scrub_all_dates))
```

**Don't over-verify** - One approval per logical behavior, not one per line of output.

**Don't hand-edit .approved files** - Always generate through running tests.
