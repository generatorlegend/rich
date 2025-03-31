# Text Styling in Rich

Rich provides powerful text styling capabilities that allow you to create visually appealing and informative console output. This guide will explain how to style text using Rich, including applying colors, formatting, and creating compound styles.

## Basic Styling

Rich offers two main ways to style text: using markup and using the `Style` class.

### Markup

Markup is a simple and intuitive way to add styling to your text. It uses square brackets to define style tags.

```python
from rich import print

print("[bold]Bold text[/bold]")
print("[italic]Italic text[/italic]")
print("[bold red]Bold red text[/bold red]")
```

### Style Class

For more programmatic control, you can use the `Style` class:

```python
from rich.console import Console
from rich.style import Style

console = Console()
style = Style(color="green", bold=True)
console.print("Styled text", style=style)
```

## Colors

Rich supports a wide range of colors, including named colors and RGB values.

```python
print("[red]Red text[/red]")
print("[#FF00FF]Magenta text[/#FF00FF]")
```

You can also set background colors:

```python
print("[on blue]Text with blue background[/on blue]")
```

## Text Formatting

Rich supports various text formatting options:

- `bold`
- `italic`
- `underline`
- `strike`
- `reverse` (inverts foreground and background colors)
- `blink`
- `dim`

Example:

```python
print("[bold underline]Bold and underlined[/bold underline]")
```

## Compound Styles

You can combine multiple styles:

```python
print("[bold italic red on white]Complex styling[/bold italic red on white]")
```

## Using the Text Class

For more advanced styling and manipulation, use the `Text` class:

```python
from rich.console import Console
from rich.text import Text

console = Console()
text = Text("Hello, World!")
text.stylize("bold magenta", 0, 5)  # Style "Hello"
text.stylize("italic green", 7, 12)  # Style "World"
console.print(text)
```

## Applying Styles Programmatically

You can apply styles to `Text` objects using methods:

```python
text = Text("Important message")
text.stylize(Style(color="red", blink=True, bold=True))
```

## Style Inheritance

Styles can be nested, with inner styles inheriting from outer styles:

```python
print("[bold]Bold text with [italic]bold and italic[/italic] text[/bold]")
```

## Escaping Markup

To display square brackets without interpreting them as markup, you can escape them:

```python
print("This is not \\[markup\\]")
```

## Conclusion

Rich's text styling capabilities allow you to create visually rich console output easily. By combining colors, formatting options, and compound styles, you can design informative and attractive text-based interfaces for your Python applications.

Remember to import the necessary components from Rich and experiment with different style combinations to achieve the desired look for your console output.