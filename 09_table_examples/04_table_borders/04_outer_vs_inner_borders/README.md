# Outer vs Inner Borders

This lesson compares applying borders to the `<table>` element itself versus applying them to the table cells (`<th>`, `<td>`).

## What you'll learn

- How a border on the `<table>` only creates an **outer box**.
- How borders on `th, td` create the **grid lines** inside the table.
- How combining both gives a full framed grid.

## Explanation

- **Outer only**: border on `<table>`. No grid lines inside, just a box around the table.
- **Inner only**: borders only on `<th>, <td>`. Grid visible inside, but no outside frame.
- **Both**: table has an outer border, cells have inner borders → full grid with frame.

## How to run

Open `index.html` in your browser.  
You’ll see three versions of the same table:

1. Outer border only
2. Inner borders only
3. Combined (outer + inner)

## Notes

- For clean data tables, use **both**.
- For card-like layouts, sometimes outer-only is enough.
