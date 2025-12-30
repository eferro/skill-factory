# UV Scripts

Standalone Python scripts with automatic dependency management. No virtualenv, no requirements.txt.

## Contents
- Basic execution
- Inline metadata (PEP 723)
- Ad-hoc dependencies
- Executable scripts
- Locking for reproducibility
- Python version control

## Basic Execution

```bash
uv run script.py                      # Run script
uv run script.py arg1 arg2            # With arguments
uv run --no-project script.py         # Skip project context
```

## Inline Metadata (PEP 723)

Declare dependencies directly in the script:

```python
#!/usr/bin/env -S uv run --script
# /// script
# requires-python = ">=3.12"
# dependencies = ["requests", "rich"]
# ///

import requests
from rich import print
```

Initialize a new script with metadata:
```bash
uv init --script example.py --python 3.12
```

Add dependencies to existing script:
```bash
uv add --script example.py requests rich
```

## Ad-hoc Dependencies

For quick runs without modifying the script:

```bash
uv run --with rich script.py
uv run --with 'requests>=2.28,<3' script.py
uv run --with requests --with rich script.py
```

## Executable Scripts

Make scripts directly runnable:

```python
#!/usr/bin/env -S uv run --script
# /// script
# dependencies = ["click"]
# ///

import click

@click.command()
def main():
    click.echo("Hello!")

if __name__ == "__main__":
    main()
```

```bash
chmod +x script.py
./script.py
```

## Locking for Reproducibility

Create a lockfile for the script:
```bash
uv lock --script example.py
```

Creates `example.py.lock` with exact versions.

Time-based reproducibility in metadata:
```python
# /// script
# dependencies = ["requests"]
# [tool.uv]
# exclude-newer = "2024-01-15T00:00:00Z"
# ///
```

## Python Version Control

```bash
uv run --python 3.11 script.py        # Specific version
uv run --python pypy script.py        # Alternative interpreter
```

Or in metadata:
```python
# /// script
# requires-python = ">=3.11,<3.13"
# ///
```

## Alternative Package Indexes

```bash
uv add --index "https://example.com/simple" --script example.py package
```

Or in metadata:
```python
# /// script
# dependencies = ["private-package"]
#
# [[tool.uv.index]]
# url = "https://example.com/simple"
# ///
```

## Platform Notes

- Windows: `.pyw` files run with `pythonw` automatically (no console)
- Shebangs work on Unix/macOS; Windows uses file associations
