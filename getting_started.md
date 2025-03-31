---
title: Getting Started with Rich
description: A comprehensive guide to installing and using Rich for beautiful terminal output in Python
---

# Getting Started with Rich

Rich is a Python library for rich text and beautiful formatting in the terminal. This guide will help you get started with Rich, covering installation, basic usage, and an overview of key features.

## Installation

To install Rich, use pip:

```bash
pip install rich
```

## Basic Usage

To start using Rich, import the `Console` class:

```python
from rich import console

console = console.Console()
```

Now you can use the `console` object to print formatted text:

```python
console.print("Hello, [bold magenta]World[/bold magenta]!")
```

This will output "Hello, World!" with "World" in bold magenta text.

## Key Features

### Text Styling

Rich supports a wide range of text styles and colors:

```python
console.print("This is [bold]bold[/bold], [italic]italic[/italic], and [underline]underlined[/underline] text.")
console.print("You can also use [red]colors[/red] and [on blue]background colors[/on blue].")
```

### Tables

Rich can create beautiful tables:

```python
from rich.table import Table

table = Table(title="My Fruits")
table.add_column("Name", style="cyan", no_wrap=True)
table.add_column("Color", style="magenta")
table.add_column("Taste", justify="right", style="green")

table.add_row("Apple", "Red", "Sweet")
table.add_row("Lemon", "Yellow", "Sour")
table.add_row("Grape", "Purple", "Sweet")

console.print(table)
```

### Progress Bars

Rich provides customizable progress bars:

```python
from rich.progress import track
import time

for step in track(range(100)):
    time.sleep(0.1)  # Simulate some work
```

This will display a progress bar that updates as the loop progresses.

### Logging

Rich can be used to enhance logging output:

```python
from rich.logging import RichHandler
import logging

logging.basicConfig(
    level="NOTSET",
    format="%(message)s",
    datefmt="[%X]",
    handlers=[RichHandler(rich_tracebacks=True)]
)

log = logging.getLogger("rich")
log.info("Hello, Rich!")
log.error("[bold red blink]Server is shutting down![/]")
```

## Next Steps

This guide covers just the basics of Rich. For more advanced features and detailed API documentation, check out the [Rich documentation](https://rich.readthedocs.io/).

Happy coding with Rich!