# Python Scrubbers

Scrubbers normalize non-deterministic data (timestamps, GUIDs, random values) before comparison.

## Imports

```python
from approvaltests import verify, Options
from approvaltests.scrubbers import (
    create_regex_scrubber,
    scrub_all_dates,
    scrub_all_guids,
    combine_scrubbers,
    create_line_scrubber,
)
from approvaltests.scrubbers.date_scrubber import DateScrubber
```

## Built-in Scrubbers

### scrub_all_dates

Replaces `YYYY-MM-DD HH:MM:SS` format with `<date0>`, `<date1>`, etc.

```python
verify(
    "Created: 2024-01-15 10:30:00",
    options=Options().with_scrubber(scrub_all_dates)
)
# Output: Created: <date0>
```

### scrub_all_guids

Replaces UUIDs with `<guid_0>`, `<guid_1>`, etc. Duplicate GUIDs get same replacement.

```python
verify(
    "ID: 2fd78d4a-ad49-447d-96a8-deda585a9aa5",
    options=Options().with_scrubber(scrub_all_guids)
)
# Output: ID: <guid_0>
```

## DateScrubber

Smart date detection for many formats:

```python
# Auto-detect format from example
scrubber = DateScrubber.get_scrubber_for("03:14:15")

verify(
    "Started at 10:30:45",
    options=Options().with_scrubber(scrubber)
)
# Output: Started at <date0>
```

### Supported Date Formats

| Example | Pattern |
|---------|---------|
| `23:30:00` | HH:MM:SS |
| `2020-02-02` | YYYY-MM-DD |
| `2020-09-10T08:07:89Z` | ISO 8601 |
| `Tue May 13 16:30:00 2014` | Day Mon DD HH:MM:SS YYYY |
| `May 13, 2014 11:30:00 PM PST` | Mon DD, YYYY HH:MM:SS AM/PM TZ |
| And 10+ more... | |

### Custom Date Format

```python
DateScrubber.add_scrubber(
    "2025-07-20",           # Example
    r"\d{4}-\d{2}-\d{2}",   # Regex pattern
    display_message=False
)

scrubber = DateScrubber.get_scrubber_for("2025-07-20")
```

## Custom Regex Scrubber

### With Static Replacement

```python
scrubber = create_regex_scrubber(
    r"user_\d+",      # Pattern
    "<USER>"          # Replacement
)

verify("Created by user_12345", options=Options().with_scrubber(scrubber))
# Output: Created by <USER>
```

### With Numbered Replacement

```python
scrubber = create_regex_scrubber(
    r"user_\d+",
    lambda n: f"<user_{n}>"  # n = match index (0, 1, 2...)
)

verify(
    "user_123 assigned to user_456",
    options=Options().with_scrubber(scrubber)
)
# Output: <user_0> assigned to <user_1>
```

## Line Scrubber

Remove entire lines containing a substring:

```python
scrubber = create_line_scrubber("password")

verify(
    "user: admin\npassword: secret123\nemail: a@b.com",
    options=Options().with_scrubber(scrubber)
)
# Output:
# user: admin
# email: a@b.com
```

## Combining Scrubbers

### Using combine_scrubbers()

```python
scrubber = combine_scrubbers(
    scrub_all_guids,
    scrub_all_dates,
    create_regex_scrubber(r"secret_\w+", "[REDACTED]"),
)

verify(data, options=Options().with_scrubber(scrubber))
```

### Using add_scrubber()

```python
options = (Options()
    .add_scrubber(scrub_all_guids)
    .add_scrubber(scrub_all_dates)
    .add_scrubber(create_line_scrubber("DEBUG")))

verify(data, options=options)
```

## Custom Scrubber Function

Any function `str -> str` works as a scrubber:

```python
def my_scrubber(text: str) -> str:
    return text.replace("PRODUCTION", "[ENV]")

verify(data, options=Options().with_scrubber(my_scrubber))
```

## Common Patterns

### Scrub Timestamps in JSON

```python
verify_as_json(
    response_data,
    options=Options().with_scrubber(scrub_all_dates)
)
```

### Scrub Multiple Dynamic Fields

```python
scrubber = combine_scrubbers(
    scrub_all_guids,
    scrub_all_dates,
    create_regex_scrubber(r'"id":\s*\d+', '"id": <ID>'),
    create_regex_scrubber(r'"token":\s*"[^"]+"', '"token": "<TOKEN>"'),
)
```

### Scrub Log Output

```python
scrubber = combine_scrubbers(
    DateScrubber.get_scrubber_for("2024-01-15 10:30:00"),
    create_line_scrubber("DEBUG"),
    create_line_scrubber("TRACE"),
)
```
