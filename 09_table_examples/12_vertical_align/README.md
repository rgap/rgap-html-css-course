# Vertical Alignment in Table Cells

This lesson demonstrates how to align content vertically inside table cells,
especially when some cells have short text and others have longer content.

## What you'll learn

- How `vertical-align` controls placement inside a cell.
- The difference between `top`, `middle`, and `bottom`.
- Why vertical alignment matters when rows have uneven content.

## Explanation

- **top** → sticks content to the top of the cell.
- **middle** → centers content vertically (this is the default).
- **bottom** → sticks content to the bottom edge.

These values are most visible when comparing short vs long text in the same row.

## How to run

Open `index.html` in your browser.  
You’ll see a table with one short cell and one longer text cell, aligned with
`top`, `middle`, and `bottom`.

## Notes

- Vertical alignment only applies to table-cell elements (like `<td>` / `<th>`).
- It’s especially useful when combining short labels with multi-line descriptions.
- Use `top` for data tables with lots of wrapped text, so rows feel tidy.
