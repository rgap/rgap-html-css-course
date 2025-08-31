# Table Widths: Percent vs PX

This lesson compares **percentage-based widths** and **pixel-based widths** in tables.

## What you'll learn

- How `%` widths scale with the container.
- How `px` widths stay fixed regardless of container size.
- How mixed strategies behave (some columns in %, others in px).
- Why `table-layout: fixed` often pairs better with explicit column widths.

## Explanation

- **Percent widths**
  - Column width is a fraction of the table width (and the table may be a fraction of its parent).
  - Great for responsive layouts.
- **Pixel widths**
  - Exact, fixed width for columns; layout does not scale automatically.
  - Useful for aligning to specific measurements.
- **Mixed**
  - Use `px` for “must-fit” columns (e.g., icon/action column).
  - Use `%` for flexible content columns.

## How to run

Open `index.html` in your browser.
Resize the window to compare how the three tables behave:

1. Percent-only
2. Pixel-only
3. Mixed (% + px)

## Notes

- With `table-layout: auto` (default), the browser may adjust column widths based on content.
- `table-layout: fixed` enforces widths from CSS/colgroup and is faster for large tables.
- Long words may overflow; later lessons cover wrapping and ellipsis.
