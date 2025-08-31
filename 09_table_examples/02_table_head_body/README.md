# Lesson 02 – Table Head & Body + Borders

This lesson introduces two key concepts:

1. **Structure with `<thead>` and `<tbody>`**
   - `<thead>` groups the header rows of a table.
   - `<tbody>` groups the main data rows.
   - `<th>` defines header cells (bold + centered by default).
   - `<td>` defines normal data cells.

2. **The `border` attribute**
   - Adding `border="1"` to `<table>` draws cell borders.
   - This is an older HTML technique (fine for demos).
   - Modern practice is to use CSS (`border`, `border-collapse`).

## What you'll learn
- Use `<thead>` and `<tbody>` for better structure.
- Difference between `<th>` and `<td>`.
- How `border="1"` works and why CSS borders are preferred.

## How to run
Open `index.html` in your browser.  
You’ll see a small product/price table with visible borders.

## Notes
- Screen readers treat `<th>` as headers and announce them correctly.
- In later lessons we’ll add `<tfoot>` for totals.
- In Lesson 04 we’ll style borders properly with CSS.
