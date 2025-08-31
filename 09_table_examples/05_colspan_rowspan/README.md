# Colspan & Rowspan

This lesson introduces how to merge table cells using the **`colspan`** and **`rowspan`** attributes.

## What you'll learn

- `colspan="N"` → merge a cell across N columns (horizontally).
- `rowspan="N"` → merge a cell across N rows (vertically).
- How merging affects the table’s grid structure.

## Explanation

- Use `colspan` when you want one cell to span multiple columns in the same row.
  Example: a header cell spanning two columns.
- Use `rowspan` when you want one cell to extend across multiple rows.
  Example: a “Category” column covering multiple items.

## How to run

Open `index.html` in your browser.  
You’ll see two examples:

1. A header that uses `colspan` to merge cells.
2. A column that uses `rowspan` to merge cells.

## Notes

- After using `colspan`/`rowspan`, other cells must adjust so the total columns per row stay consistent.
- Overusing merged cells can hurt readability.
