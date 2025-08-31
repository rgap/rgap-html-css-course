# Colgroup

This lesson shows how to use `<colgroup>` and `<col>` to control table column widths and styles.

## What you'll learn

- How `<colgroup>` groups table columns.
- How `<col>` can define width and styles for each column.
- Why column-level styling is useful.

## Explanation

- `<colgroup>` goes inside `<table>`, before `<thead>`, `<tbody>`, etc.
- Each `<col>` matches a column in the table, from left to right.
- Attributes like `width` or CSS styles can be applied to `<col>`.
- Useful when you want all cells in a column styled the same way (e.g., background color, width).

## How to run

Open `index.html` in your browser.  
You’ll see a table with:

- First column wider.
- Second column highlighted with a background color.
- Third column narrower.

## Notes

- `<col>` cannot contain content (only attributes/styles).
- If fewer `<col>` elements are defined than actual columns, the remaining columns are unaffected.
