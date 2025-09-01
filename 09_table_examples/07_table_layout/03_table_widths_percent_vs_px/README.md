# Table Widths: Percent vs PX

This lesson compares **percentage-based widths** and **pixel-based widths** in tables, with the table width set to **1000px**.

## What you'll learn

- How `%` widths scale with the container.
- How `px` widths stay fixed regardless of container size.
- Why `table-layout: fixed` often pairs better with explicit column widths.

## Explanation

- **Percent widths**
  - Column width is a fraction of the table width (1000px in this demo).
  - Example: 20% = 200px, 50% = 500px, 30% = 300px.
  - Great for responsive layouts that adapt to parent size.
- **Pixel widths**
  - Exact, fixed width for columns; layout does not scale automatically.
  - Example: 250px + 450px + 300px = 1000px total.
  - Useful for aligning to precise measurements where consistency matters.

## How to run

Open `index.html` in your browser.  
Resize the window to compare how the two tables behave:

1. **Percent-only** (20% / 50% / 30%)
2. **Pixel-only** (250px / 450px / 300px)

## Notes

- With `table-layout: auto` (default), the browser may adjust column widths based on content.
- `table-layout: fixed` enforces widths from CSS/colgroup and is faster for large tables.
- Long words may overflow; later lessons cover wrapping and ellipsis.
