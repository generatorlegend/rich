# Syntax Highlighting

Rich provides powerful syntax highlighting capabilities for displaying code snippets in the terminal. This feature allows you to render code with colorful and informative syntax highlighting, making it easier to read and understand.

## Basic Usage

To use syntax highlighting in Rich, you can use the `Syntax` class from the `rich.syntax` module. Here's a simple example:

```python
from rich.console import Console
from rich.syntax import Syntax

console = Console()

code = """
def hello_world():
    print("Hello, World!")
"""

syntax = Syntax(code, "python", theme="monokai")
console.print(syntax)
```

This will display the Python code with syntax highlighting using the "monokai" theme.

## Supported Languages

Rich uses Pygments under the hood for syntax highlighting, which supports a wide range of programming languages and file formats. You can specify the language either by name or by file extension. For example:

```python
Syntax(code, "python")  # Specify by language name
Syntax.from_path("example.py")  # Automatically detect based on file extension
```

If you're unsure about the language or want to let Rich guess, you can use the `guess_lexer` method:

```python
lexer = Syntax.guess_lexer("example.py", code)
syntax = Syntax(code, lexer)
```

## Customizing Themes

Rich comes with several built-in themes, including "monokai" (the default), "vim", "emacs", and more. You can specify a theme when creating a `Syntax` object:

```python
syntax = Syntax(code, "python", theme="vim")
```

You can also create custom themes by subclassing `pygments.style.Style` and defining your own color scheme.

## Additional Features

### Line Numbers

You can display line numbers alongside your code:

```python
syntax = Syntax(code, "python", line_numbers=True)
```

### Highlighting Specific Lines

To highlight specific lines in your code:

```python
syntax = Syntax(code, "python", highlight_lines={1, 3, 5})
```

### Word Wrap

Enable word wrapping for long lines:

```python
syntax = Syntax(code, "python", word_wrap=True)
```

### Indent Guides

Show indent guides in your code:

```python
syntax = Syntax(code, "python", indent_guides=True)
```

## Integration with Other Rich Features

Syntax highlighting can be easily integrated with other Rich features:

### In Tables

```python
from rich.table import Table

table = Table(title="Code Samples")
table.add_column("Language", style="cyan")
table.add_column("Code", style="magenta")

table.add_row("Python", Syntax(python_code, "python"))
table.add_row("JavaScript", Syntax(js_code, "javascript"))

console.print(table)
```

### In Panels

```python
from rich.panel import Panel

panel = Panel(Syntax(code, "python"), title="Python Code", expand=False)
console.print(panel)
```

## Command-Line Interface

Rich also provides a command-line interface for syntax highlighting. You can use it to highlight files or input from stdin:

```bash
python -m rich.syntax example.py
```

This will display the contents of `example.py` with syntax highlighting in your terminal.

## Conclusion

Rich's syntax highlighting feature offers a flexible and powerful way to display code in your terminal applications. By leveraging Pygments' extensive language support and customizable themes, you can create visually appealing and informative code displays that integrate seamlessly with other Rich components.