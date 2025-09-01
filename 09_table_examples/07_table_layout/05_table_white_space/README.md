# Table Overflow Handling

This lesson demonstrates how to control content that overflows a table cell.

## What you'll learn

- The default overflow behavior in table cells.
- Using `overflow: hidden` to clip content.
- Using `overflow: auto` to add scrollbars inside a cell.
- Combining overflow with fixed heights/widths.

## Explanation

- By default, table cells expand to fit content.
- To keep table dimensions stable, you can:
  - Clip extra content with `overflow: hidden`.
  - Allow scrollbars inside the cell with `overflow: auto`.
- These strategies require fixed sizes (width/height) on the cell or column.

## How to run

Open `index.html` in your browser.  
You’ll see three columns:

1. Default overflow (cell expands).
2. Hidden overflow (content clipped).
3. Scroll overflow (scrollbar appears inside cell).

## Notes

- Use clipping or scrollbars only when you must strictly enforce dimensions.
- Otherwise, let cells expand naturally for better readability.
