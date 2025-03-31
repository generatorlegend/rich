# Progress and Status Displays

Rich provides powerful tools for creating progress bars and status displays in your console applications. This guide will walk you through creating and customizing progress bars, handling multiple progress bars, and using the Live class for updating displays.

## Progress Bars

### Creating a Simple Progress Bar

To create a basic progress bar, use the `Progress` class:

```python
from rich.progress import Progress

with Progress() as progress:
    task = progress.add_task("[red]Downloading...", total=100)
    for i in range(100):
        progress.update(task, advance=1)
```

This will display a progress bar with a description, percentage, and estimated time remaining.

### Customizing Progress Bar Appearance

You can customize the appearance of your progress bar by specifying columns:

```python
from rich.progress import Progress, BarColumn, TextColumn, TimeRemainingColumn

progress = Progress(
    TextColumn("[bold blue]{task.description}", justify="right"),
    BarColumn(bar_width=None),
    "[progress.percentage]{task.percentage:>3.0f}%",
    TimeRemainingColumn()
)
```

### Multiple Progress Bars

Rich can display multiple progress bars simultaneously:

```python
with Progress() as progress:
    task1 = progress.add_task("[red]Downloading...", total=100)
    task2 = progress.add_task("[green]Processing...", total=100)
    task3 = progress.add_task("[cyan]Uploading...", total=100)

    while not progress.finished:
        progress.update(task1, advance=0.5)
        progress.update(task2, advance=0.3)
        progress.update(task3, advance=0.9)
```

### Tracking File Downloads

For tracking file downloads, use the `DownloadColumn`:

```python
from rich.progress import Progress, DownloadColumn, TransferSpeedColumn, TimeRemainingColumn

progress = Progress(
    TextColumn("[bold blue]{task.description}"),
    BarColumn(),
    DownloadColumn(),
    TransferSpeedColumn(),
    TimeRemainingColumn()
)
```

## Status Displays

### Creating a Status Display

Use the `Status` class to create a status display with a spinner:

```python
from rich.status import Status

with Status("Processing...") as status:
    # Perform some work
    status.update(status="Completed!", spinner="tada")
```

### Customizing Status Display

You can customize the spinner and style of the status display:

```python
from rich.status import Status

with Status("Loading...", spinner="dots", style="bold green") as status:
    # Perform some work
    status.update(status="Ready!", spinner="star", style="bold blue")
```

## Live Displays

The `Live` class allows you to create auto-updating displays:

```python
from rich.live import Live
from rich.table import Table
import time

table = Table()
table.add_column("Row ID")
table.add_column("Description")
table.add_column("Status")

with Live(table, refresh_per_second=4) as live:
    for row in range(12):
        time.sleep(0.4)
        table.add_row(f"{row}", f"Task #{row+1}", "[bold green]DONE")
        live.update(table)
```

This will display a continuously updating table in the console.

## Advanced Usage

### Progress Callbacks

You can use callbacks to update progress based on external events:

```python
def process_chunk(chunk):
    # Process the chunk
    size = len(chunk)
    progress.update(task_id, advance=size)

with Progress() as progress:
    task_id = progress.add_task("[green]Processing chunks...", total=total_size)
    for chunk in get_chunks():
        process_chunk(chunk)
```

### Transient Progress Bars

For short-lived progress displays, use the `transient=True` parameter:

```python
with Progress(transient=True) as progress:
    task = progress.add_task("Working...", total=100)
    for i in range(100):
        progress.update(task, advance=1)
```

This will clear the progress bar after completion.

## Conclusion

Rich's progress and status display features provide a flexible and powerful way to create informative and visually appealing console output. By combining these tools, you can create sophisticated and responsive command-line interfaces for your Python applications.