# Border Types Demo

This lesson compares different ways of applying borders to HTML tables:

- no borders at all
- borders on the `<table>` only
- borders on the cells only
- borders on the rows only
- a combination of table + cell borders
- all borders together

## What you'll learn

- How a border on the `<table>` only creates an **outer frame**.
- How borders on `<th>, <td>` create the **grid lines** inside the table.
- How a border on `<tr>` gives **horizontal row lines**.
- How combining these rules changes the table’s look.
- Which combination is best depending on your design.

## Explanation

- **0. No borders**: plain table, padding only.
- **1. Table border only**: single box around the whole table.
- **2. Cell borders only**: grid lines inside, but no outside frame.
- **3. Row borders only**: horizontal separators, no vertical grid lines.
- **4. Table + cell borders**: outer frame plus internal grid.
- **5. All borders (table + cells + rows)**: every possible border, full separation.

## How to run

Open `index.html` in your browser.  
You’ll see six versions of the same table:

0. No borders
1. Table border only
2. Cell borders only
3. Row borders only
4. Table + cell borders
5. All borders

## Notes

- For **data tables**, usually _table + cell borders_ (option 4) looks the clearest.
- For **visual cards or layouts**, outer-only (option 1) is often enough.
- Row-only (option 3) can work well for **lists** where horizontal separation matters more than vertical separation.
