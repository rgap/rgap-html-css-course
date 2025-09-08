# Table Nested Tables

This lesson shows how to insert a table inside another table cell.

## What you'll learn

- How to structure nested tables in HTML.
- Why nested tables can be useful (e.g., grouping details inside a summary row).
- Styling tips to avoid visual clutter.

## Explanation

- Nested tables are simply `<table>` elements placed inside `<td>`.
- The outer table provides the main layout, while the inner table gives detail for a single cell.
- This was a common technique in early web design, but today it’s mostly used for **emails** or complex reports.

## How to run

Open `index.html` in your browser.  
You’ll see an outer table with two products.  
The second product’s cell contains a nested table with extra details.

## Notes

- Nested tables increase complexity → avoid unless necessary.
- For modern UIs, consider CSS grid or flexbox for complex layouts.
- Always style nested tables separately to keep borders clean.
