# Troubleshooting and FAQ

This page provides solutions to common issues and answers to frequently asked questions about using Rich. If you encounter any problems or have questions not covered here, please open an issue on the [Rich GitHub repository](https://github.com/Textualize/rich).

## Common Issues and Solutions

### 1. Text not displaying colors or styles

**Problem:** The text appears plain without any colors or styles when using Rich.

**Possible causes and solutions:**

a) Terminal doesn't support colors:
   - Ensure you're using a terminal that supports ANSI colors.
   - Try setting the `FORCE_COLOR` environment variable to `1`.

b) Windows-specific issues:
   - Make sure you're using Windows 10 or later with a modern terminal.
   - Enable ANSI color support by running `reg add HKCU\Console /v VirtualTerminalLevel /t REG_DWORD /d 1` in an admin command prompt.

c) Color system not detected correctly:
   - Manually set the color system using `Console(color_system="truecolor")` or `Console(color_system="256")`.

### 2. Unexpected line breaks or text wrapping

**Problem:** Text is not wrapping as expected or line breaks appear in unexpected places.

**Solutions:**

a) Check the `width` parameter:
   - Ensure you're not setting a `width` that's too narrow for your content.
   - Use `console.width` to get the current terminal width.

b) Use `no_wrap` option:
   - Set `no_wrap=True` when calling `print()` or `log()` to prevent automatic wrapping.

c) Adjust `overflow` method:
   - Try different overflow methods like "crop", "fold", or "ellipsis".

Example:
```python
from rich.console import Console

console = Console()
console.print("This is a long line of text that may wrap unexpectedly.", no_wrap=True, overflow="crop")
```

### 3. Performance issues with large outputs

**Problem:** Rich becomes slow when dealing with very large amounts of text or complex layouts.

**Solutions:**

a) Use `Live` for updating content:
   - Instead of repeatedly printing, use `Live` for dynamic content updates.

b) Limit the amount of styled text:
   - Apply styles to smaller portions of text rather than entire large strings.

c) Use `Text` objects for repeated styling:
   - Pre-create `Text` objects with styles for reuse instead of applying styles on every print.

Example:
```python
from rich.live import Live
from rich.table import Table
import time

table = Table()
table.add_column("Row")
table.add_column("Value")

with Live(table, refresh_per_second=4) as live:
    for i in range(100):
        table.add_row(str(i), str(i * i))
        time.sleep(0.25)
```

## Frequently Asked Questions

### 1. How do I change the default color theme?

You can create a custom theme by subclassing `Theme` and passing it to the `Console` constructor:

```python
from rich.console import Console
from rich.theme import Theme

custom_theme = Theme({
    "info": "dim cyan",
    "warning": "magenta",
    "danger": "bold red"
})

console = Console(theme=custom_theme)
console.print("This is an [info]info message[/info]")
```

### 2. Can I use Rich in Jupyter notebooks?

Yes, Rich works well in Jupyter notebooks. Make sure to create the `Console` with `jupyter=True`:

```python
from rich.console import Console
console = Console(jupyter=True)
```

### 3. How do I capture Rich output as a string?

Use the `capture` method of the `Console` class:

```python
from rich.console import Console

console = Console()
with console.capture() as capture:
    console.print("[bold red]Hello[/] World")
str_output = capture.get()
```

### 4. Can I use custom fonts or emojis with Rich?

Rich uses the fonts and emojis available in your terminal. It doesn't directly support custom fonts, but it does support emoji rendering if your terminal supports it. Use the `emoji` parameter when creating a `Console` to enable or disable emoji rendering:

```python
from rich.console import Console

console = Console(emoji=True)
console.print(":smiley: Hello, World! :thumbs_up:")
```

### 5. How do I handle multiline output in tables or panels?

Rich automatically handles multiline content in tables and panels. Just make sure to use `\n` for line breaks in your strings:

```python
from rich.console import Console
from rich.table import Table

console = Console()
table = Table(title="Multiline Content")
table.add_column("Name", style="cyan")
table.add_column("Description")
table.add_row("Rich", "Rich is a Python library for rich text and beautiful formatting\nin the terminal.")
table.add_row("Python", "Python is a programming language that lets you work quickly\nand integrate systems more effectively.")

console.print(table)
```

## Debugging Tips

1. Use `console.log()` instead of `print()` for debugging, as it provides additional context like file names and line numbers.

2. Set `RICH_TRACEBACK=1` environment variable to get detailed tracebacks with syntax highlighting.

3. Use `Console(record=True)` and `console.save_html()` to save the output as HTML for easier debugging of complex layouts.

4. When in doubt about the structure of your Rich content, use `print(repr(your_content))` to see a representation of the object.

If you're still experiencing issues after trying these solutions, please provide a minimal reproducible example when seeking help from the community or reporting a bug.