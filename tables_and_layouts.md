# Tables and Layouts in Rich

Rich provides powerful tools for creating and customizing tables and other layout elements in your console applications. This guide will walk you through the process of creating tables, styling columns and rows, and using advanced features like span and overflow handling.

## Tables

The `Table` class in Rich allows you to create highly customizable tables with various styling options.

### Creating a Basic Table

To create a basic table, you can use the `Table` class:

```python
from rich.console import Console
from rich.table import Table

table = Table(title="My Table")

table.add_column("Name", style="cyan")
table.add_column("Age", style="magenta")
table.add_column("City", style="green")

table.add_row("Alice", "30", "New York")
table.add_row("Bob", "25", "Los Angeles")
table.add_row("Charlie", "35", "Chicago")

console = Console()
console.print(table)
```

This will create a table with three columns and three rows, with a title and styled column headers.

### Customizing Table Appearance

You can customize various aspects of the table's appearance:

```python
table = Table(
    title="Customized Table",
    caption="Table Caption",
    show_header=True,
    header_style="bold magenta",
    show_lines=True,
    expand=True,
    border_style="green",
    row_styles=["dim", "none"],
)
```

This creates a table with:
- A title and caption
- Visible headers with a custom style
- Lines between rows
- Expanded width
- Green border
- Alternating row styles

### Column Styling

You can style individual columns when adding them to the table:

```python
table.add_column("Name", style="cyan", justify="left")
table.add_column("Age", style="magenta", justify="center")
table.add_column("City", style="green", justify="right")
```

This sets different text colors and justification for each column.

### Row Styling

You can apply styles to entire rows:

```python
table.add_row("Alice", "30", "New York", style="on blue")
table.add_row("Bob", "25", "Los Angeles", style="on red")
```

This sets a background color for each row.

### Advanced Features

#### Span and Overflow

Rich provides options for handling cell content that exceeds column width:

```python
table = Table(show_header=True, header_style="bold magenta")
table.add_column("Name", style="dim", width=12)
table.add_column("Description", style="dim", width=20, overflow="fold")

table.add_row("Alice", "A very long description that will be folded")
table.add_row("Bob", "Short description")
```

The `overflow="fold"` option will wrap text that exceeds the column width.

#### Column Groups

You can create column groups to span multiple columns:

```python
table = Table(title="Column Groups Example")
table.add_column("Name", style="cyan")
table.add_column("Age", style="magenta")
table.add_column("City", style="green")
table.add_column("Country", style="yellow")

table.add_row("Alice", "30", "New York", "USA")
table.add_row("Bob", "25", "London", "UK")

table.columns[2].header_style = "bold red"
table.columns[3].header_style = "bold red"
table.columns[2].footer = "Location"
table.columns[3].footer = "Location"
```

This creates a group for the "City" and "Country" columns with a shared footer.

## Other Layout Elements

### Panels

Rich's `Panel` class allows you to create bordered sections of content:

```python
from rich.panel import Panel
from rich.text import Text

panel = Panel(
    Text("Hello, World!", style="bold red"),
    title="My Panel",
    subtitle="Panel Subtitle",
    expand=False,
    border_style="green",
)

console.print(panel)
```

This creates a panel with a title, subtitle, and custom border style.

### Columns

The `Columns` class helps you organize content into columns:

```python
from rich.columns import Columns

data = ["Apple", "Banana", "Cherry", "Date", "Elderberry", "Fig"]
columns = Columns(data, equal=True, expand=True)

console.print(columns)
```

This displays the list items in equal-width columns that expand to fill the console width.

## Conclusion

Rich provides a wide range of options for creating and customizing tables and layout elements. By combining these features, you can create visually appealing and informative console outputs for your Python applications.

For more detailed information on specific classes and methods, refer to the Rich API documentation.