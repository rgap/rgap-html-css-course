# Table Column Sizing: What Works and What Doesn’t

This lesson explains **what actually works** when trying to control table column widths, and why `max-width` on `<col>` is misleading.

## What you’ll learn

- How HTML table layout calculates column widths.
- Why `max-width` and `min-width` on `<col>` are **ignored** by browsers.
- Reliable ways to cap a column’s width.
- Alternatives when you need “max but can shrink” behavior.

## The uncomfortable truth

- `<col>` is not a normal box; it’s a **hint** to the table layout algorithm.
- With `table-layout: fixed`, browsers honor **`width`** on `<col>` (or widths on first-row cells).
- **`max-width` and `min-width` on `<col>` are ignored** by the layout algorithm. Columns can exceed `max-width` and go below `min-width` despite those rules.
- That’s why your column still grew to 599px even with `max-width: 400px`.

## Reliable patterns

1. **Hard cap a column (fixed size)**  
   Use `width` on `<col>`:
   ```css
   table {
     table-layout: fixed;
   }
   col.first {
     width: 400px;
   } /* hard cap: reliable */
   ```
