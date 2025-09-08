# Border Collapse vs Separate

This lesson focuses only on the difference between:

- `border-collapse: collapse`
- `border-collapse: separate`

## What you'll learn

- How `collapse` merges adjacent borders into a single line.
- How `separate` keeps each cell’s borders distinct.
- Why collapsed borders are usually cleaner for data tables.
- Why separate borders can be useful with `border-spacing`.

## Explanation

- **Collapsed**

  - Borders between cells merge into one line.
  - Avoids “double borders.”
  - Common for spreadsheets and dashboards.

- **Separate**
  - Each cell keeps its own border.
  - Allows gaps between cells using `border-spacing`.
  - Default mode if you don’t specify anything.

## How to run

Open `index.html` in your browser.  
You’ll see two identical tables side by side — one collapsed, one separate.

## Notes

- `collapse` is the standard look for grid-like data tables.
- `separate` is more common when you want card-like cells or spacing.
